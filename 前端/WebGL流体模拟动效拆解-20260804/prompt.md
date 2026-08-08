# WebGL 流体模拟动效拆解（paveldogreat/WebGL-Fluid-Simulation）

> 2026-08-04 拆解沉淀。源码：`D:\Code\AI资源管理\libs\effects\webgl-fluid-simulation\`（script.js 1645 行，MIT）
> 效果：鼠标/触摸驱动的实时彩色流体，带发光(Bloom)与体积光(Sunrays)后处理，移动端可用

## 一、效果概览与适用场景

- 交互式流体（拖动产生旋涡与色彩混合），可用作：登录页背景、加载动画、Hero 视觉、互动展示
- 技术要点：WebGL2（回退 WebGL1）+ 半浮点纹理 + GPU 上的 Stable Fluids 求解
- 性能分级：SIM_RESOLUTION 128 / DYE_RESOLUTION 1024 为桌面档；移动端自动降为 512

## 二、结构拆解（渲染管线）

```
每帧 update():
  1. updateColors(dt)      → 颜色随时间演化（COLORFUL 模式，Hue 渐变）
  2. applyInputs()          → 处理鼠标/触摸 splat（喷射速度+染料）
  3. step(dt)               → 物理模拟（核心，见下）
  4. render()               → 后处理 + 上屏
      ├─ applyBloom()       → 发光（prefilter→blur×N→final）
      ├─ applySunrays()     → 体积光（mask→blur→composite）
      └─ drawDisplay()      → 上屏（含 shading 高光 + dithering 抖动）
```

**step(dt) 物理模拟管线（Stable Fluids + curl 增强）：**

| 顺序 | Pass | 作用 | 输入→输出 |
|------|------|------|-----------|
| 1 | curl | 计算速度场卷曲（局部旋转强度） | velocity → curl 场 |
| 2 | vorticity | 涡量约束：把旋度加回速度场，恢复被耗散的小涡 | velocity+curl → velocity |
| 3 | divergence | 计算散度（不可压缩偏差） | velocity → divergence 场 |
| 4 | pressure×20 | Jacobi 迭代求解压力泊松方程（投影第一步） | divergence+pressure → pressure |
| 5 | gradientSubtract | 减去压力梯度，强制速度场无散（不可压缩） | pressure+velocity → velocity |
| 6 | advection×2 | 速度场自平流；染料随速度场平流（半拉格朗日反向追踪） | velocity→velocity；velocity+dye→dye |

**关键机制：**
- **双缓冲 FBO（ping-pong）**：velocity/dye 各有 read/write 两个纹理，模拟 pass 写入 write、下一 pass 读 read，再 swap——避免读写冲突
- **半拉格朗日平流**（advection shader）：`coord = vUv - dt * velocity * texelSize`，从当前像素沿速度反向采样上一帧，天然稳定
- **耗散**：`result / (1.0 + dissipation * dt)`——VELOCITY_DISSIPATION 0.2（速度衰减慢）、DENSITY_DISSIPATION 1（染料消散快）
- **纹理分辨率分离**：速度场 128²（便宜），染料场 1024²（精细），渲染时双线性插值

## 三、核心 shader 提取（可直接复用的数学）

**平流（advection）**——半拉格朗日：
```glsl
vec2 coord = vUv - dt * texture2D(uVelocity, vUv).xy * texelSize;
gl_FragColor = texture2D(uSource, coord) / (1.0 + dissipation * dt);
```

**涡量约束（vorticity）**——让流体"活着"的关键：
```glsl
vec2 force = 0.5 * vec2(abs(T) - abs(B), abs(R) - abs(L)); // T/B/L/R 为四邻域卷曲
force /= length(force) + 0.0001;
force *= curl * C;              // curl 为强度参数(默认30)，C 为当前卷曲值
velocity += force * dt;
```

**散度（divergence）**：
```glsl
float div = 0.5 * (R - L + T - B);   // 速度场的邻居差分
```

**压力（pressure）**——Jacobi 迭代：
```glsl
// 20 次迭代收敛；pressure = (L+R+T+B - divergence) * 0.25
```

**投影（gradientSubtract）**：
```glsl
// velocity -= pressure 梯度 → 恢复无散度
```

## 四、设计理念（为什么流体动效显高级）

1. **有机不可预测**：curl 噪声注入（涡量约束）让流体永不重复、永不"死板"，这是与简单 CSS 动效的本质区别
2. **层级质感**：Shading（沿速度场扰动法线产生高光）+ Bloom（亮部发光）+ Sunrays（顶部体积光）三层叠加，营造"液体材质"感
3. **色彩即反馈**：鼠标路径即色彩，交互与视觉反馈合一（COLORFUL 模式下颜色随时间渐变）
4. **克制的性能预算**：128² 物理 + 1024² 显示 + 移动端自动降级，保证 60fps

## 五、可复用提示词（WebGL 流体加载动效）

> 用法：把下面提示词给 AI 前端代理，生成流体加载/背景动效

```text
请用 WebGL（优先 WebGL2，回退 WebGL1）实现一个流体动效，要求：

1. 基于 Stable Fluids 方法，GPU 上逐 pass 求解：curl → vorticity（涡量约束，CURL≈30）→ divergence → pressure（Jacobi 迭代 20 次）→ gradientSubtract → advection（半拉格朗日，速度场与染料场分开）
2. 双缓冲 FBO ping-pong 读写；速度场 128×128、染料场 512-1024（移动端自动降级）
3. 输入：鼠标/触摸拖动喷射速度与染料（splat），支持多指
4. 后处理：Bloom（threshold 0.6）+ 可选 Sunrays 体积光；染料耗散 1.0、速度耗散 0.2
5. 配色：暗底 + 高饱和流动色彩（HSV 随时间缓慢旋转）
6. 保持 60fps，WebGL 不可用时优雅降级为 CSS 渐变背景
```

## 六、参数调优表（config）

| 参数 | 默认 | 调优方向 |
|------|------|----------|
| SIM_RESOLUTION | 128 | 降低→更快更糊；提高→更精细更慢 |
| DYE_RESOLUTION | 1024 | 染料清晰度 |
| VELOCITY_DISSIPATION | 0.2 | 越小流速维持越久 |
| DENSITY_DISSIPATION | 1 | 越小染料消散越慢 |
| CURL | 30 | 越大旋涡越强（0=无旋涡） |
| PRESSURE_ITERATIONS | 20 | 越高越"刚体"，越低越"糊" |
| BLOOM / SUNRAYS | on/on | 关闭可省性能，质感下降 |

## 七、配套

- 在线 Demo：https://paveldogreat.github.io/WebGL-Fluid-Simulation/
- 同类拆解可参考：`libs\effects\gravy\`（引力透镜）、`black-hole\`（黑洞）、`threejs-shader\`（GLSL 特效合集，中文注释）
- 学习基础：`.prompt\前端\WebGL与three.js学习与动效资源-20260804\prompt.md`
