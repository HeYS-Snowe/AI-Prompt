# 设计系统 Prompt 架构

> 适用平台：所有 AI 编程工具
> 核心原则：将设计系统转化为 AI 可执行的结构化 Prompt 规范
> 参考来源：Brian C. (Substack) - Vibe Coding 设计系统指南、火山引擎 - Vibe Coding 工程化最佳实践

---

## 一、风格 Prompt 的九段式结构

将设计系统翻译为 AI 可执行的 Prompt 规范，不再零散描述各个视觉元素，而是构建一份完整的"风格 Prompt 架构"：

```
§1 Role 定义 → AI 的身份和设计哲学
§2 Design Token → 色彩、字体、圆角、阴影的精确数值
§3 排除清单 → 明确禁止的视觉元素
§4 组件规格 → 各组件的具体样式规则
§5 版面策略 → Grid 系统和间距规范
§6 动效系统 → 核心原则 + 分类定义
§7 响应式策略 → 断点 + 适配规则 + 视觉特征保留
§8 无障碍规范 → 对比度 + 焦点状态 + 语义化 HTML
§9 技术规范 → 字体加载 + 自定义工具类 + 性能约束
```

---

## 二、Design Token 体系

在 Prompt 中用精确数值定义设计变量：

```
色彩系统：
- Primary: #111111 (主文字)
- Background: #F9F9F7 (米白底色)
- Accent: #CC0000 (编辑红，用于强调)
- 排除清单：No blur, No inner shadows, No gradients, No rounded corners

字体系统：
- 标题：Playfair Display (衬线)
- 正文：Lora (衬线)
- 界面：Inter (无衬线)
- 代码：JetBrains Mono (等宽)
```

---

## 三、视觉风格定义的三种策略

### 策略一：关键词法

直接使用风格关键词描述：

- Modern（现代）、Minimalist（极简）、Playful（活泼）、Brutalism（粗野主义）
- Glassmorphism（玻璃拟态）、Neumorphism（新拟态）、Editorial（编辑风格）

### 策略二：对标法（最佳捷径）

引用知名产品作为视觉参考：

```
"Design style similar to Notion/Linear/Airbnb"
"Apple Human Interface Guidelines"
"参考 Linear.app 的设计语言"
```

### 策略三：技术规范法

明确指定 CSS 框架和组件库：

```
"使用 Tailwind CSS + Shadcn UI"
"主色调为靛蓝色 (#6366f1)，背景使用柔和的浅灰色，
  卡片带有轻微的阴影和圆角"
```

**推荐组合使用：关键词 + 对标法 + 排除清单**

---

## 四、Anti-Pattern 声明方法

不仅定义"要做什么"，更要定义"不能做什么"。这种方法能有效防止 AI "自作主张"加入不符合风格的元素。

```
排除清单示例：
- No blur, No inner shadows, No gradients
- No rounded corners (强制 border-radius: 0)
- No bouncy or organic easing
- 绝不将红色文字放在黑色背景上（对比度不足）
- 禁止对 box-shadow 做动态变化（性能原因）
```

---

## 五、动效系统定义法

### 核心原则定义

首先用一句话为整个动效系统定调：

```
Fast, snappy, mechanical. No bouncy or organic easing.
```

### Transition 分类逻辑

```
"transition-all duration-200 ease-out"    /* 涉及位移、大小等多属性变化 */
"transition-colors duration-200"          /* 仅颜色变化 */
```

- `transition-all` 用于需要同时改变多个属性的场景（如卡片 Hover 时的位移 + 阴影 + 背景色）
- `transition-colors` 专门用于只有颜色改变的场景（如按钮的黑白反转）
- 背后有性能考量：精确指定属性可让浏览器专注处理真正有变化的部分

### Hover 行为的五种类型

```
1. 色彩反转：按钮、图标在黑白之间瞬间切换
2. 偏移阴影：卡片 Hover 时出现往右下偏移的实色阴影 + 轻微位移(Translate)
3. 底线：链接出现粗底线（decoration-2 decoration-[#CC0000]）
4. 缩放：小型元素如圆点可以 hover:scale-150
5. 背景：容器 Hover 时加上淡灰色背景（hover:bg-neutral-100）
```

---

## 六、版面配置策略

```
- 基于 12 栏 Grid 系统
- 不对称比例：8:4 或 5:7
- 8px 基准间距系统：
  Tight: 8px, Standard: 16px, Comfortable: 32px, Spacious: 64px
```

---

## 七、响应式策略

### 跨设备核心视觉特征保留

```
即使在手机小屏上也必须保留的视觉特征：
- 直角（Zero radius）
- 高对比
- 水平线分隔区段
- 大写标签与 metadata
```

---

## 八、设计系统风格 Prompt 模板（可直接复用）

```
## 风格定义：[风格名称]

### 核心设计哲学
[一句话概括风格的精髓，例如："Fast, snappy, mechanical. No bouncy or organic easing."]

### Design Tokens
色彩：
- Primary: [色值] (用途)
- Background: [色值] (用途)
- Accent: [色值] (用途)
- 排除：[明确禁止的色彩/效果]

字体：
- 标题：[字体名] ([衬线/无衬线])
- 正文：[字体名]
- 界面：[字体名]
- 代码：[字体名]

### 组件规格
[列出关键组件的样式规则]

### 动效系统
核心原则：[一句话]
- Transition 分类：[按场景分类的动画规范]
- Hover 行为：[分类型的交互规范]

### 排除清单
[明确禁止的视觉元素和效果]

### 响应式策略
- 断点：Mobile (<768px) / Tablet (768px+) / Desktop (1024px+)
- 适配规则：[Grid 折叠、间距缩减、字体缩放等]
- 必须保留的视觉特征：[跨设备一致的核心元素]

### 无障碍
- 对比度标准：[WCAG AA/AAA]
- 焦点状态：[具体样式]
- ARIA 要求：[必须的 ARIA 属性]

### 技术实现
- CSS 框架：[Tailwind CSS]
- 组件库：[Shadcn UI]
- 性能约束：动画只用 transform 和 opacity
```

---

## 九、参考来源

| 来源                                       | 核心贡献             |
| ---------------------------------------- | ---------------- |
| Brian C. - Vibe Coding 设计系统指南 (Substack) | 风格 Prompt 9 段式架构 |
| 火山引擎 - Vibe Coding 工程化最佳实践               | 分层解耦开发流程         |
