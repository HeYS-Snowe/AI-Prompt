# 开发环境配置指南

> 适用场景：学生独立开发者，从零搭建开发环境
> 核心原则：环境一致性、配置外置、版本控制先行
> 参考来源：Addy Osmani 博客、社区最佳实践

---

## 一、环境搭建检查清单

### 基础工具安装

```
[ ] Git — 版本控制（https://git-scm.com）
[ ] Node.js 20+ (LTS) — 前端 + 后端
[ ] Python 3.11+ — 后端（如选 Python）
[ ] VS Code / Cursor — 编辑器
[ ] Docker Desktop — 容器化（可选，推荐安装）
[ ] 终端 — Windows Terminal / iTerm2
```

### Git 初始化（项目第一步）

```bash
# 初始化
git init
git remote add origin [仓库地址]

# .gitignore（必须在第一次 commit 前创建）
node_modules/
.env
.env.local
*.pyc
__pycache__/
dist/
.next/
.DS_Store
*.log
```

### Git 分支策略（学生推荐）

```
main          — 稳定版本，随时可部署
├── dev       — 日常开发分支
├── feature/* — 功能分支（如 feature/user-auth）
└── fix/*     — 修复分支（如 fix/login-bug）

规则：
- main 分支永远可运行
- 功能开发在 feature/* 分支进行
- 完成后 merge 到 dev，测试通过后 merge 到 main
- 每次合并前做 code review（即使是自己 review）
```

### Git Commit 规范

```
feat: 添加用户注册功能
fix: 修复登录页面密码验证错误
docs: 更新 API 文档
style: 调整按钮样式（不影响逻辑）
refactor: 重构数据库连接池
test: 添加用户认证单元测试
chore: 更新依赖版本

格式：<type>: <description>
- type 必须是以上之一
- description 用中文或英文，简洁明了
- 每次功能完成后立即 commit，不要攒一大堆
```

---

## 二、环境变量管理

### .env 文件规范

```bash
# .env.example（提交到 Git 的模板）

# 应用配置
APP_NAME=MyApp
APP_ENV=development
APP_PORT=3000
APP_SECRET=your-secret-key-here

# 数据库
DATABASE_URL=postgresql://user:password@localhost:5432/dbname
# 或 SQLite: DATABASE_URL=sqlite:///./dev.db

# JWT
JWT_SECRET=your-jwt-secret-here
JWT_ALGORITHM=HS256
JWT_ACCESS_TOKEN_EXPIRE_MINUTES=15
JWT_REFRESH_TOKEN_EXPIRE_DAYS=7

# 第三方服务（如需）
# SUPABASE_URL=
# SUPABASE_ANON_KEY=
# REDIS_URL=
```

### 核心规则

```
1. .env 永远不提交到 Git（加入 .gitignore）
2. .env.example 必须提交到 Git（提供模板）
3. 所有密钥通过环境变量加载，禁止硬编码
4. 生产环境的密钥与开发环境不同
5. 密钥生成：python -c "import secrets; print(secrets.token_urlsafe(32))"
```

---

## 三、项目配置文件模板

### Node.js 项目

```
package.json — 依赖管理
tsconfig.json — TypeScript 配置
.eslintrc.js — 代码规范
.prettierrc — 格式化配置
.env.example — 环境变量模板
.gitignore — Git 忽略规则
```

### Python 项目

```
requirements.txt — 依赖管理（或 pyproject.toml）
alembic.ini — 数据库迁移配置
.env.example — 环境变量模板
.gitignore — Git 忽略规则
```

### Docker 配置

```dockerfile
# Dockerfile 示例（多阶段构建）
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
RUN addgroup -g 1001 appgroup && adduser -u 1001 -G appgroup -s /bin/sh -D appuser
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./
USER appuser
EXPOSE 3000
HEALTHCHECK --interval=30s CMD wget -q --spider http://localhost:3000/health || exit 1
CMD ["node", "dist/main.js"]
```

```yaml
# docker-compose.yml 示例
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    env_file: .env
    depends_on:
      - db
    volumes:
      - ./src:/app/src  # 开发时挂载源码
  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: ${DB_NAME}
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
volumes:
  pgdata:
```

---

## 四、编辑器推荐配置

### Cursor / VS Code 推荐扩展

```
前端：
- ESLint
- Prettier
- Tailwind CSS IntelliSense
- Auto Rename Tag

后端（Python）：
- Python
- Pylance
- Python Debugger

后端（Node.js）：
- ESLint
- TypeScript

通用：
- GitLens
- Docker
- REST Client（测试 API）
- Thunder Client（API 测试）
```

### 推荐设置

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.tabSize": 2,
  "files.autoSave": "afterDelay",
  "terminal.integrated.defaultProfile.windows": "Git Bash"
}
```
