# 部署与维护指南

> 适用场景：学生独立开发者，将项目从本地部署到线上
> 核心原则：先跑通再优化、免费额度起步、自动化优先
> 参考来源：Vercel/Railway/Render 官方文档、社区实践

---

## 一、部署方案对比与选择

| 方案 | 适合场景 | 价格 | 学习成本 |
|------|---------|------|---------|
| **Vercel** | 前端（Next.js/React/Vue） | 免费额度充足 | 低 |
| **Railway** | 后端 API + 数据库 | 免费额度 $5/月 | 低 |
| **Render** | 后端 API + 定时任务 | 免费层（冷启动） | 低 |
| **Fly.io** | Docker 化应用 | 免费额度 | 中 |
| **Supabase** | 数据库 + Auth + Storage | 免费层 | 低 |
| **Neon** | Serverless PostgreSQL | 免费层 | 低 |
| **VPS + Docker** | 完全控制 | $5-10/月 | 高 |

### 推荐组合

```
入门推荐：Vercel（前端）+ Supabase（数据库+Auth）
进阶推荐：Vercel（前端）+ Railway（后端）+ Neon（数据库）
全栈一体：Railway（前后端+数据库）
自托管：VPS + Docker Compose
```

---

## 二、Vercel 前端部署流程

```bash
# 1. 安装 Vercel CLI
npm i -g vercel

# 2. 登录
vercel login

# 3. 部署（项目根目录执行）
vercel          # 预览部署
vercel --prod   # 生产部署

# 4. 配置环境变量（在 Vercel Dashboard 中设置）
# Settings → Environment Variables
# 添加所有 .env 中的变量
```

### 自动部署

```
1. 将代码推送到 GitHub
2. Vercel 自动检测并部署
3. PR 自动生成预览链接
4. 合并到 main 自动部署到生产
```

---

## 三、Railway 后端部署流程

```bash
# 1. 安装 CLI
npm i -g @railway/cli

# 2. 登录
railway login

# 3. 初始化项目
railway init

# 4. 添加 PostgreSQL
railway add --database postgres

# 5. 部署
railway up

# 6. 查看日志
railway logs

# 7. 环境变量
railway variables  # 查看
# 在 Dashboard 中设置环境变量
```

---

## 四、GitHub Actions CI/CD 基础

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, dev]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm run lint
      - run: npm test
      - run: npm run build
```

### 核心原则

```
1. 每次 push 到 dev/main 自动运行 lint + test + build
2. PR 必须通过 CI 才能合并
3. 测试失败不部署
4. 环境变量通过 GitHub Secrets 管理（不写在代码中）
```

---

## 五、域名与 HTTPS

```
1. 购买域名：Cloudflare / Namesilo（便宜）
2. DNS 解析：指向 Vercel/Railway 提供的地址
3. HTTPS：Vercel/Railway 自动提供免费 SSL 证书
4. 无需手动配置证书
```

---

## 六、监控与运维基础

### 健康检查端点

```
# 后端必须提供
GET /health → { "status": "ok", "timestamp": "..." }
```

### 日志管理

```
1. 关键操作记录日志（登录、支付、错误）
2. 日志中排除敏感信息（token、密码、邮箱）
3. 使用平台提供的日志查看器
4. 生产环境设置 NODE_ENV=production
```

### 常见运维操作

```
- 查看日志：railway logs / vercel logs
- 重启服务：railway run <command>
- 回滚部署：vercel rollback / railway rollback
- 扩容：在 Dashboard 中调整资源
- 数据库备份：定期导出 SQL dump
```

---

## 七、部署检查清单

### 上线前

```
[ ] 所有环境变量已设置（.env 不再需要）
[ ] 数据库迁移已运行
[ ] CORS 配置为生产域名
[ ] HTTPS 已启用
[ ] 健康检查端点可访问
[ ] 错误页面已配置（404/500）
[ ] 静态资源已优化（压缩/CDN）
```

### 上线后

```
[ ] 注册/登录流程正常
[ ] API 响应正常
[ ] 移动端显示正常
[ ] 加载速度可接受（< 3s）
[ ] 日志无异常错误
```

---

## 八、常见部署问题

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 构建失败 | 依赖版本不一致 | 锁定版本（package-lock.json） |
| 环境变量缺失 | 未在平台设置 | 检查 Dashboard 环境变量 |
| 数据库连接失败 | URL 配置错误 | 检查 DATABASE_URL 格式 |
| CORS 错误 | 未配置允许来源 | 设置正确的 CORS origin |
| 冷启动慢 | 免费层休眠 | 升级方案或设置健康检查保活 |
| 502 错误 | 应用崩溃 | 查看日志定位原因 |
