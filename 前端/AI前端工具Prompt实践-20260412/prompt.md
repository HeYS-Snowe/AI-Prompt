# AI 前端工具 Prompt 实践

> 适用平台：v0.dev / Bolt.new / Cursor / Lovable / Replit
> 核心原则：不同工具各有擅长，选择对的工具比优化 Prompt 更重要
> 参考来源：Bolt.new 官方文档、Addy Osmani 博客、Beyond the Build、Aakash Gupta 教程

---

## 一、工具选择指南

| 工具          | 最适合场景      | 核心优势          | 数据持久化       |
| ----------- | ---------- | ------------- | ----------- |
| **v0**      | 精美前端 UI 组件 | 设计感强，组件质量高    | 需第三方集成      |
| **Bolt**    | 快速全栈原型     | 浏览器内运行，迭代快    | 需 Supabase  |
| **Lovable** | 非技术人员使用    | 低门槛，友好界面      | Supabase 同步 |
| **Cursor**  | 精细开发与修 bug | 专业 IDE，上下文理解强 | 原生支持        |
| **Replit**  | 需要数据持久化    | 内置数据库和认证      | 内置          |

**推荐工作流**：先用 Bolt/Lovable 生成初始设计 → 导入 Cursor 进行精细化修改 → 部署到 Vercel

---

## 二、v0.dev Prompt 最佳实践

### 核心定位

擅长生成精美的前端 UI 组件

### Prompt 策略

1. **像写设计简报一样写 Prompt** — 描述意图、用户目标、布局需求，而非纯粹的 UI 描述
2. **像设计师一样思考，像开发者一样表达** — 提及表单验证、viewport 高度、暗色/亮色模式、组件状态等
3. **先从单个组件开始**，逐步构建整个页面
4. **使用截图作为视觉参考** — v0 支持上传 mockup 或截图来引导生成
5. **可选中特定元素进行定向修改**

### v0 Prompt 示例

```
Task: Build a responsive header in Next.js App Router.
Context: Files live under app/(marketing)/. Use Tailwind and next/link.
Constraints: Server Components by default; only the mobile menu is "use client".
  Accessibility: keyboard focus, aria-expanded.
Output: Create Header.tsx and MobileMenu.tsx. Minimal CSS classes. No external deps.

Return output as a unified diff inside ```diff fences.
```

### v0 的局限

- 几轮提示后，所有结果开始看起来相似
- 不了解你的上下文、市场环境或品牌故事
- 迭代微调不够流畅

---

## 三、Bolt.new Prompt 最佳实践

### 核心定位

快速原型，灵活迭代，浏览器内运行

### Prompt 策略

1. **从应用架构开始**，包括工具、框架的选择
2. **定期清理上下文**，只要确定 Bolt 不再需要记住短期信息
3. **逐个添加组件和功能**，一次一个
4. **每个组件用小而具体的提示词添加细节**，避免一次给太多指令
5. **明确说明什么应该改变、什么不应该改变**，引用特定的元素、类名或函数
6. **不要期望 LLM 有常识**

### Bolt 项目级 System Prompt 模板

```
For all designs I ask you to make, have them be beautiful, not cookie cutter.
Make webpages that are fully featured and worthy for production.

By default, this template supports JSX syntax with Tailwind CSS classes,
the shadcn/ui library, React hooks, and Lucide React for icons.
Do not install other packages for UI themes, icons, etc unless absolutely
necessary or I request them.

Use icons from lucide-react for logos.
Use stock photos from unsplash where appropriate.
```

### Bolt MEGA PROMPT 策略（一次性生成完整应用）

```
技术栈锁定：
- Frontend: React + TypeScript + Tailwind CSS
- Backend: [选择]
- Database: [选择]
- Auth: [选择]

功能清单（按优先级排列）：
1. [核心功能]
2. [次要功能]

设计规范：
- 风格参考：[产品名]
- 色彩方案：[具体色值]
- 响应式要求：[断点]

禁止事项：
- 禁止引入未指定的第三方库
- 禁止硬编码 API 密钥
```

---

## 四、Cursor Prompt 最佳实践

### 核心定位

专业的 AI 编程 IDE，适合精细化修改和持续开发

### 核心工作流

```
需求分析(5-10min) → 架构设计(10-15min) → 编码实现 → 代码审查(15-20min) → 测试 → 提交
```

编码实现阶段使用四个层次的 AI 协作：

- **Composer**（Cmd+I）：多文件协同编辑，创建文件结构
- **Inline Edit**（Cmd+K）：原地修改代码，局部优化
- **Tab 补全**：无感知的日常代码补全
- **Chat**（Cmd+L）：结对编程，解决卡点

### 上下文管理技巧

- `@文件名` 精确引用特定文件的风格
- `@codebase` 全局搜索保持风格一致
- `@docs` 引用官方文档写法
- 开启新话题时主动清理上下文

### Cursor "Task + Context + Constraints + Output" 模式

```
Task: Build a responsive header in Next.js App Router.
Context: Files live under app/(marketing)/. Use Tailwind and next/link.
Constraints: Server Components by default; only the mobile menu is "use client".
  Accessibility: keyboard focus, aria-expanded.
Output: Create Header.tsx and MobileMenu.tsx. Minimal CSS classes.
  No external deps. Return output as a unified diff.
```

### 纠错 Prompt

```
Re-generate: Server Components only. Move non-interactive code out of "use client".
Only MobileMenu.tsx should be client.
```

---

## 五、Agent Skills 设计思路

### Skills 的本质

Skills = 领域专业知识 + 你的项目偏好 + 严厉的审查官

Skills 解决的是大模型"博而不精"的缺陷，将通才 AI 转变为专才 AI。

### Skills 文件夹三要素

1. **规约（Rules）**：`.cursorrules` 或 `.md` 文件，告诉 AI "准许做什么"和"严禁做什么"
2. **上下文（Context）**：项目特殊结构（路由位置、接口封装方式）
3. **工具（Tools）**：自动化脚本（如代码生成后自动运行 `npm lint`）

### 通才 AI vs 专才 AI

| 维度   | 通才 AI     | 安装 Skills 后的专才 AI |
| ---- | --------- | ----------------- |
| 思维边界 | 无边界，易产生幻觉 | 严格锁定在当前技术栈内       |
| 项目理解 | 只看当前文件    | 理解路由、状态管理、样式体系    |
| 输出质量 | "大概能跑"的代码 | 符合工程直觉的生产级代码      |
| 角色定位 | 知识检索器     | 虚拟技术负责人           |

---

## 六、常用 Prompt 模板

### 代码审查模板

```
请审查这段代码，关注：
1. 潜在的安全问题（XSS、注入、敏感信息泄露）
2. 性能问题（不必要的循环、内存泄漏风险）
3. 可维护性问题（魔法数字、重复代码、过长函数）
4. 类型安全问题
用表格形式列出问题，按严重程度排序。
```

### 重构模板

```
重构这段代码，目标：
1. 降低圈复杂度到 5 以下
2. 提取重复逻辑为独立函数
3. 添加适当的错误处理
4. 保持向后兼容
先解释重构思路，再给出代码。
```

### 单元测试模板

```
为以下函数编写完整的 Jest 单元测试：
- 覆盖正常路径
- 覆盖边界情况
- 覆盖错误情况
- 使用 describe/it 结构
- 包含有意义的测试描述
```

---

## 七、参考来源

| 来源                                     | 核心贡献              |
| -------------------------------------- | ----------------- |
| Bolt.new 官方 - Prompting Effectively    | Bolt 专用 Prompt 技巧 |
| Addy Osmani - LLM Coding Workflow      | Cursor 工作流与最佳实践   |
| Beyond the Build - Building with v0    | v0 实践指南           |
| Aakash Gupta - AI Prototyping Tutorial | 工具对比与选择           |
| GitHub Gist - Bolt.new MEGA PROMPT     | 一次性应用生成模板         |
| 掘金 - 前端项目常用的三个 Skills                  | Agent Skills 设计思路 |
