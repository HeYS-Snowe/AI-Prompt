# 生产可用库清单（本地归档 + npm 引用）

> 2026-08-04 从 GitHub 下载、本地构建归档；生产项目可 npm 引用或引用本地构建产物。
> 库源码与构建产物：`D:\Code\AI资源管理\libs\`（详细引用说明见 `libs\README.md`）

## 清单

| 库 | 版本 | 类型 | 生产引用 | 构建状态 |
|----|------|------|----------|----------|
| animejs | 4.5.0 | JS 动画引擎 | `npm i animejs`；或本地 `dist/bundles/anime.umd.min.js`（全局 `anime`）/ `anime.esm.min.js` | 已构建 |
| thinking-orbs | 0.2.0 | 思考球加载组件（9 状态） | `npm i thinking-orbs`；`import { ThinkingOrb } from 'thinking-orbs'` | 已构建 |
| sticker-forge | 0.1.0 | WebGL 贴纸 Web Component | 未发布 npm，本地引用 `embed/sticker-forge.iife.js` 或 `.es.js`（自动注册 `<sticker-forge>`） | 已构建 |
| canvas-ui | 0.1.0 | Canvas 创意组件库（33 组件） | 未发布 npm，官方站点 canvasui.dev；本地 `src/` 源码参考 | 源码归档 |

## 快速用法

### animejs

```javascript
import anime from 'animejs';
anime({ targets: '.el', translateX: 100, duration: 800, easing: 'easeOutExpo' });
```

### thinking-orbs（AI/Agent UI 专用）

```tsx
import { ThinkingOrb } from 'thinking-orbs';
<ThinkingOrb state="searching" size={64} />
// 9 状态：working/searching/solving/listening/connecting/weaving/composing/breathing/shaping
// 尺寸：64（聊天头像级）/ 20（行内文本级）；自动适配明暗主题
```

### sticker-forge（文本/图片 → 可撕贴纸）

```html
<script src="sticker-forge.iife.js"></script>
<sticker-forge src="image-or-text" />
<!-- 或 ES module：import 'sticker-forge.es.js' 后使用 <sticker-forge> -->
```

### canvas-ui

- 框架无关（React/Vue/Svelte/Solid/Preact），HTML-in-canvas 读取活动 DOM，不支持时回退 WebGL overlay
- **许可注意：MIT + Commons Clause，商用需评估**

## 提示

- 全部插件/库免费；animejs 与 thinking-orbs 生产优先走 npm，内网/离线用本地产物
- 相关 skill 已安装：gsap 8 个（`~/.deepcode/skills/gsap-*`，动画实现首选推荐）
- 更新此清单时同步更新 `D:\Code\AI资源管理\libs\README.md` 与 `MIGRATION-SUMMARY.md`
