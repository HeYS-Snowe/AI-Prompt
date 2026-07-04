# Claude Skills 与 Agents 清单

> 适用场景：快速查阅本机已安装的 Claude Agent Skills（41 个）与自定义 Subagents（13 个）各自做什么、何时触发，便于会话中调用与复用。
> 维护方式：Skills 由 `npx skills`（vercel-labs/skills）管理，实体位于 `D:\Desktop\Claude临时对话\.agents\skills\`，`.claude\skills\` 为软链接；Agents 定义位于 `C:\Users\aaa\.claude\agents\`。
> 触发机制：Skills 依据 `SKILL.md` 的 description 自动触发，无需手动调用；Agents 由主代理按场景调度。
> 生成日期：2026-06-19

---

## 一、已安装的 Agent Skills（41 个）

按来源仓库分组。Skill 名即目录名，可直接引用。

### 1. anthropics/skills（18 个）— 官方文档 / 设计 / 工具类

| Skill | 简介 |
|-------|------|
| claude-api | Claude API / Anthropic SDK 参考手册：模型 id、定价、参数、流式、工具调用、MCP、缓存、token 计数、模型迁移 |
| docx | 创建 / 读取 / 编辑 Word 文档（.docx），含目录、页码、表格等排版 |
| pdf | PDF 全套操作：读取 / 合并 / 拆分 / 填表 / 加水印 / 加解密 / OCR |
| pptx | 创建 / 读取 / 编辑 PowerPoint（.pptx）演示文稿 |
| xlsx | 创建 / 读取 / 编辑 / 清洗电子表格（.xlsx / .xlsm / .csv） |
| doc-coauthoring | 引导用户走结构化的文档协作撰写流程 |
| frontend-design | 创建有设计感、可投产的高质量前端界面 |
| web-artifacts-builder | 用模型创建复杂的 claude.ai 多组件 HTML artifacts |
| webapp-testing | 用 Playwright 与本地 web 应用交互并端到端测试 |
| mcp-builder | 创建高质量 MCP（Model Context Protocol）服务器的指南 |
| skill-creator | 创建 / 修改 / 改进 skill 并衡量其表现 |
| algorithmic-art | 用 p5.js 创作算法艺术（流场、粒子系统），支持随机种子与交互参数 |
| canvas-design | 用设计理念创作 .png / .pdf 格式的精美视觉艺术 |
| brand-guidelines | 将 Anthropic 官方品牌色与字体应用到各类产出物 |
| theme-factory | 为幻灯片 / 文档 / 报告等产出物统一应用主题样式 |
| internal-comms | 撰写各类内部沟通文档的资源与模板 |
| slack-gif-creator | 制作适配 Slack 的动图 GIF（含尺寸约束） |
| template-skill | Skill 模板（占位，供创建新 skill 时参考） |

### 2. obra/superpowers（14 个）— 开发流程与方法论

| Skill | 简介 |
|-------|------|
| using-superpowers | 会话开始时使用，建立如何发现和使用 skill 的机制 |
| brainstorming | 任何创造性工作（功能 / 组件 / 新增）前必须使用的头脑风暴流程 |
| writing-plans | 有多步任务的规格 / 需求时、动手写代码前，先写实现计划 |
| executing-plans | 在独立会话中执行已写好的实现计划（带评审） |
| subagent-driven-development | 在当前会话用子代理执行含独立任务的实现计划 |
| dispatching-parallel-agents | 面对 2+ 个无共享状态、可并行的独立任务时使用 |
| test-driven-development | 实现任何功能 / 修复前，先写测试的 TDD 流程 |
| systematic-debugging | 遇到 bug / 测试失败 / 异常行为时，提出修复前的系统化调试法 |
| verification-before-completion | 声称工作完成 / 修复 / 通过之前，进行验证 |
| requesting-code-review | 完成任务 / 重大功能 / 合并前，请求代码评审以验证质量 |
| receiving-code-review | 收到代码评审反馈后、实施建议前使用 |
| finishing-a-development-branch | 实现完成、测试通过后，决定如何合并 / 收尾分支 |
| using-git-worktrees | 需要与当前工作区隔离地启动功能开发时，使用 git worktree |
| writing-skills | 创建 / 编辑 / 验证 skill 时使用 |

### 3. vercel-labs/agent-skills（8 个）— React / Vercel 工程

| Skill | 简介 |
|-------|------|
| deploy-to-vercel | 部署应用到 Vercel（"部署我的应用""给我链接"） |
| vercel-cli-with-tokens | 用 token 认证方式经 Vercel CLI 部署和管理项目 |
| vercel-react-best-practices | Vercel 工程团队的 React / Next.js 性能优化指南 |
| vercel-composition-patterns | 可扩展的 React 组合模式（复合组件 / render props / context），重构布尔参数泛滥 |
| vercel-react-native-skills | React Native / Expo 构建高性能移动应用的最佳实践 |
| vercel-react-view-transitions | 用 React View Transition API 实现流畅的页面 / 元素过渡动画 |
| vercel-optimize | Vercel 已部署项目的成本与性能优化（基于真实指标给出排序建议） |
| web-design-guidelines | 按 Web Interface Guidelines 审查 UI 代码（"审查我的 UI"） |

### 4. remotion-dev/skills（1 个）— 视频

| Skill | 简介 |
|-------|------|
| remotion-best-practices | Remotion（用 React 创作视频）的最佳实践 |

---

## 二、自定义 Claude Code Subagents（13 个）

定义于 `C:\Users\aaa\.claude\agents\`，由主代理按场景调度。

| Agent | 简介 |
|-------|------|
| product-manager | 分析需求、规划功能、创建产品文档（新功能开发的第一步） |
| ui-designer | UI / UX 设计（新界面、组件库、设计系统、响应式适配） |
| frontend-designer | UI 设计规格完成后，实现为功能性前端代码 |
| backend-engineer | 开发 / 修改 / 调试后端 API、业务逻辑、数据库结构、后端性能与安全 |
| ai-integration-engineer | 需集成 AI / ML 功能（LLM 对话、推荐、智能自动化、模型部署、RAG）时 |
| api-test-pro | 全面的 API 测试与质量保证（契约 / 功能 / 性能 / 安全） |
| performance-expert | 跨前端 / 后端 / 数据库 / 基础设施分析并优化系统性能 |
| bug-detector | 代码写完或修改后做安全漏洞检测与代码质量分析（OWASP Top 10、静态分析、依赖审计） |
| bug-fixer | 检测到代码问题 / bug / 漏洞后进行诊断与修复 |
| devops-engineer | 部署应用、配置 CI/CD、监控告警、处理系统故障、基础设施扩缩 |
| doc-engineer | 依赖管理、环境配置更新、技术文档创建并与代码同步 |
| logger | 记录代码变更、构建失败、运行时崩溃、配置更新等项目事件 |
| version-manager | 应用构建产物（APK / IPA / AAB）按命名规范重命名与版本管理 |

---

## 三、相关命令速查

```bash
# 查看已装 skill
cd /d/Desktop/Claude临时对话 && npx skills list

# 安装 / 更新 / 卸载
npx skills add <owner/repo> --skill <name> -y
npx skills update <skill>
npx skills remove <skill>
```

详见记忆文件 `skills-install-workflow`。
