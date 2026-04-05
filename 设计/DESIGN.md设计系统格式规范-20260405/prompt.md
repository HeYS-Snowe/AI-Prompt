# DESIGN.md 设计系统格式规范

## 适用场景

- 使用 AI 编码代理（Claude Code、Cursor、Windsurf 等）生成一致 UI 时
- 使用 Google Stitch 根据 DESIGN.md 生成界面时
- 为项目建立可被 AI 理解的纯文本设计系统文档时
- 需要快速复制某网站视觉风格来构建新页面时

## 核心概念

DESIGN.md 是一种纯 Markdown 格式的设计系统文档，专为 AI 代理读取而设计。将它放入项目根目录，任何 AI 编码代理都能理解项目应有的视觉风格，从而生成像素级精确的 UI。

与 AGENTS.md 的关系对照：

| 文件 | 读者 | 定义内容 |
|------|------|----------|
| `AGENTS.md` | 编码代理 | 如何构建项目（技术规范） |
| `DESIGN.md` | 设计代理 | 项目应呈现的视觉与交互风格 |

## 九段式标准格式

每个 DESIGN.md 必须按以下 9 个章节组织，顺序固定，缺一不可。

---

### 第 1 章：Visual Theme & Atmosphere（视觉主题与氛围）

**目的**：用自然语言描述整体设计感觉、情绪基调和核心理念。这是 AI 理解设计意图的首要入口。

**必须包含的内容**：
- 一段 3-5 句的氛围描述（散文式，传达设计哲学）
- 字体系统概述（主字体、特色 OpenType 特性、最关键的字号/字重组合）
- 色彩概述（主色调、背景/前景关系、品牌色定位）
- **Key Characteristics** 列表（8-10 条，每条一句，覆盖字体、色彩、间距、圆角、阴影等核心视觉特征）

**编写要点**：
- 用比喻和意象传达感觉，而非仅列数据
- 指出"什么是这个设计最与众不同的地方"
- Key Characteristics 条目格式：`特征描述 — 具体参数`（如 "Geist Sans 极端负字间距 — 48px 时 -2.4px"）

---

### 第 2 章：Color Palette & Roles（色彩体系与角色）

**目的**：定义所有颜色的精确值和语义用途。

**必须包含的分组**：
- **Primary**（主色）：背景色、文字色、品牌主色
- **Interactive**（交互色）：链接色、悬停色、激活色、焦点色
- **Accent**（强调色）：辅助装饰色、渐变色
- **Neutral Scale**（中性色阶）：从最深的文字到最浅的背景的完整灰度
- **Surface & Borders**（表面与边框）：卡片背景、边框色、分隔线色
- **Shadows**（阴影色）：各层阴影的精确 rgba 值

**每个颜色的标准格式**：
```
- **语义名称** (`#十六进制`): CSS 变量名（如有），功能角色说明
```

**编写要点**：
- 每个颜色都必须有语义名称，不能用 "blue-1" 这类无意义命名
- 附上 CSS 变量名（如从网站源码提取到），增强可操作性
- 用一句话说明"为什么是这个颜色"（如 "Not pure black — the slight warmth prevents harshness"）

---

### 第 3 章：Typography Rules（排版规则）

**目的**：定义完整的字体层级体系。

**必须包含的内容**：

1. **Font Family** 部分
   - 主字体 + fallback 链
   - 等宽字体 + fallback 链
   - 启用的 OpenType 特性及原因

2. **Hierarchy** 层级表（Markdown 表格）

   | 列名 | 含义 |
   |------|------|
   | Role | 语义角色（如 Display Hero, Body, Caption） |
   | Font | 使用的字体 |
   | Size | 字号（px + rem） |
   | Weight | 字重 |
   | Line Height | 行高（标注 tight/normal/relaxed） |
   | Letter Spacing | 字间距（负值为紧缩） |
   | Notes | 使用场景备注 |

3. **Principles** 原则
   - 3-5 条排版哲学原则（如"负字间距贯穿所有层级"）

**编写要点**：
- 表格行数通常在 15-20 行，覆盖从最大 Display 到最小 Micro/Nano
- 字间距在标题层常为负值（-0.x 到 -3px），正文层趋向 normal
- OpenType 特性（ss01, liga, tnum, kern 等）需说明启用理由

---

### 第 4 章：Component Stylings（组件样式）

**目的**：定义所有 UI 组件的精确视觉参数。

**必须覆盖的组件**：
- **Buttons**（按钮）：Primary / Secondary / Ghost / Pill 等变体
- **Cards & Containers**（卡片与容器）：背景、边框、圆角、阴影、悬停态
- **Inputs & Forms**（输入与表单）：边框、焦点态、占位符、标签
- **Navigation**（导航）：背景、字号、悬停效果、移动端折叠策略
- **Badges / Tags / Pills**（徽章/标签/药丸）：背景色、圆角、字号
- **Distinctive Components**（特色组件）：该网站独有的标志性组件

**每个组件的标准格式**：
```
**组件名**
- Background: 颜色值
- Text: 颜色值
- Padding: 数值
- Radius: 数值
- Border: 数值（或 "none"）
- Font: 字体 字号 weight
- Hover: 悬停态描述
- Focus: 焦点态描述
- Use: 使用场景
```

---

### 第 5 章：Layout Principles（布局原则）

**目的**：定义间距系统、网格、留白哲学。

**必须包含的内容**：
- **Spacing System**：基准单位 + 完整间距刻度
- **Grid & Container**：最大内容宽度、列数策略
- **Whitespace Philosophy**：3-5 句描述留白理念
- **Border Radius Scale**：从最小到最大的圆角刻度

**编写要点**：
- 间距刻度通常以 8px 为基准，列出所有使用的值
- 留白哲学要用比喻说明（如 Apple 的 "cinematic breathing room"）
- 圆角刻度从 2px 到 9999px(pill)，标注每个级别的使用场景

---

### 第 6 章：Depth & Elevation（深度与层次）

**目的**：定义阴影系统和表面层级。

**格式**：层级表格 + 阴影哲学说明

| 列名 | 含义 |
|------|------|
| Level | 层级名称（Flat → Elevated → Deep） |
| Treatment | 精确的 CSS box-shadow 值 |
| Use | 使用场景 |

**编写要点**：
- 现代设计系统通常 4-6 个层级
- 阴影常用多层叠加（如 Vercel 的 border + elevation + ambient 三层）
- 需要单独的 **Shadow Philosophy** 段落解释设计意图

---

### 第 7 章：Do's and Don'ts（设计准则）

**目的**：设定设计护栏，防止 AI 生成偏离风格的元素。

**格式**：
- **Do** 列表：8-10 条"必须做"的规则
- **Don't** 列表：8-10 条"绝对不做"的规则

**编写要点**：
- 每条规则必须有明确理由（如 "Don't use weight 800+ — the maximum is 700"）
- 聚焦于最容易出错的方面（色彩使用范围、字重限制、圆角限制）
- 这是 AI 代理最直接的"约束条件"来源

---

### 第 8 章：Responsive Behavior（响应式行为）

**目的**：定义断点、触控目标、折叠策略。

**必须包含的内容**：
- **Breakpoints** 断点表（名称 + 宽度范围 + 关键变化）
- **Touch Targets** 触控目标尺寸
- **Collapsing Strategy** 各组件的折叠/缩放策略
- **Image Behavior** 图片响应行为

**编写要点**：
- 通常 5-7 个断点，从 Mobile Small 到 Large Desktop
- 触控目标最小 44x44px
- 重点说明"什么变了、什么不变"

---

### 第 9 章：Agent Prompt Guide（代理提示词指南）

**目的**：为 AI 代理提供即用型提示词片段。

**必须包含的内容**：
- **Quick Color Reference**：10-15 个最常用颜色的速查表
- **Example Component Prompts**：5-6 个可直接复制使用的组件生成提示词
- **Iteration Guide**：8 条迭代守则（AI 生成后的检查清单）

**编写要点**：
- 组件提示词必须包含所有精确参数（字号、字重、颜色、圆角等）
- 迭代守则按优先级排列，最重要的放前面
- 这是 AI 代理的"快速启动手册"

---

## 使用方式

### 基础用法
1. 选择一个网站的 DESIGN.md
2. 复制到项目根目录
3. 告诉 AI 代理："按照这个 DESIGN.md 的风格来构建页面"

### 进阶用法
1. 使用本格式规范为你的项目编写专属 DESIGN.md
2. 将多个 DESIGN.md 中喜欢的元素组合
3. 在迭代守则中添加项目特定的约束

### 参考来源
- 完整的 55 个网站 DESIGN.md 合集位于 `D:\Code\.prompt\awesome-design-md-main\design-md\`
- 涵盖 AI 产品、开发者工具、基础设施、设计工具、金融科技、消费品牌等类别
