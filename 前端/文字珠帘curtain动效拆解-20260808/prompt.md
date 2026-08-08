# 文字珠帘（Curtain）动效拆解——天坛定制版

> 2026-08-08 拆解沉淀。来源：飞书文档「文字 curtain 效果」；源码 demo：`D:\Code\AI资源管理\libs\curtain\temple-curtain.html`（单文件 1072 行，引用 `twg.png` 背景图，同目录）
> 效果：字符按古代竖排（右起第一列）悬挂成珠帘，verlet 绳子物理——鼠标划过帘子被拨动回摆，敲击链串发出按列定音高的金属音
> 运行：`temple-curtain.html` 与 `twg.png` 放同一目录，浏览器直接打开（纯静态，无依赖）

## 一、效果概览与适用场景

| 维度 | 说明 |
|------|------|
| 视觉 | 文字珠帘垂挂于背景建筑图上，鼠标拨动时整帘物理摆动，帘面有半透明缎带质感 + 锚钉 + 阴影 |
| 听觉 | 拨动帘串触发 Web Audio 合成音（十音音阶按列定音高 + 立体声定位 + 延迟/反馈混响） |
| 交互 | 鼠标拖扫拨帘（可调强度/影响半径/惯性）；右上角可自定义文字与背景图 |
| 适用 | 品牌主页 hero、节气/诗词/古风主题页、文字展示型落地页、交互装饰性背景 |

技术路线：**Canvas 2D + verlet 积分绳子物理 + Web Audio 合成音**。与 WebGL 流体/粒子路线（fragment shader）不同，本作是「CPU 轻量物理 + 每帧 fillText」——无 shader、无外部库、单文件可运行，移动端友好。

## 二、架构与数据模型

```
temple-curtain.html（单文件）
├── CSS    纸张质感背景（repeating-gradient 斜纹 + 径向光 + 点阵噪点混合）
├── HTML   背景图 <img id=temple> + <canvas id=curtain> + 设置面板 + 滑杆
└── JS     物理引擎 + 布局 + 渲染 + 音效 + 自定义输入
```

核心数据结构：**chains[] = 若干列，每列一条绳子链**：

```js
chain[i] = {
  x, y, oldX, oldY,      // verlet 位置（old = 上一帧位置，隐含速度）
  anchorX, anchorY,      // 悬挂锚点（第一点 pinned，其余跟随）
  pinned,                // row 0 钉在顶部
  restLength,            // 链段等距长（segmentLength）
  char,                  // 该点显示的字符（空串 = 无字，仍参与物理）
  alpha: 0.8
}
```

关键点：**每个字符点 = 一个物理质点**，字符渲染只是该点的视觉外衣；链段等距保证珠帘均匀下垂。

## 三、核心机制拆解

### 3.1 布局：列数反推 + 古代竖排次序

```js
// 列数 = 按「每列最小高度能容纳的字数」反推，而非固定密度阈值
const rowCapacity = Math.max(1, absoluteMinRows - 1);   // 每列字容量
let columns = clamp(Math.ceil(source.length / rowCapacity), minColumns, maxColumns);
// 珠帘横跨屋顶宽度 84%，列均匀分布（字少列少时自动拉开间距）
const x = left + (column * curtainWidth) / (columns - 1);
// 古代书写习惯：第一列在最右（右起竖排）
const readingColumn = columns - 1 - column;
const globalIndex = readingColumn * textRowsCount + textRowIndex;  // 列优先填充
```

设计要点：
- **列数反推而非密度判断**——文字再短也不会出现大量空列，帘形始终饱满
- 列数 2~26（窄屏 <720px 上限 16）、字号窄屏 9.5px / 正常 10.5px、行距 fontSpacingFactor=17
- `readingColumn = columns-1-column` 让滕王阁序按古书右起阅读

### 3.2 物理：verlet 积分 + 距离约束迭代

```js
// 一、积分（速度 = 当前位置 - 旧位置）
function integrate() {
  for (const point of chain) {
    if (point.pinned) continue;
    const vx = (point.x - point.oldX) * physics.friction;   // 摩擦 0.95
    const vy = (point.y - point.oldY) * physics.friction;
    point.oldX = point.x; point.oldY = point.y;
    point.x += vx; point.y += vy + physics.gravity;         // 重力 0.18
  }
}

// 二、约束（6 次迭代距离修正，经典 rope）
function constrain() {
  for (let pass = 0; pass < 6; pass++) {
    const anchor = chain[0]; anchor.x = anchorX; anchor.y = anchorY;  // 锚点钉死
    for (let i = 1; i < chain.length; i++) {
      const dx = b.x - a.x, dy = b.y - a.y;
      const dist = Math.hypot(dx, dy);
      const diff = (dist - b.restLength) / dist;   // 距离误差比例
      // 首点 pinned → 只推 b；否则 a/b 各 50% 分摊
      b.x -= dx * diff; b.y -= dy * diff;
    }
  }
}
```

要点：
- **verlet 积分天然稳定**——速度由位置差隐式表达，无需显式 velocity 数组
- 6 次约束迭代足够让帘子"硬"而不抖；锚点每次迭代强制回位
- 这是"绳子/链/布"通用物理模板，换 `restLength` 与迭代次数即可调软硬

### 3.3 鼠标交互：位移冲击 + 线性衰减

```js
function injectMouseDelta() {
  const moveX = mouse.x - mouse.oldX, moveY = mouse.y - mouse.oldY;
  const speed = Math.hypot(moveX, moveY);
  if (speed < 0.01 || speed > 80) return;          // 抖动/瞬移过滤
  for (const chain of chains)
    for (let i = 1; i < chain.length; i++) {
      const dist = Math.hypot(point.x - mouse.oldX, point.y - mouse.oldY);
      if (dist >= physics.radius) continue;        // 半径 34px
      const falloff = 1 - dist / physics.radius;   // 线性衰减
      strongestImpact = Math.max(strongestImpact, speed * falloff);
      point.x += moveX * physics.strength * falloff;   // 强度 0.82
      point.y += moveY * physics.strength * falloff;
    }
  if (strongestImpact > 0) strikeChain(chainIndex, strongestImpact, chain[0].x);
}
```

要点：
- **注入位移而非力**——直接叠加在位置上的冲击，verlet 里效果最直观
- 基于**鼠标帧间位移量**（非位置），拖动越快冲击越强
- falloff 线性衰减形成"近重远轻"的拨动手感；impact 同时驱动音效音量

### 3.4 音效：合成金属音（3 分音 + 列定音高 + 立体声）

```js
const scale = [523.25, 587.33, 659.25, 783.99, 880, 1046.5, 1174.66, 1318.51, 1567.98, 1760]; // C5~A6
const frequency = sound.scale[columnIndex % sound.scale.length];  // 列号 → 音高
// 3 个泛音分音（1x / 2.01x / 3.96x）sine 振荡器 + 指数衰减包络 → 金属质感
[{ratio:1,amount:1,decay:1},{ratio:2.01,amount:0.24,decay:0.62},{ratio:3.96,amount:0.1,decay:0.38}]
  .forEach(p => { osc.frequency = frequency * p.ratio; env.gain.exponentialRampToValueAtTime(0.0001, now + duration*p.decay); });
// 立体声定位：按列 x 位置 pan -0.9~+0.9
const pan = clamp((x / width) * 2 - 1, -0.9, 0.9);  // StereoPanner
// 防爆音节流：同列 95ms、全局 28ms、最多 8 并发 voices
// 混响链：output(gain 0.62) → compressor(-18dB, 3:1) → delay(0.11s)+feedback(0.14)+wet(0.13) → destination
```

要点：
- **列号映射音高**——从左到右扫帘 = 弹奏音阶上行/下行，交互即乐器
- 分音合成替代采样——零音频资源，泛音比例决定"金属 vs 木鱼"质感
- 三节流防爆音：同列限频、全局限频、并发上限

### 3.5 渲染：缎带帘面 + 锚钉 + 字符

```js
// 每列左右两侧由法线偏移生成缎带（帘布质感）
const nx = -dy / dist, ny = dx / dist;
p.lx = x + nx * widthParam; p.ly = y + ny * widthParam;    // 左缘
p.rx = x - nx * widthParam; p.ry = y - ny * widthParam;    // 右缘
// 4 种半透明棕色调（RIBBON_COLORS）按列分组填充 → 布帘层次
// 阴影：shadowColor rgba(53,39,24,0.08) blur 3 offset (1.2, 2) → 帘影立体感
// 锚钉：金色小圆点（rgba(156,108,46,0.78) r=1.8）
// 字符：ctx.fillText(point.char, x, y)，深棕 #2e251f，Songti SC/SimSun
```

缎带宽度自适应：`clamp((width*0.84/columnsCount)*0.34, 4.5, 6.5)`——列多时帘带收窄。

### 3.6 自定义与参数

| 控件 | 作用 | 底层 |
|------|------|------|
| textarea | 自定义文字（去空白，空则回默认滕王阁序） | `glyphs → build()` 重建链 |
| 背景图 file | 自定义背景图 | FileReader → dataURL → img src |
| strength 滑杆 | 拨动强度 | `physics.strength`（默认 0.82） |
| reach 滑杆 | 影响半径 | `physics.radius`（默认 34） |
| inertia 滑杆 | 惯性/摩擦 | `physics.friction`（默认 0.95） |
| Reset curtain | 重排链 | `build()` |
| Reset image & text | 恢复默认 | 还原 img src + glyphs |

## 四、可复用提示词

### 4.1 完整效果复刻（通用）

```text
用 Canvas 2D 实现一个"文字珠帘"交互效果，单 HTML 文件：
1. 布局：把指定文字按列竖排（右起第一列，古代书写顺序），每列 = 一条 verlet 绳子链；
   列数按"每列最小高度可容纳字数"反推（避免短文字出现大量空列），列间等距横跨画布 84% 宽度。
2. 物理：verlet 积分（隐式速度 = 当前位置 - 旧位置，乘摩擦 0.95）+ 重力 0.18；
   每帧 6 次距离约束迭代（首点钉死为悬挂锚点，其余点 50/50 分摊修正），链段等距。
3. 交互：鼠标帧间位移量作为冲击，注入半径 34px 内的质点（线性衰减 falloff = 1 - d/r，
   位移 × 强度 0.82 × falloff）；过滤抖动（speed<0.01）与瞬移（speed>80）。
4. 音效：Web Audio 合成金属音——每列按列号取十音音阶（C5~A6）定音高，3 个泛音分音
   （1x/2.01x/3.96x）sine + 指数衰减包络；StereoPanner 按 x 位置 -0.9~0.9 立体声；
   节流：同列 95ms / 全局 28ms / 并发 ≤8。
5. 渲染：每列按法线偏移左右缘生成半透明缎带（4 色调色板分组填充 + 阴影 blur3），
   顶部画金色锚钉小圆点，字符 fillText 深棕色。
6. 响应式：窄屏（<720px）列数上限 16、字号 9.5px；正常 26 列、10.5px；DPR cap 2。
7. 自定义：文字 textarea + 背景图 file（FileReader→dataURL）+ 强度/半径/惯性三个滑杆。
```

### 4.2 绳子物理最小模板（无音效版）

```text
实现 verlet 绳子：质点数组 {x, y, oldX, oldY}，每帧
1) integrate：vx=(x-oldX)*friction, vy=(y-oldY)*friction, oldX=x, oldY=y, x+=vx, y+=vy+gravity
2) constrain ×N：对每对相邻质点做距离修正 (dist-restLength)/dist，锚点强制回位
3) 渲染：连线或沿法线画缎带
参数：friction 0.9~0.99（惯性）、gravity 0.1~0.3、迭代 3~8（越大越硬）、restLength 均匀=绳节距
```

### 4.3 合成音效模板（金属敲击）

```text
Web Audio 合成敲击音：AudioContext → 3 个 sine 振荡器（频率 f, 2.01f, 3.96f，detune ±4 随机），
各自连接 gain 包络（初始 level×amount，exponentialRamp 到 0.0001，时长 duration×decay），
统一接 StereoPanner（pan -0.9~0.9）→ 主 gain(0.62) → DynamicsCompressor(-18dB, 3:1) → destination。
可选混响：DelayNode(0.11s) + feedback gain(0.14) + wet(0.13) 并联进 compressor。
泛音比例（1 / 0.24 / 0.1）决定音色：比例高 = 金属脆响，低 = 木鱼钝音。
```

## 五、设计理念与调参指南

- **物理即乐器**：列号 → 音高映射让"拨帘"变成"弹奏"，交互从被动浏览升级为主动演奏——体验设计的核心杠杆
- **字与帘合一**：字符点是物理质点，文字"长在"帘子上而非贴在背景上——内容与动效融合的范例
- **缎带分层**：法线偏移画布帘 + 4 色调色板分组，避免"只见文字不见帘"的单薄感；阴影 blur 3 制造布帘厚度
- **防呆细节**：速度过滤（<0.01 抖动 / >80 瞬移）、音效三节流、`prefers-reduced-motion` 可加（本 demo 未内置）
- **调参表**：

| 参数 | 位置 | 效果 |
|------|------|------|
| gravity | 0.18 | ↑垂坠感强 / ↓轻盈 |
| friction | 0.95 | ↑惯性大回摆久 / ↓快速静止 |
| strength | 0.82 | ↑拨动猛烈 / ↓轻柔 |
| radius | 34 | ↑影响范围大 / ↓精准 |
| constrain 迭代 | 6 | ↑帘子更硬挺 / ↓更柔软飘 |
| widthParam | 4.5~6.5 | 缎带宽度（列多自动收窄） |
| scale 数组 | 十音 | 换五声音阶/自定义旋律 = 不同"乐器" |

## 六、参考资源

- 运行 demo：`libs\curtain\temple-curtain.html` + `twg.png`（天坛背景 1501×818）
- 物理参考：verlet integration / 距离约束（绳子、布、链通用）
- 音效参考：Web Audio API 振荡器合成 + 分音泛音（additive synthesis 简化版）
