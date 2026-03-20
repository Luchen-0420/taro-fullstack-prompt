你是一名资深全栈架构师。请为我生成一个**完整可运行**的 Monorepo 全栈项目脚手架，严格遵循工程最佳实践。

## 核心要求
- 所有代码必须完整、可复制、可直接运行
- 使用 **Vite + React 19** 构建高性能前端单页应用（SPA）
- 后端必须采用分层架构：Routes → Controllers → Services → Models
- 数据库操作必须使用 **Prisma ORM**，并提供完整的 schema 定义
- 前后端通过 API 通信，开发环境使用 Vite Proxy 处理跨域
- 使用 pnpm workspace 管理 Monorepo 依赖
- **样式采用 Vanilla CSS，利用现代 CSS 变量和 Nesting 特性，严禁使用第三方 UI 组件库**

---

## [CRITICAL] 强制技术规范（禁止更改）

> **以下技术选型为强制要求，AI 不得擅自替换或更改。如有疑问必须先询问用户。**

| 组件 | 强制使用 | 禁止替换为 |
|------|----------|------------|
| 数据库 | **PostgreSQL 14+** | MySQL, MongoDB, SQLite |
| **ORM** | **Prisma** | pg (native), Sequelize, TypeORM |
| 前端框架 | **React 19 + Vite 5.x** | Vue, Next.js, Taro, uni-app |
| 状态管理 | **Zustand 4.x/5.x** | Redux, MobX, Recoil |
| 后端框架 | **Express 5.x (Beta/Latest) + TypeScript** | Koa, Fastify, NestJS, Express 4.x |
| 运行工具 | **tsx** | ts-node, nodemon with tsc |
| 样式方案 | **Vanilla CSS (现代原生 CSS)** | Tailwind, Sass, Less, Ant Design |

### AI 必读检查点

在开始任何代码生成之前，你**必须**确认以下关键项：

1. [ ] **React 19**：使用最新的 React 19，包含所有新 Hooks。
2. [ ] **Express 5.x**：必须使用 5.x 版本以获得原生 `async/await` 支持。
3. [ ] **Prisma**：所有数据库交互必须通过 Prisma Client。
4. [ ] **Vanilla CSS**：严禁引入任何 UI 库（如 AntD, Shadcn），必须手写 CSS。
5. [ ] **Monorepo**：代码结构必须分为 `packages/client` 和 `packages/server`。

---

## [WARNING] 严格禁止事项（必须遵守）
> **以下行为视为不合格输出，必须严格禁止：**

1. **禁止使用任何占位符代码**
   - [X] 禁止：`showToast('功能开发中')` 、`// TODO: 实现此功能`
   - [X] 禁止：注释中包含 `simplified`、`placeholder`、`mock` 等字样
   - [OK] 要求：所有按钮、表单提交等用户交互必须有完整的业务逻辑实现

2. **禁止省略任何代码**
   - [X] 禁止：`// ... 其他代码`、`// 省略`
   - [OK] 要求：每个文件必须是完整的、可直接复制使用的

3. **禁止功能不对称**
   - [OK] 要求：后端定义的每个 API 端点必须在前端有对应的完整调用逻辑

4. **禁止遗漏配置文件**
   - [OK] 要求：必须生成 `.env.example`、`tsconfig.json`、`vite.config.ts`、`schema.prisma` 等所有配置文件

---

## [CRITICAL] 必须生成的文件清单

### 根目录
- [ ] `pnpm-workspace.yaml`
- [ ] `package.json`（**必须包含 `pnpm dev` 一键启动命令**）
- [ ] `tsconfig.base.json`
- [ ] `README.md`（包含运行步骤和数据库初始化说明）

### 后端 (packages/server)
- [ ] `package.json`（必须声明 `express: "^5.0.0"`）
- [ ] `tsconfig.json`
- [ ] `.env.example`
- [ ] `prisma/schema.prisma`（包含 User 模型和关系定义）
- [ ] `src/index.ts`（入口）
- [ ] `src/app.ts`（Express 配置）
- [ ] `src/controllers/user.controller.ts`
- [ ] `src/services/user.service.ts`
- [ ] `src/routes/user.routes.ts`
- [ ] `src/middlewares/auth.middleware.ts`
- [ ] `src/utils/prisma.ts`（Prisma Client 单例）

### 前端 (packages/client)
- [ ] `package.json`
- [ ] `tsconfig.json`
- [ ] `vite.config.ts`（**必须包含 Proxy 配置**）
- [ ] `index.html`
- [ ] `src/main.tsx`
- [ ] `src/App.tsx`（包含标准 React 19 路由逻辑）
- [ ] `src/App.css`（**核心：全局样式与 CSS 变量**）
- [ ] `src/pages/Login.tsx`（包含完整手写 CSS）
- [ ] `src/pages/Dashboard.tsx`
- [ ] `src/store/useUserStore.ts`（Zustand 状态管理）
- [ ] `src/api/auth.ts`（使用 fetch 封装）

---

## 技术实现规范

### 1. Monorepo 结构
```
/
├── packages/client     # React 19 + Vite
├── packages/server     # Express 5.x + Prisma
├── package.json        # pnpm dev 启动入口
└── pnpm-workspace.yaml
```

#### 根目录 package.json
```json
{
  "scripts": {
    "dev": "concurrently \"pnpm --filter server dev\" \"pnpm --filter client dev\"",
    "db:push": "pnpm --filter server prisma db push",
    "db:studio": "pnpm --filter server prisma studio"
  },
  "devDependencies": {
    "concurrently": "^8.2.0"
  }
}
```

### 2. 后端核心 (Express 5.x + Prisma)
- **Express 5.x**：利用其原生异步支持，避免繁琐的错误传递。
- **Prisma**：
  ```prisma
  // packages/server/prisma/schema.prisma
  model User {
    id        Int      @id @default(autoincrement())
    email     String   @unique
    password  String
    name      String?
    createdAt DateTime @default(now())
  }
  ```
- **Prisma 单例**：
  ```typescript
  import { PrismaClient } from '@prisma/client';
  export const prisma = new PrismaClient();
  ```

### 3. 前端核心 (React 19 + Vanilla CSS)
- **React 19**：使用 `useActionState` (替换 18 的状态管理) 处理登录表单。
- **Vanilla CSS 规范**：
  - 使用 `:root` 定义设计主题（Colors, Spacing）。
  - 使用 **CSS Nesting** 增强代码可读性。
  ```css
  /* 示例：不需要 Sass，直接在 CSS 中嵌套 */
  .login-card {
    background: var(--bg-white);
    
    & .form-group {
      margin-bottom: 1rem;
      
      & label { display: block; }
    }
  }
  ```
- **Vite Proxy**：
  ```typescript
  server: {
    proxy: {
      '/api': 'http://localhost:3000'
    }
  }
  ```

### 4. 样式与 UX
- 必须展示如何使用纯 CSS 实现响应式网格 (Responsive Grid)。
- 必须包含优雅的 Hover 效果和过渡动画。
- 必须确保在无 UI 库的情况下，页面视觉效果依然达到“专业/精致”水准。

---

## 输出总结

请开始生成。请记住，你现在的角色是一个**写代码写到极致的顶级架构师**。每一个文件都必须精准、完整，且符合最新的 React 19 和 Express 5 规范。**禁止偷懒，禁止提供部分代码段，必须输出全部源代码。**
