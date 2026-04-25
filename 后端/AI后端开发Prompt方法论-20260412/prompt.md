# AI 后端开发 Prompt 方法论

> 适用平台：所有 AI 编程工具
> 核心原则：前端决定后端、Prompt 即接口、规划先行
> 技术栈偏好：Python (FastAPI/Flask) / Node.js (Express/NestJS)、PostgreSQL/SQLite
> 参考来源：火山引擎 Vibe Coding 实践、Auth0 Blog、Cursor Blog、LLMBase Prompt Library

---

## 一、三大黄金法则

| 法则 | 说明 | 行动 |
|------|------|------|
| **Git 是底裤** | 写第一行代码前先初始化 Git，这是唯一的后悔药 | `git init` + 远程仓库，每次功能完成后 commit |
| **前端决定后端** | 先画出界面，用 Mock 数据跑通交互，UI 决定数据库怎么建 | 先定义 JSON 数据结构，再建库 |
| **治理大文件** | AI 喜欢生成巨型文件，必须强制拆分 | 任何文件超过 250 行就提醒拆分 |

---

## 二、API 设计 Prompt 模板

```
# 背景
我正在开发 [项目名称]，这是一个 [项目类型] 项目。
技术栈：[FastAPI/Flask/Express/NestJS] + [PostgreSQL/SQLite]

# 目标
设计 RESTful API 用于 [资源名称]

# 要求
## 端点设计
- GET /api/v1/[资源] — 列表查询（支持分页、排序、筛选）
- GET /api/v1/[资源]/:id — 详情查询
- POST /api/v1/[资源] — 创建
- PUT /api/v1/[资源]/:id — 全量更新
- PATCH /api/v1/[资源]/:id — 部分更新
- DELETE /api/v1/[资源]/:id — 删除

## 响应格式
- 统一 JSON：{ "data": {...}, "meta": {...}, "error": null }
- 成功：200/201/204
- 客户端错误：400/401/403/404/409/422
- 错误格式：{ "error": { "code": "ERROR_CODE", "message": "描述", "details": {} } }

## 安全要求
- 所有端点需要认证（JWT Bearer Token）
- 输入验证（类型、长度、格式）
- 参数化查询（防 SQL 注入）
- CORS 仅允许可信来源
```

### API 设计规范（写入 Prompt 的规则）

```
1. URL 使用 kebab-case（/user-profiles），JSON 字段统一使用 snake_case 或 camelCase
2. 集合端点使用复数名词（/users 而非 /user）
3. 嵌套资源不超过两层
4. 分页返回总数：{ data: [], meta: { total, page, per_page, total_pages } }
5. 201 Created 返回创建的资源
6. 204 No Content 用于删除操作
7. 使用 OpenAPI/Swagger 自动生成文档
8. 版本化从第一天开始（/api/v1/）
```

### FastAPI 端点生成 Prompt

```
使用 FastAPI + SQLAlchemy + Pydantic 实现以下 API 端点：

[贴入上面设计的端点列表]

要求：
- 使用 APIRouter 组织路由
- Pydantic 模型区分 Create/Update/Response Schema
- async def 异步处理
- 依赖注入方式处理数据库会话和认证
- 统一异常处理
- 所有端点有完整的类型注解和 docstring
```

### NestJS 端点生成 Prompt

```
使用 NestJS + TypeORM + class-validator 实现 [资源] CRUD API：

要求：
- Controller / Service / Module 分层
- DTO 使用 class-validator 装饰器验证
- 使用拦截器统一响应格式
- 使用守卫（Guard）处理 JWT 认证
- Swagger 装饰器自动生成文档
```

---

## 三、数据库建模 Prompt 方法

### 前端优先的数据契约法（推荐）

```
步骤 1：先让 AI 定义 JSON 数据结构
"请先帮我定义这个页面涉及的 JSON 数据结构（Schema），
包含哪些字段和类型，然后再写任何代码"

步骤 2：用 Mock 数据跑通前端
"基于以上 Schema，生成 Mock Data 并构建前端页面"

步骤 3：将 Mock Data 映射为数据库 Schema
"将上面定义的 Data Contract 映射为 PostgreSQL 表结构，
确保字段一一对应"
```

### 数据库设计 Prompt 模板

```
# 业务实体
- User: id, email, username, password_hash, role, created_at, updated_at
- [Entity2]: [属性列表]

# 关系
- User -> [Entity2]: 一对多

# 技术要求
- 数据库：PostgreSQL（生产）/ SQLite（开发）
- 使用 SQLAlchemy ORM 或 Prisma
- 所有表包含 id、created_at、updated_at
- 软删除使用 deleted_at 字段

# 强制约束（不可违反）
- 禁止使用 DROP TABLE 或 TRUNCATE
- 所有外键必须设置 ON DELETE 策略
- password 字段必须命名为 password_hash
- email 字段添加 UNIQUE 约束
- 金额字段使用 Decimal/NUMERIC 而非 Float
- 时间字段统一使用 UTC（TIMESTAMP WITH TIME ZONE）

# 输出要求
1. 生成 ORM 模型文件
2. 生成迁移脚本
3. 生成 seed 数据脚本（使用 Faker 库）
4. 列出所有索引及添加理由
```

---

## 四、认证/权限 Prompt 模板

### JWT 认证系统

```
# 需求
实现基于 JWT 的用户认证系统：

## 注册（POST /api/v1/auth/register）
- 接收：email, username, password
- 验证：邮箱格式、密码强度（>= 8位，含数字和字母）
- 密码使用 bcrypt 哈希（cost factor 12）

## 登录（POST /api/v1/auth/login）
- 登录失败 5 次后锁定账户 15 分钟
- 返回 access_token（15分钟）和 refresh_token（7天）

## 刷新令牌（POST /api/v1/auth/refresh）
- 实现 refresh token rotation（每次使用后旧 token 失效）

## 安全要求（严格遵守）
- JWT 算法明确指定，禁止 alg: none
- token 存储在 HttpOnly + Secure + SameSite=Strict cookie
- 验证 JWT 的 iss 和 aud
- 敏感路由添加速率限制
```

### RBAC 权限控制

```
实现基于角色的访问控制（RBAC）：

## 角色定义
- admin：全部权限
- user：操作自己的资源
- guest：只读权限

## 安全规则
- 用户身份从 token 中提取，绝不能从请求参数中获取
- 每个受保护的路由都必须同时检查认证和授权
- 资源所有权检查：确保用户只能操作自己的资源
```

---

## 五、增量式开发工作流

### 五阶段开发法

```
阶段 0：业务梳理（PM 角色）
├── 定义 Who/What/Why
├── 列出核心功能点
├── 定义 JSON 数据契约（Schema）
└── 初始化 Git + 技术栈锁定
    ✅ 成功标准：需求文档 + 数据结构定义

阶段 1：前端优先 + UI 交互
├── 用 Mock Data 跑通界面
├── 实现所有状态（Loading/Error/Empty）
└── 定义前后端数据契约
    ✅ 成功标准：界面可交互，Mock Data 完整

阶段 2：后端服务实现
├── 将数据契约映射为数据库 Schema
├── 生成迁移脚本 + seed 数据
├── API 空壳先行（返回 Mock JSON）
└── 逐步填充真实业务逻辑
    ✅ 成功标准：API 可调通，数据库可读写

阶段 3：前后端集成
├── 替换 Mock Data 为 API 调用
├── 统一错误处理
└── 认证流程打通
    ✅ 成功标准：完整业务流程可用

阶段 4：测试与部署
├── 单元测试（AI 主导 90%）
├── 集成测试（AI 主导 60%）
└── 部署配置
    ✅ 成功标准：测试覆盖率 > 80%，可部署
```

### 大任务拆分示例（用户认证系统）

```
阶段 1：基础设施（1-2 天）- 用户表 + CRUD
阶段 2：认证逻辑（2-3 天）- 密码哈希 + JWT + 登录端点
阶段 3：授权中间件（1 天）- Token 验证 + 角色检查
阶段 4：高级功能（2-3 天）- 忘记密码 + 邮箱验证 + Token 刷新
阶段 5：测试和文档（1-2 天）- 覆盖率 > 80%
```

---

## 六、重新提示策略

当 AI 输出不理想时，按以下顺序细化：

```
第 1 轮：模糊描述
"实现用户登录功能"

第 2 轮：添加具体要求
"使用 JWT、bcrypt、登录失败锁定、统一错误格式"

第 3 轮：提供参考示例
"参考项目中 signup 的实现模式，使用现有 AuthService 类"

第 3 轮仍不理想 → 明确不想要的内容：
"重新实现，但：不要用 Session / 不要明文密码 / 不要返回堆栈"
```

---

## 七、实用 Prompt 速查

### Bug 修复

```
# Bug 描述
[清晰描述 bug 现象]

# 复现步骤
1. [步骤]  2. [步骤]  3. [观察到的错误]

# 相关上下文
- 错误日志：[粘贴完整日志]
- 文件：[路径]
- 环境：[开发/测试/生产]

# 请
1. 分析可能的根本原因（至少 3 个）
2. 提供诊断步骤
3. 等待我确认后再修复
```

### 测试生成

```
为以下代码生成测试：

[粘贴代码]

覆盖场景：
- 正常路径（Happy Path）
- 边界条件（空值、零、最大值、特殊字符）
- 异常路径（错误输入、权限不足、资源不存在）

使用 [pytest / Jest / Vitest]
```

### 部署配置

```
为以下应用创建 Docker 配置：

应用类型：[FastAPI / Express / NestJS]
端口：[端口号]

要求：
- Dockerfile 多阶段构建
- docker-compose.yml 包含应用 + PostgreSQL
- 非 root 用户运行
- 健康检查
- .env 通过 env_file 注入
- 数据持久化（volume）
```

---

## 八、技术栈推荐（学生/独立开发者）

### Python 方案（推荐学生）

```
FastAPI + SQLAlchemy + Alembic + PostgreSQL/SQLite + Docker
```

### Node.js 方案

```
NestJS + Prisma + PostgreSQL/SQLite + Docker
```

### 快速原型方案（无后端经验）

```
Lovable/Bolt（前端）+ Supabase（BaaS）
- PostgreSQL + Auth + Storage 一站式
- 内置 Row Level Security（RLS）
```

---

## 九、参考来源

| 来源 | 核心贡献 |
|------|---------|
| 火山引擎 - Vibe Coding 工程化实践 | 分层解耦、前端决定后端 |
| Auth0 Blog - AI 安全代码生成 | 认证安全 Checklist |
| Cursor Blog - Prompt Design | 规划先行方法论 |
| LLMBase Prompt Library | 后端架构 Agent Prompt |
| Medium - Backend with AI | API/数据库 Prompt 模板 |
