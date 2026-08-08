# 宇宙胶囊 WebGL 动效拆解（画境观屿 · Cosmic Capsules）

> 2026-08-06 拆解沉淀。源码 demo：`D:\Code\AI资源管理\libs\capsules\nebula-capsules\`（MIT，12 组实时动效，~2400 行 JS+GLSL）
> 效果：三种渲染模式——Nebula 宇宙星云（NC-01~06）、Aurora 柔光流带（NC-07~09）、Progress 流体进度（NC-10~12）
> 在线运行：`npm start`（本地 127.0.0.1:4173，ES Modules 需经本地服务，勿直接双击 index.html）

## 一、效果概览与适用场景

| 模式 | 编号 | 渲染技术 | 适用场景 |
|------|------|----------|----------|
| Nebula | NC-01~06 | WebGL2 fragment shader（fbm 噪声 + domain warping + 星点） | Hero 背景、品牌主视觉、加载页 |
| Aurora | NC-07~09 | WebGL2 fragment shader（高斯光带 + 流动相位 + 软核心） | 卡片光效、产品卡片、CTA 强调 |
| Progress | NC-10~12 | WebGL2 + 运动轨迹纹理图集 + Canvas 2D 降级 | 品牌化进度条、AI 训练/迁移进度展示 |

技术要点：单 fragment shader 覆盖 Nebula + Aurora（`u_mode`/`u_profile` uniform 切换），全屏三角形而非 quad，DPR cap 1.75、IntersectionObserver 离屏停渲染、`prefers-reduced-motion` 自动暂停、WebGL2 不可用时 Canvas 2D 降级。

## 二、架构与渲染调度

```
index.html                      页面 shell + 筛选栏
src/main.js                     画廊调度：创建 capsule、共享 rAF、IntersectionObserver
src/presets.js                  NC-01~09 冻结预设（seed/speed/4 色/mode）
src/cosmic-shader.js            CosmicRenderer：Nebula + Aurora 共用 program
src/fallback.js                 Canvas 2D 降级（WebGL2 不可用时）
aurora.css                      NC-07~09 柔光主题覆盖
src/progress-*.js               NC-10~12 独立模块（不侵入原九组）
progress.css                    454×104px 固定窄幅布局
```

**冻结边界原则**（项目核心工程约束）：`NC-01~09` 与 `NC-10~12` 模块完全解耦——进度模块通过 `progress-entry.js` 在原九组挂载后接入，`main.js/presets.js/cosmic-shader.js/fallback.js/aurora.css` 不因进度更新而改动。`progress-tests.mjs` 自动验证这条边界不被破坏。

## 三、Nebula 渲染拆解（NC-01~06）

### Shader 管线（单 fragment shader，main 函数顺序）

```
1. 坐标修正：uv → p = uv-0.5，p.x 按宽高比拉伸（保持各向同性）
2. 指针涡旋场：exp(-dist*4.6) 衰减 → 旋转矩阵 swirl → 沿 delta 方向位移
3. 域扭曲（domain warping，IQ 经典）：
     drift = vec2(t*0.22, -t*0.13)            // 时间漂移
     q = vec2(fbm(p*1.35 + drift), fbm(p*1.35 + offset - drift*0.85))
     r = vec2(fbm(p*2.0 + 3.6*q + offset), fbm(p*2.0 + 3.0*q + offset))
     cloud = fbm(p*1.7 + 4.2*r)
     veins = fbm(p*4.0 - 2.0*q + t*0.065)
     nebula = smoothstep(0.18, 0.91, cloud*0.9 + veins*0.22)
4. 4 色调色板：palette(nebula) —— shadow→body→highlight 三段 smoothstep 混合
5. 星点网格：floor(uv * vec2(132,58)) cell，step(0.989, random) 稀疏化（仅 ~1% cell 出现星）
     twinkle = 0.35 + 0.65 * sin(t*(1+random*2.4) + random*40) * 0.5 + 0.5
6. 指针辉光：exp(-dist*7.0) 累加 colorD
7. 暗角 + gamma：vignette smoothstep(0.94,0.18,...) + pow(color, 0.88)
```

### 核心 fbm（值噪声 6 octaves，每层旋转 + 倍频）

```glsl
float noise(vec2 p) {                    // 值噪声：四角 hash 双线性插值
  vec2 i = floor(p), f = fract(p);
  f = f * f * (3.0 - 2.0 * f);            // Hermite 平滑（消除网格纹）
  float a = hash21(i), b = hash21(i+vec2(1,0)), c = hash21(i+vec2(0,1)), d = hash21(i+vec2(1,1));
  return mix(mix(a,b,f.x), mix(c,d,f.x), f.y);
}
float fbm(vec2 p) {
  float value = 0.0, amplitude = 0.52;
  mat2 rotation = mat2(0.80, 0.60, -0.60, 0.80);  // ~37° 旋转，减少轴向伪影
  for (int i = 0; i < 6; i++) {
    value += amplitude * noise(p);
    p = rotation * p * 2.03 + 17.7;                // 倍频 + 域偏移
    amplitude *= 0.5;
  }
  return value;
}
```

### 4 色调色板（shadow/body/highlight 三段）

```glsl
vec3 palette(float t) {
  t = clamp(t, 0.0, 1.0);
  vec3 shadow    = mix(u_colorA, u_colorB, smoothstep(0.06, 0.62, t));
  vec3 body      = mix(u_colorB, u_colorC, smoothstep(0.30, 0.82, t));
  vec3 highlight = mix(u_colorC, u_colorD, smoothstep(0.74, 1.0, t));
  vec3 restrained = mix(shadow, body, smoothstep(0.26, 0.72, t));
  return mix(restrained, highlight, smoothstep(0.78, 0.97, t));
}
```

> 设计要点：每段 smoothstep 的 [start,end] 区间有意重叠（如 body 0.30~0.82 与 shadow 0.06~0.62 在 0.30~0.62 重叠），制造柔和过渡而非硬带。

### 指针涡旋（局部旋转 + 径向位移）

```glsl
float influence = exp(-distanceToPointer * 4.6) * u_motion;  // 衰减场，motion 为交互强度
float angle = influence * 1.7;
mat2 swirl = mat2(cos(angle), -sin(angle), sin(angle), cos(angle));
p = pointer + swirl * delta;                                  // 旋转
p += normalize(delta + 0.0001) * influence * 0.08;            // 径向外推
```

## 四、Aurora 渲染拆解（NC-07~09）

同一 fragment shader 内由 `u_mode=1` + `u_profile∈{1,2,3}` 切换三种子样式。无 domain warping，改用「高斯光带 + 流动相位 + 软核心」。

### Polar（NC-07，深底暖极光）

```glsl
// 四条高斯光带，center 随相位 + uv.x 摆动（产生横向流动感）
float phase = t * 1.08 + u_seed * 0.063;
float grain = fbm(...) - 0.5;                                  // fbm 颗粒扰动 center
float orangeCenter  = 0.76 - uv.x*0.20 + sin(phase + uv.x*3.7)*0.14  + grain*0.16;
float magentaCenter = 0.37 + uv.x*0.13 + sin(phase*0.84 + uv.x*4.7 + 1.1)*0.16 - grain*0.14;
float orangeBand  = gaussian(uv.y, orangeCenter, 0.074);       // 越小越细
// 白色脉冲核心（椭圆 exp 衰减 + sin 脉冲）
float whiteCore = exp(-length((uv-corePos) * vec2(2.05, 0.94)) * 6.1);
color += u_colorD * whiteCore * (0.72 + sin(phase*1.62)*0.28) * 1.30;
```

### 高斯光带通用公式

```glsl
float gaussian(float v, float center, float width) {
  return exp(-pow(v - center, 2.0) / max(width, 0.0001));   // width 越小带越细
}
```

> 三种 profile 共同手法：① `rightField = smoothstep(0.06, 0.96, uv.x)` 让光带从左到右渐显 ② 光带 center = 基准 + sin(相位) 摆动 + fbm 颗粒扰动 ③ 白色软核心用椭圆 exp 衰减 + sin 脉冲呼吸 ④ `pointerBend = exp(-dist*6.4..6.8)` 实现指针局部弯曲。

### 三个 profile 差异速查

| profile | 速度 | 底色 | 光带数 | 特色 |
|---------|------|------|--------|------|
| Polar (NC-07) | t×1.08 | 深色 #202126 | 橙/洋红/暖白/扫掠 4 带 | 白色脉冲核心 + sweepBand |
| Dubdot (NC-08) | t×0.86 | 白色 #FFFFFF | 上/下/中 3 带 + softBody | 右侧大椭圆软体 |
| Vercel (NC-09) | t×1.62 | 白色 #FFFFFF | 薄荷/金/粉 3 带 + 3 独立 core | separation 分离线（白化） |

## 五、Progress 流体进度拆解（NC-10~12）

固定窄幅 `454×104px`，桌面不拉伸、小屏自适应缩小。核心是「运动轨迹纹理图集」驱动边界位移，非实时物理模拟（与 WebGL流体模拟动效拆解 的 Stable Fluids 路线不同，这里走「预烘焙轨迹 + 纹理采样」更轻量）。

| 子模块 | 职责 |
|--------|------|
| `progress-presets.js` | NC-10~12 编号、4 色、初始值（43/33/58）、loadRate（1.10/1.00/1.05 %/秒） |
| `progress-motion-data.js` | 240×80 平滑边界轨迹生成（`PROGRESS_MOTION_WIDTH/HEIGHT/DURATION/MAX_PX`） |
| `progress-reference-atlases.js` | 运行时 24 帧纹理图集 |
| `progress-flow-renderer.js` | WebGL2 流体 shader（fbm + 运动纹理采样 + 高斯带 + 边界位移） |
| `progress-flow-overlays.js` | WebGL 叠层 / Canvas 2D 降级切换 |
| `progress-capsules.js` | 组件壳：拖动、键盘（←→ 2% / PgUpDn 10% / HomeEnd 0/100%）、单向进度逻辑 |
| `progress-entry.js` | 等待原九组挂载后接入，保证冻结边界 |

**进度交互规则**（产品级细节，值得复刻）：
- 自动进度仅正向、线性、匀速，不回退、不随机跳值；到 100% 保持不重置
- 手动调整后等待 ~1.8 秒，再从当前位置继续向右
- "随机切换"只改流体纹理时相，不改百分比
- 拖动 / 触摸 / 键盘三路输入统一

## 六、可复用提示词（WebGL 星云 / 柔光带 / 品牌进度条）

> 三段独立提示词，分别对应三种模式，可单独喂给 AI 前端代理

```text
【星云背景·Nebula】请用 WebGL2 fragment shader 实现宇宙星云动效：
1. 全屏三角形（vertices: -1,-1, 3,-1, -1,3），单 shader 内 u_mode 切换星云/极光
2. 星云分支：6 octaves 值噪声 fbm（每层 37° 旋转矩阵 + 2.03 倍频 + 0.5 振幅衰减）
3. 域扭曲：q=fbm(p+drift), r=fbm(p+3.6*q), cloud=fbm(p+4.2*r)，drift 随时间漂移
4. 4 色调色板：shadow→body→highlight 三段 smoothstep（区间有意重叠 0.06~0.97）
5. 星点：132×58 cell 网格，step(0.989, hash) 仅 ~1% 出现，sin twinkle 闪烁
6. 指针涡旋：exp(-dist*4.6) 衰减旋转 + 径向位移 0.08；DPR cap 1.75，离屏停渲染
7. 收尾：暗角 smoothstep(0.94,0.18) + gamma pow(0.88)

【柔光流带·Aurora】请用 WebGL2 fragment shader 实现柔光极光带：
1. 高斯光带 gaussian(uv.y, center, width)：center = 基准 + sin(phase + uv.x*k)*amp + fbm*grain
2. rightField = smoothstep(0.06,0.96,uv.x) 让光带从左渐显
3. 白色脉冲核心：椭圆 exp(-length((uv-pos)*aspect)*k) × (0.72+sin(phase)*0.28)
4. 指针弯曲 exp(-dist*6.4~6.8)；三种子样式由 u_profile 切换
5. 配色示例：Polar 暖（橙/洋红/暖白）、Dubdot 冷（浅蓝/天蓝/青蓝）、Vercel 柔（薄荷/淡黄/浅粉）

【品牌进度条·Progress】请实现 WebGL2 流体进度条（454×104px 固定窄幅）：
1. 预烘焙运动轨迹（240×80 边界位移数据）+ 24 帧运行时纹理图集，非实时物理（更轻量）
2. shader 内 fbm + 运动纹理采样 motionSample(y,t) + 高斯带 + 边界位移 edgeDisplacement
3. 自动进度：正向线性匀速 1.0~1.1%/秒，到 100% 保持不重置，不回退不跳值
4. 交互：拖动/触摸/键盘（←→ 2%, PgUpDn 10%, Home/End 0/100%）；手动后等 1.8s 继续
5. "随机切换"只换流体纹理时相，不改百分比
6. WebGL2 不可用时 Canvas 2D 降级；prefers-reduced-motion 暂停
```

## 七、预设参数表（NC-01~09）

| 编号 | 名称 | seed | speed | 配色（4 色 A/B/C/D） | 分组 |
|------|------|------|-------|----------------------|------|
| NC-01 | ORIGINAL | 1.7 | 0.50 | #FFF3EA / #F5B27A / #F67BC6 / #A978E8 | 暖 |
| NC-02 | OCEAN | 8.2 | 0.48 | #EAF6FF / #8FD0FF / #3B87F6 / #6B58E9 | 冷 |
| NC-03 | KLEIN | 14.1 | 0.49 | #EDF2FF / #2F58D5 / #1B2040 / #E07A43 | 冷 |
| NC-04 | ULTRAVIOLET | 23.4 | 0.47 | #F2EEFF / #B99AF1 / #8F74DB / #D7D85C | 冷 |
| NC-05 | CHROME | 37.8 | 0.42 | #F5F6F8 / #B9C0CC / #7F8793 / #4A4F59 | 冷 |
| NC-06 | PLUS | 51.3 | 0.50 | #FFF0E6 / #F6C26B / #F98A64 / #E86D74 | 暖 |
| NC-07 | POLAR | 67.4 | 0.34 | #202126 / #FF7A1A / #FF22D3 / #FFF7A3 | 暖(极光) |
| NC-08 | DUBDOT | 78.6 | 0.30 | #FFFFFF / #DDEEFF / #A7DBFF / #27B8F3 | 冷(极光) |
| NC-09 | VERCEL | 89.9 | 0.36 | #FFFFFF / #BCEFEA / #FFD76A / #FF8BB6 | 暖(极光) |

> Aurora 速度普遍低于 Nebula（0.30~0.36 vs 0.42~0.50），因光带流动视觉更明显，需更慢才不刺眼。

## 八、设计理念（为什么这套动效显高级）

1. **域扭曲而非裸噪声**：直接 fbm 出来是"棉絮感"，经 q→r→cloud 三层 domain warping 后才成"流体星云"——这是 IQ 的招牌手法，与简单 CSS 噪声背景的本质差距
2. **区间重叠的调色板**：shadow/body/highlight 三段 smoothstep 的 [start,end] 故意交叉重叠，避免色彩断层；4 色（A 暗 / B 主 / C 亮 / D 高光）梯度明确
3. **克制的星点密度**：step(0.989, random) 意味着仅 ~1.1% cell 出星，配合 twinkle 形成"稀疏闪烁"而非"密集噪点"
4. **指针交互的物理感**：exp 衰减旋转 + 径向位移，让指针周围"搅动"星云；motion 用 0.07 lerp 平滑过渡，避免突变
5. **冻结边界工程**：NC-01~09 与 NC-10~12 模块完全解耦，进度模块以增量方式接入——大型动效项目可借鉴的演进策略
6. **优雅降级链**：WebGL2 → Canvas 2D（fallback.js）→ prefers-reduced-motion 暂停，覆盖全部环境

## 九、配套

- 可运行 demo：`D:\Code\AI资源管理\libs\capsules\nebula-capsules\`（`npm start` → http://127.0.0.1:4173）
- 关联沉淀：
  - `.prompt\前端\WebGL流体模拟动效拆解-20260804\prompt.md`（Stable Fluids 物理路线，与本文「纹理图集」路线互补）
  - `.prompt\前端\WebGL与three.js学习与动效资源-20260804\prompt.md`（shader 学习资源）
  - `.prompt\前端\动画设计审计清单-emil-20260806\prompt.md`（动效预算与审计）
- 关键源码：`src/cosmic-shader.js`（Nebula+Aurora，412 行）、`src/progress-flow-renderer.js`（Progress，405 行）、`src/presets.js`（预设）、`docs/ARCHITECTURE.md`（架构）
