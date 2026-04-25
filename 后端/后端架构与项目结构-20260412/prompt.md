# 后端架构与项目结构规范

> 适用平台：所有 AI 编程工具
> 核心原则：项目初始化先行、文件治理、单一职责
> 参考来源：火山引擎 Vibe Coding 实践、Addy Osmani 博客、社区最佳实践

---

## 一、项目初始化 Prompt

```
# 项目初始化
创建一个 [FastAPI / Express / NestJS] 后端项目，用于 [项目描述]。

## 技术栈
- 语言：[Python 3.11+ / Node.js 20+ / TypeScript]
- 框架：[FastAPI / Express / NestJS]
- 数据库：[PostgreSQL / SQLite]
- ORM：[SQLAlchemy / TypeORM / Prisma]
- 认证：JWT
- 文档：OpenAPI/Swagger

## 项目结构（严格遵循）
project-root/
├── src/
│   ├── api/              # API 路由定义
│   │   ├── v1/           # API 版本
│   │   │   ├── routes/   # 路由模块
│   │   │   └── __init__.py / index.ts
│   │   └── dependencies/ # 依赖注入
│   ├── core/             # 核心配置
│   │   ├── config.py/ts  # 环境变量配置
│   │   ├── security.py/ts# 安全相关工具
│   │   └── exceptions.py # 自定义异常
│   ├── models/           # 数据库模型
│   ├── schemas/          # Pydantic/DTO 模型
│   ├── services/         # 业务逻辑层
│   ├── repositories/     # 数据访问层
│   ├── middleware/       # 中间件
│   └── utils/            # 工具函数
├── migrations/           # 数据库迁移
├── tests/                # 测试
│   ├── unit/
│   ├── integration/
│   └── conftest.py / setup.ts
├── .env.example          # 环境变量模板
├── .gitignore
├── requirements.txt / package.json
└── README.md

## 约束
- 禁止硬编码任何配置，全部通过 .env 管理
- .env 文件必须加入 .gitignore
- 每个模块独立，单一职责
- 代码中的敏感信息禁止出现在代码中
```

---

## 二、架构设计 Prompt（规划先行）

```
我需要为 [项目描述] 设计后端架构。

# 请先执行以下步骤（不要直接写代码）

## 第一步：需求分析
1. 研究并分析需求
2. 提出至少 5 个澄清问题
3. 识别隐含需求

## 第二步：架构方案
提供 2-3 个架构方案，每个方案包含：
- 架构图（ASCII 或 Mermaid）
- 技术栈
- 优势 / 劣势 / 风险

## 第三步：等待我选择
等我确认方案后再进入实施阶段
```

---

## 三、文件治理 Prompt

```
系统规则：请主动监控代码复杂度。
当任一文件超过 250 行，或包含多个独立逻辑块时，
请主动提醒我：
'检测到文件复杂度较高，是否需要将其拆分为子模块？'

拆分规则：
- 路由定义与业务逻辑分离
- 数据模型与数据访问分离
- 公共工具提取到 utils/
- 配置集中到 core/config
```

---

## 四、推荐技术栈组合

| 方案 | 技术栈 | 适合场景 |
|------|--------|---------|
| **Python 学生推荐** | FastAPI + SQLAlchemy + Alembic + SQLite | 学习后端、快速迭代 |
| **Python 生产** | FastAPI + SQLAlchemy + Alembic + PostgreSQL + Docker | 正式项目 |
| **Node.js 推荐** | NestJS + Prisma + PostgreSQL + Docker | TypeScript 全栈 |
| **快速原型** | Lovable/Bolt（前端）+ Supabase（BaaS） | 无后端经验、快速 MVP |

---

## 五、AI 编程工具对比（后端场景）

| 工具 | 后端能力 | 价格 | 说明 |
|------|---------|------|------|
| **Cursor** | 最强 | 免费/$20月 | 完整项目上下文理解 |
| **Claude Code** | 极强 | API 计费 | 擅长大型代码库和重构 |
| **Bolt.new** | 中等 | 免费/$20月 | 适合 MVP 但难维护 |
| **Lovable** | 中等 | 免费/$20月 | Supabase 集成好 |
| **GitHub Copilot** | 辅助 | 免费(学生)/$10月 | 适合小函数生成 |

---

## 六、部署方案推荐（学生/独立开发者）

| 场景 | 推荐方案 | 价格 |
|------|---------|------|
| 学生项目 | Railway / Render | 免费额度 |
| API 服务 | Fly.io / Railway | 按用量 |
| 全栈应用 | Vercel（前端）+ Railway（后端）| 免费起步 |
| 数据库 | Supabase / Neon | 免费额度 |
| 自托管 | VPS + Docker Compose | $5-10/月 |
