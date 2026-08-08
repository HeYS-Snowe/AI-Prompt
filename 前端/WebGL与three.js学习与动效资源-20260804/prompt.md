# WebGL / three.js 学习与动效资源

> 2026-08-04 网络搜集整理。覆盖：学习路径、GLSL 着色器、以及用户关注的动效类型（simplex noise、WebGL 流体加载、引力透镜与涟漪、流光动效）。

## 一、学习路径（推荐顺序）

1. **WebGL 基础**（可选但推荐先看）：[WebGL3D 中文网](https://www.webgl3d.cn/pages/d30795/) — 从 WebGL 入门再学 Three.js Shader 更容易
2. **Three.js 主线**：
   - [Threejs 指南（中文）](https://threejs-learning.com/zh/) — 从零掌握 WebGL 3D 编程，含着色器教程、GLSL 学习资源、交互式编辑器、API 参考
   - [Three.js 官方示例](https://threejs.org/examples/) — 官方全部示例（shader/lava/ocean/sky/tsl 等）
   - [Three.js 完全学习指南（掘金）](https://juejin.cn/post/7505675796907360283) — 中文教程系列：入门→进阶→复杂 3D 应用
3. **GLSL 着色器**：
   - [The Book of Shaders](https://thebookofshaders.com) — 着色器编程圣经（含 simplex noise 章节，作者 patriciogonzalezvivo）
   - [ThreeJS-Shader（GitHub csdjk）](https://github.com/csdjk/ThreeJS-Shader) — 中文注释的 GLSL 特效 demo，从简单线条到炫酷特效逐步深入
   - [Three.js Shader 资源集合](https://threejsresources.com/category/shaders) — GLSL/TSL 编辑器、shader 画廊、噪声库、学习参考聚合
   - [腾讯云：学习 Three.js 最佳平台](https://cloud.tencent.com/developer/article/2390519) — 官方文档、中文网、在线编辑器、**Shadertoy**、**glsl.app** 五个平台

## 二、用户关注动效类型对应资源

| 动效类型 | 资源 | 说明 |
|----------|------|------|
| Simplex 噪声 | [patriciogonzalezvivo GLSL Simplex Noise Gist](https://gist.github.com/patriciogonzalezvivo/aa143699b07aaf127ff60c9dcb1d3f1e) | 最常用的 GLSL simplex noise 实现（Book of Shaders 作者），是程序化纹理/流体/云彩的基础 |
| WebGL 流体加载/模拟 | [WebGL-Fluid-Simulation（paveldogreat）](https://github.com/paveldogreat/WebGL-Fluid-Simulation) | 最著名的 WebGL 流体模拟，移动端可用，[在线 Demo](https://paveldogreat.github.io/WebGL-Fluid-Simulation/) |
| 引力透镜 / 黑洞 | [gravy（portsmouth）](https://github.com/portsmouth/gravy) | WebGL 引力透镜物理模拟 |
| 引力透镜 / 黑洞 | [black-hole（Scenes3D）](https://github.com/Scenes3D/black-hole) | Three.js + 自定义 GLSL + Vite 的实时黑洞效果 |
| 引力透镜 / 黑洞 | [black-hole（oseiskar）](https://github.com/oseiskar/black-hole) | 史瓦西黑洞光线路径计算，物理较准确 |
| 涟漪 / 水波纹 | [amandaghassaei Shaders 集合](https://amandaghassaei.com/projects/shaders) | 大量物理模拟 fragment shader（含波纹类），适合拆解学习 |
| 流光 / 流体光效 | [Fluid Light（threejs3d）](https://threejs3d.com/examples/shaderweb1) | Three.js + WebGL 流体光效互动网页特效 |

## 三、核心概念速览（给 AI 拆解动效用）

- **GLSL 着色器**：vertex shader（顶点位置）+ fragment shader（像素颜色），WebGL 渲染管线的核心
- **噪声函数**：simplex noise / value noise / fbm（分形布朗运动）——程序化生成纹理、流体、云、地形的数学基础；fbm 是"多层噪声叠加"，产生自然感
- **流体模拟**：Navier-Stokes 方程在 GPU 上实时求解（速度场+压力场+密度场，ping-pong 纹理渲染）
- **引力透镜**：光线在质量附近弯曲（相对论效应），shader 中常用"背景重采样+径向畸变"近似
- **涟漪**：径向波方程叠加，常见于 post-processing 或 UV 置换
- **Three.js 上手**：Scene → Camera → Renderer → Mesh（Geometry + Material）→ 动画循环 requestAnimationFrame；ShaderMaterial 直接写 GLSL

## 四、与现有沉淀配合

- 拆解动效后的提示词沉淀 → `.prompt\前端\`（参考 GSAP动画完整提示词-20260804 的结构：适用场景/核心范式/最佳实践）
- 组件/灵感资源 → `.prompt\前端\前端设计资源集合-20260804\prompt.md`
- 如需下载以上特效库源码到本地归档（类似 libs/ 流程），在会话中提出即可
