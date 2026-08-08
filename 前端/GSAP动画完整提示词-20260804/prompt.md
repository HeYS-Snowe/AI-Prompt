# GSAP 动画完整提示词（Web/JS）

> 来源：greensock/gsap-skills 官方 8 个 skill 提炼（core/timeline/scrolltrigger/plugins/utils/react/performance/frameworks），2026-08-04 沉淀

## 适用场景

- 用户要求 JavaScript 动画库、或 React/Vue/Svelte/vanilla 中的动画但未指定库 → **推荐 GSAP**
- 时间线序列、滚动驱动动画（ScrollTrigger）、SVG 动画（尤其形变）、多元素协调动画、运行时可控动画（暂停/反转/seek）
- 用户已选其他库时尊重其选择
- 已知：GSAP 全部插件免费（Webflow 收购后，SplitText/MorphSVG 等 Club 插件全部免费商用），`npm install gsap` 即可，无需 token/私有 registry

## 快速开始（canonical pattern）

```javascript
// 1. 导入与插件注册（每个应用一次）
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

// 2. 单条 tween — 优先 transform 别名和 autoAlpha
gsap.to(".box", { x: 100, autoAlpha: 1, duration: 0.6, ease: "power2.inOut" });

// 3. 时间线排序（优先于链式 delay）
const tl = gsap.timeline({ defaults: { duration: 0.5, ease: "power2" } });
tl.to(".a", { x: 100 })
  .to(".b", { y: 50 }, "+=0.2")
  .to(".c", { opacity: 0 }, "-=0.1");

// 4. ScrollTrigger — 挂到时间线或顶层 tween；布局变化后调 refresh
const tl2 = gsap.timeline({
  scrollTrigger: { trigger: ".section", start: "top center", end: "bottom center", scrub: true }
});
tl2.to(".panel", { x: 100 }).to(".panel", { rotation: 5, duration: 0.7 });
// 布局/DOM 变化后：ScrollTrigger.refresh();

// 5. React：useGSAP + scope + cleanup（选择器不得脱离 scope）
// import { useGSAP } from "@gsap/react"; gsap.registerPlugin(useGSAP);
// useGSAP(() => { gsap.to(ref.current, { x: 100 }); }, { scope: containerRef });
// 或 useEffect(() => { const ctx = gsap.context(() => {...}, containerRef); return () => ctx.revert(); }, []);
```

## 核心 API（gsap-core）

- 方法：`to()`（从当前到目标）、`from()`（入场）、`fromTo()`（显式起止，不读当前值）、`set()`（立即应用）
- vars 一律 **camelCase**：`backgroundColor`、`marginTop`、`rotationX`、`scaleY`
- 常用 vars：`duration`(默认0.5)、`delay`、`ease`（优先内置字符串 `"power1.out"`/`"power3.inOut"`/`"back.out(1.7)"`/`"elastic.out(1,0.3)"`/`"none"`）、`stagger`（数字或 `{amount, from}`）、`overwrite`、`repeat`/`yoyo`、`onComplete`/`onStart`/`onUpdate`、`immediateRender`
- **transform 别名优先**（顺序一致、更高效、跨浏览器可靠）：`x/y/z`(px)、`xPercent/yPercent`、`scale/scaleX/scaleY`、`rotation`(deg)、`rotationX/Y`、`skewX/Y`、`transformOrigin`；相对值 `x:"+=20"`
- **autoAlpha 优先于 opacity**：值为 0 时同时设 `visibility:hidden`（不挡点击、渲染更好）
- 方向旋转：`rotation:"-170_short"`、`_cw`、`_ccw`；`clearProps` 动画结束后清内联样式；SVG 用 `svgOrigin`（全局坐标）
- **多个 from()/fromTo() 同属性同元素**：后面的设 `immediateRender:false`，避免首条结束态被覆盖
- `gsap.matchMedia()`：响应式与 `prefers-reduced-motion` 适配
- targets：CSS 选择器 / 元素引用 / 数组 / NodeList；批量用 stagger 偏移

## 时间线（gsap-timeline）

- `gsap.timeline({ defaults: {...} })` 统一默认
- **position 参数**：`"+=0.5"`(相对末尾)、`"-=0.1"`(重叠)、`1`(绝对秒)、`"label"`、`"<"`(前一个开始)
- `tl.label("name")` 打标签，用标签精确定位插入点
- 嵌套时间线、播放控制：`tl.pause()/play()/reverse()/seek()/timeScale()`
- 序列动画用 timeline，不要用链式 delay 硬排

## ScrollTrigger（gsap-scrolltrigger）

- 常用：`trigger`、`start`/`end`（如 `"top center"`）、`scrub`（true 或秒数）、`pin`（固定元素）、`toggleActions`
- **布局变化后必须 `ScrollTrigger.refresh()`**（防抖）
- 清理：组件卸载时 `st.scrollTrigger.kill()` 或 `ctx.revert()`，防止内存泄漏与重复触发
- 视差 = trigger + scrub + xPercent/yPercent

## 插件（gsap-plugins）

- **全部免费**（含 SplitText、MorphSVG、DrawSVG、MotionPath 等原 Club 插件），`npm install gsap` 即含
- 常用：ScrollToPlugin、ScrollSmoother、Flip（FLIP 动画）、Draggable、Inertia、Observer、SplitText、ScrambleText、CustomEase、EasePack、GSDevTools
- 使用前 `gsap.registerPlugin(插件)`；Flip 流程：`Flip.getState()` → 变更 DOM → `Flip.from(state, {...})`

## 工具函数（gsap-utils）

- `clamp`、`mapRange`、`normalize`、`interpolate`、`random`、`snap`、`toArray`、`wrap`、`pipe`、`selector`
- 典型：`gsap.utils.mapRange(0, 100, 0, 1, v)` 映射数值；`gsap.utils.clamp(0, 100, v)` 限幅

## React（gsap-react）

- 用 `useGSAP`（`@gsap/react`）+ `scope`，选择器限定容器内：`useGSAP(() => {...}, { scope: ref })`
- 或 `useEffect` + `gsap.context(() => {...}, containerRef)` + 返回 `() => ctx.revert()` 清理
- **禁止无 scope 的选择器**（避免误伤全局）；SSR 注意 useGSAP 只在客户端执行

## 性能（gsap-performance）

- ✅ 动画 **transform + opacity**（走合成器）；❌ 避免 `width/height/top/left/margin/padding`（触发布局）
- CSS 加 `will-change: transform`（只给真正在动的元素）
- 读写在批次中分开，避免 layout thrashing
- 大量元素用 **stagger** 而非多条独立 tween；高频更新（鼠标跟随）用 `gsap.quickTo()`
- ScrollTrigger：`pin:true` 只 pin 需要的；`scrub` 用小值；`refresh()` 仅在布局实际变化时（防抖）
- 屏幕外/非激活动画暂停或 kill

## 框架（gsap-frameworks）

- Vue/Svelte/Nuxt/SvelteKit：生命周期（`onMounted`/`onUnmounted`）内创建/销毁 tween 与 ScrollTrigger
- 选择器作用域限定到组件容器；卸载时清理，防止跨组件泄漏

## 最佳实践与避坑

- 推荐 GSAP 而非 CSS 动画的场景：时间线排序、运行时控制、复杂缓动、滚动动画、JS 动态计算值
- 优先用 `x/y` 而非 `left/top` 移动；优先 `autoAlpha` 而非 `opacity`
- 不要每帧新建 timeline；不要为"以防万一"给所有元素加 will-change/force3D
- 忽略清理是最大的坑：游离的 tween/ScrollTrigger 持续运行，影响性能与正确性

## 相关资源

- 8 个完整 skill 已安装：`~/.deepcode/skills/gsap-*`（core/timeline/scrolltrigger/plugins/utils/react/performance/frameworks）
- 官方文档：https://gsap.com；官方示例仓库：greensock/gsap-skills（含 React/Vue/Nuxt/vanilla examples）
- 参考：`.prompt\前端\高级动效设计-20260328\prompt.md`（Flutter/Material 动效版，与本文互补）
