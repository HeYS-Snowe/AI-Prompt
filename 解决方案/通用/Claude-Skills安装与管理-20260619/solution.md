# Claude Skills 安装与管理（npx skills 工具）

> 适用场景：在 Windows 本机为 Claude Code（及多个 coding agent）安装新的 Agent Skill，并纳入 `skills-lock.json` 管理体系
> 环境信息：Windows 11 + Git Bash + Node.js v24.11.0 + npm 11.6.1
> 生成日期：2026-06-19

---

## 问题

需要从 GitHub 仓库安装新的 Claude Agent Skill（如 `claude-api`、`vercel-optimize`），并让它：

1. 被 Claude Code 识别调用
2. 与现有 `.agents/skills/` + `.claude/skills/` 软链接体系保持一致
3. 在 `skills-lock.json` 中正确登记 `source` + `computedHash`

## 原因（关键认知）

这套 skills 管理体系由 **`vercel-labs/skills`** 这个 CLI（命令 `npx skills`）维护，**不是手动拷文件**。

核心坑在 `skills-lock.json` 里的 `computedHash`：

- 它是对 skill 文件夹内**每个文件的原始字节做 SHA-256**
- 已知存在**跨平台一致性问题**（Windows CRLF vs Linux LF、文件遍历顺序差异）
- 因此 hash **必须由工具自己算**，手动复刻算法极易失配 → lock 的完整性校验形同虚设
- 实测：用 5 种手算方式（单文件 hash、拼接 hash、排序拼接等）都对不上已知样本的 hash

结论：**放弃手动安装，全程用 `npx skills` 命令**，让工具统一处理下载、软链接、hash、lock 更新。

## 解决方案

### 安装命令

`cd` 到含 `skills-lock.json` 的项目根目录，**串行**安装（多个 add 都写同一个 lock 文件，并行会竞争写）：

```bash
cd /d/Desktop/Claude临时对话
DISABLE_TELEMETRY=1 npx --yes skills@latest add anthropics/skills --skill claude-api -y
DISABLE_TELEMETRY=1 npx --yes skills@latest add vercel-labs/agent-skills --skill vercel-optimize -y
```

参数说明：

| 参数 | 作用 |
|------|------|
| `<owner/repo>` | skill 来源仓库 |
| `--skill <name>` | 指定要装的 skill（不加会进入交互式选择） |
| `-y` | 跳过确认，默认采用 Symlink（推荐）安装方式 |
| `DISABLE_TELEMETRY=1` | 关闭遥测 |
| `--yes`（给 npx） | 自动确认首次下载 skills 包 |

工具会**自动检测已安装的 agent**，把 skill 装到所有 agent（无需手写 `-a`）。

### 预检（只读，强烈建议先做）

```bash
npx --yes skills@latest list                     # 查看已装 skill 及其 agent 映射、canonical 位置
npx --yes skills@latest add <owner/repo> --list  # 只读列出某仓库可装的 skill 及其确切 id
```

预检能避免 skill 名不符（internal skill、命名前缀差异）导致装错。

### 体系架构

- **canonical 实体**：`.agents/skills/<name>/`（universal agent 共享目录，single source of truth）
- **软链接**：`.claude/skills/<name>` → `.agents/skills/<name>`（Claude Code 专属目录接入）
- **清单**：`skills-lock.json` 记录每个 skill 的 `source`（GitHub repo）、`skillPath`、`computedHash`
- **现有 4 个来源仓库**：`anthropics/skills`、`obra/superpowers`、`vercel-labs/agent-skills`、`remotion-dev/skills`

### 命名约定（vercel 仓库特有）

`vercel-labs/agent-skills` 里若 skill 名本身不含 brand（如 `react-best-practices`、`composition-patterns`），lock/目录会加 `vercel-` 前缀；名字本身已够明确（如 `deploy-to-vercel`、`web-design-guidelines`）则不加前缀。安装时用 `--list` 确认确切 id。

## 验证方式

安装后实测四项，**不轻信工具自报成功**：

1. **实体目录**：`ls .agents/skills/<name>/` 内容与 GitHub 仓库一致
2. **软链接**：`ls -la .claude/skills/<name>` 指向 `.agents/skills/<name>`
3. **软链接可读**：能读到 `SKILL.md`，frontmatter 的 `name` 正确
4. **lock 登记**：`skills-lock.json` 出现新条目（新版 CLI 会多带 `skillPath` 字段，旧条目没有，不影响功能）

最后 `npx skills list` 应显示总数 +N 且包含新 skill。

## 避坑点

- **重启会话才生效**：Claude Code 在会话**启动时**加载 skill 列表，新装的 skill 在当前会话不可用，需重启或开新会话
- **安全评估**：工具会跑第三方安全扫描（Snyk / Socket），如 `claude-api` 报 Snyk Med Risk —— 关注但不必阻断，详情可查 `https://skills.sh/<owner>/<repo>`
- **GitHub 限流**：未设 `GITHUB_TOKEN` 时可能触发 rate limit，工具会 fallback 到 git clone（稍慢；已 `gh auth login` 可缓解）
- **多 skill 串行**：用 `&&` 串接，避免并发写 `skills-lock.json` 竞争
- **首次 npx 较慢**：第一次 `npx skills` 要下载包，后续走缓存

## 相关

- 41 个 skill + 13 个 agent 的简介清单见 `通用/Claude-Skills与Agents清单-20260619/prompt.md`
- 来源：`vercel-labs/skills` 仓库；hash 跨平台差异 issue #781
