# 设计风格图鉴 Design Style Atlas

> 前端设计风格的「理论 + 实践」配套知识库,供人和 AI 参考。
> 看到好看,叫得出名字,复刻得出来。

---

## 这是什么

一套覆盖 93 种前端设计风格的图鉴,按 6 大流派分册。每种风格同时提供:

- **理论**(本目录下的分册 md):精髓、配色、字体、视觉特征、复刻要点、即用 Prompt
- **实践**(`实践/demos/*.html`):可浏览器打开的可视化 demo,配色可点击复制 hex

理论是给人和 AI 读的「为什么这样设计 + 怎么复刻」;实践是给人看的「做出来长什么样」。两者配套,缺一不可。

---

## 目录结构

```
设计风格图鉴-20260704\
├── README.md                  本文件:索引与使用说明
├── styles.json                93 风格结构化数据(机器可读,AI 直接引用)
├── 复刻实战指南.md             三步法 / Prompt 模板 / 混搭 / 避坑
├── 01-网页表面风格.md          20 种:glass / neumorphism / claymorphism / bento ...
├── 02-氛围主题风格.md          33 种:brutalism / neobrutalism / swiss / bauhaus / y2k / cyberpunk ...
├── 03-沉浸式3D.md              8 种:spatial / clay3d / lowpoly / particle / holographic ...
├── 04-移动端App.md             14 种:ios / android / cardfeed / bottomsheet / widget ...
├── 05-桌面软件.md              10 种:macos / win11 / ide / admin / console ...
├── 06-复合风格.md              8 种:linearbento / glassclay / cyberhud / bentobrutal ...
└── 实践\
    ├── 前端设计风格图鉴.html   可视化总览(浏览器打开:搜索 / 筛选 / 点开看详情)
    └── demos\                  93 个单风格 demo(每个含配色点击复制 + 即用 Prompt)
```

---

## 6 大流派速查

| 流派 | 分册 | 数量 | 一句话 |
|---|---|---|---|
| 网页表面风格 | 01 | 20 | 表层质感:玻璃、黏土、扁平、便当盒、金属、纸张 |
| 氛围主题风格 | 02 | 33 | 情绪表达:野性、极简、杂志、Y2K、赛博、蒸汽波 |
| 沉浸式 / 3D | 03 | 8 | 空间深度:3D 黏土、低多边、粒子、全息、液态玻璃 |
| 移动端 App | 04 | 14 | 触屏范式:iOS/安卓原生、卡片流、底部弹层、小组件 |
| 桌面软件 | 05 | 10 | 专业界面:macOS、Win11、IDE、后台、云控制台 |
| 复合风格 | 06 | 8 | 黄金混搭:当代产品高辨识配方 |

---

## 人怎么用

1. **找灵感**:浏览器打开 `实践/前端设计风格图鉴.html`,搜索 / 筛选风格,点开卡片看详情
2. **看效果**:点详情里的「Demo」打开 `实践/demos/<风格>.html`,直观看做出来什么样
3. **学复刻**:打开对应分册 md,读「视觉特征 + 复刻要点」理解为什么这样设计
4. **抄配色**:demo 里配色色块点击即复制 hex
5. **动手做**:按 `复刻实战指南.md` 的三步法,用「即用 Prompt」驱动 AI 生成

## AI 怎么用(Vibe Coding)

两种引用方式:

- **精准**:把 `styles.json` 中目标风格的对象直接喂给 AI,字段齐全(essence / features / replicate / palette / type),AI 可严格按数据复刻
- **速查**:把分册 md 里该风格的「即用 Prompt」整段粘给 Claude Code / Cursor / CodeX

典型流程:用户说「我要做个 Linear 风的落地页」→ AI 读 `06-复合风格.md` 的 linearbento 或相关条目 → 按即用 Prompt + 配色生成代码。

---

## 数据源说明

- `styles.json`:93 风格的完整结构化数据,每条含 `id / en / zh / cat / era / keywords / essence / palette / type / features / replicate / examples`。AI 友好,可直接 `JSON.parse` 使用。
- 配色、字体、复刻代码均来自原始图鉴,经结构化提取,未手工篡改。
- `实践/demos/` 下每个 demo 自包含(纯 HTML+CSS+JS),离线可用。

---

## 与 .prompt 其他库的关系

| 库 | 定位 | 关系 |
|---|---|---|
| 本图鉴 | 横向:93 种具体风格长什么样、怎么复刻 | 选风格 |
| `.prompt/设计/` | 纵向:通用设计原则与方法论 | 定基调 |
| `.prompt/前端/`(其他) | 实现规范(如亚克力/液态玻璃的 Flutter 实现) | 落地代码 |
| `.prompt/awesome-design-md-main/` | 真实公司的品牌设计系统 DESIGN.md | 真实参照 |

配合食用顺序:**原则定基调 → 本图鉴选风格 → 实现规范落地代码 → 品牌库做参照**。

---

*编撰于 2026-07-04。新增风格或修正配色,请同步更新 `styles.json` 与对应分册 md,二者同源。*
