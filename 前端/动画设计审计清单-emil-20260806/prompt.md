# 动画设计审计清单（emilkowalski 方法论）

> 来源：emilkowalski/skills 提炼（animation-vocabulary + improve-animations/AUDIT.md），2026-08-06 沉淀
> 作者：Emil Kowalski（Vercel/Linear 背景，动画设计专家，https://emilkowal.ski）
> 完整 skill：`~/.deepcode/skills/improve-animations/`（含 AUDIT.md、PLAN-TEMPLATE.md）

## 适用场景

- 审查/改进项目动画："improve the animations"、"audit the motion"、"make this app feel better"
- 编写动画设计规范与提示词时引用具体数值（时长、缓动曲线）
- 动画评审（单 diff 用 review-animations，全库审计用本清单）

## 一、核心预算（写提示词时直接引用）

### 缓动曲线（作为 token 引入，内置 CSS 缓动太弱）

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);     /* 进入/退出：快速响应 */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1); /* 屏幕内移动/形变 */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);  /* iOS 风格抽屉 */
```

缓动决策顺序：进入/退出→ease-out；屏幕内移动→ease-in-out；hover/变色→ease；常速运动（跑马灯/进度）→linear；默认→ease-out。**UI 上的 ease-in 永远是问题**（起点慢，延迟用户正在看的瞬间）。

### 时长预算（UI 动画不超过 300ms）

| 元素 | 时长 |
|------|------|
| 按钮按压反馈 | 100–160ms |
| 提示框/小 popover | 125–200ms |
| 下拉/select | 150–250ms |
| 弹窗/抽屉 | 200–500ms |
| 营销/解说类 | 可更长 |

## 二、八类审计规则（评审清单）

### 1. 目的与频率
- 每个动画必须回答"为什么动"：空间一致性/状态指示/反馈/解释/防突兀。高频元素上"好看"不是目的
- **100+ 次/天**（快捷键、命令面板）：永不动画（Raycast 命令面板无动画——正确）
- 数十次/天（hover、列表导航）：移除或大幅减少
- 偶尔（弹窗/抽屉/toast）：标准动画
- 稀有/首次（引导/庆祝）：可加 delight
- 最有效的修复常常是**删掉动画**

### 2. 缓动与时长
- 见上文预算表；寻找：任何 ease-in、入场用裸 ease/linear、UI 元素时长 >300ms、工具栏每个 tooltip 都有延迟动画（第一个之后应瞬时）

### 3. 物理性与原点
- **永远不要 scale(0)**——现实世界没有东西凭空出现。目标：`scale(0.9–0.97)` + `opacity: 0`
- popover/下拉/tooltip 从**触发器**缩放（`transform-origin: var(--transform-origin)`）；**弹窗例外**（居中，transform-origin: center 正确，不要报告）
- 按压反馈：`:active` 时 `transform: scale(0.97)` + `transition: transform 160ms ease-out`（0.95–0.98 微妙即可）

### 4. 可中断性
- CSS transition 可中途改目标；**keyframes 从零重启**——快速触发/可逆的动画（toast 堆叠、toggle、拖拽、折叠）必须用 transition 或 spring
- 手势驱动用 spring（中断时携带速度）；Apple 风格 spring：`{ type: "spring", duration: 0.5, bounce: 0.2 }`，bounce 保持 0.1–0.3
- 非对称时序：蓄力（按压/保持/破坏性确认）慢，系统响应快；按-放对称是问题

### 5. 性能
- **只动 transform 和 opacity**；width/height/margin/padding/top/left 触发 layout+paint
- `transition: all` 永远算问题（把无关属性动画到非 GPU）
- Framer Motion 的 `x`/`y`/`scale` 简写**不走硬件加速**（主线程跑，高压下掉帧）——用完整 transform 字符串
- 不要用父元素 CSS 变量驱动子元素 transform（重算所有子样式）；直接设在元素上
- 预设运动用 CSS/WAAPI，动态/手势用 JS/spring；transition 期间的 `filter: blur()` 保持在 20px 内

### 6. 无障碍
- 减少动画 = **更少更温和**，不是零：保留有助于理解的过渡，移除位置变化
- `@media (prefers-reduced-motion: reduce)` 保留 opacity/color、去掉移动
- hover 动效要 `@media (hover: hover) and (pointer: fine)` 门控（触摸屏点按会误触发 hover）

### 7. 一致性（token）
- 动效要匹配产品性格（活泼可弹跳，仪表盘保持干脆）；跨组件性格不一致是问题
- 曲线和时长做成共享 token；5 个手写且几乎相同的 cubic-bezier 需要合并
- 群体入场应有 **30–80ms stagger**（装饰性，绝不能阻塞交互）
- 重叠状态的生硬 crossfade 可用过渡期 `filter: blur(2px)` 掩盖

### 8. 错失的机会（加法类）
- 状态突变（内容替换/布局跳变）应有短暂过渡防突兀
- 空间关联 UI（面板从触发器出现）应有解释来源的动效
- 稀有高情绪时刻（首次运行/成功/庆祝）值得动用 delight 预算
- 工具：`translate` 百分比（translateY(100%) = 自身高度，无硬编码像素）、`clip-path: inset()` 揭示

## 三、动画术语速查（animation-vocabulary 核心）

| 类别 | 术语 |
|------|------|
| 入场/退场 | Fade in/out、Slide in、Scale in、**Pop in**（轻微过冲）、Reveal（clip-path/mask 揭示） |
| 序列/时机 | Keyframes、Interpolation/Tween、**Stagger**（级联）、Orchestration、Fill mode |
| 变换 | Translate、Scale、Rotate、Skew、3D tilt/Flip、Perspective、**Transform origin**、Origin-aware（从触发器长出） |
| 状态过渡 | Crossfade、Continuity、**Morph**（形变，Dynamic Island）、Shared element transition（缩略图→卡片）、Layout animation、Accordion、Direction-aware |
| 滚动 | Scroll reveal、Scroll-driven、Parallax、Page transition、View transition |
| 反馈 | Hover、Press/Tap（scale 0.97）、Hold to confirm、Drag（带动量）、Swipe to dismiss、Rubber-banding（iOS 过拉回弹）、Shake/Wiggle、Ripple |
| 缓动 | Ease-out（默认，响应式）、Ease-in（避免）、Ease-in-out、Linear（仅 spinner/跑马灯） |

## 四、可复用提示词（动画审计）

> 用法：给 AI 前端代理，对项目动画做一次系统审计

```text
请作为资深动效设计工程师，对当前项目的动画/动效代码做一次只读审计（不改代码），输出按杠杆率（影响÷成本）排序的发现表。

1. Recon：识别技术栈（Framer Motion/GSAP/纯 CSS/WAAPI）、动效位置（CSS token、keyframe、transition/animate 属性）、现有缓动与时长约定、产品性格（活泼 vs 干脆）、高频元素地图
2. 按 8 类审计：目的与频率 / 缓动与时长 / 物理性与原点 / 可中断性 / 性能 / 无障碍 / 一致性token / 错失机会
3. 每条发现给出 file:line 证据与修复摘要；严重度：HIGH=破坏手感（UI 上 ease-in、高频动画、掉帧、scale(0)）、MEDIUM=明显不对（原点错误、不可中断、缺 reduced-motion）、LOW=打磨（stagger、blur crossfade、token 合并）
4. 预算标准：UI 动画 ≤300ms；按钮按压 100-160ms；入场 ease-out cubic-bezier(0.23,1,0.32,1)；永不 scale(0)，用 scale(0.9-0.97)+opacity 0；只动 transform/opacity；transition: all 一律报告；stagger 30-80ms
5. 最后列出 2-4 个"应该动但没动"的错失机会
```

## 五、配套

- 相关 skill：`~/.deepcode/skills/animation-vocabulary/`（术语反查）、`animate/`（动画实现）、`review-animations/`（单 diff 评审）、`find-animation-opportunities/`（找动效机会）
- 与 GSAP 提示词互补：`.prompt\前端\GSAP动画完整提示词-20260804\prompt.md`（实现层）、本清单（评审/规范层）
