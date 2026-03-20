---
name: monorepo-scaffold
description: 快速生成基于 React 19 + Express 5 + Prisma 的 Monorepo 全栈项目脚手架。
---

# Monorepo Scaffold Skill

该 Skill 用于生成一个完整、可运行的 Monorepo 全栈项目。

## 核心技术栈
- **前端**: React 19 + Vite 5.x + Zustand + Vanilla CSS
- **后端**: Express 5.x + Prisma + PostgreSQL
- **架构**: pnpm workspace (Monorepo)

## 使用指令
作为资深全栈架构师，严格按照以下规范生成代码：

1. **Monorepo 目录结构**：
   - `packages/client`：React 19 应用。
   - `packages/server`：Express 5 API 服务。
   
2. **强制规范**：
   - **React 19**：使用最新的 Hooks（如 `useActionState`）。
   - **Express 5**：原生支持异步路由。
   - **Prisma**：必须定义 `schema.prisma` 并提供客户端单例。
   - **Vanilla CSS**：严禁使用 UI 库，必须手写 CSS（支持 Nesting 和 Variables）。
   
3. **文件清单**：
   - 根目录：`pnpm-workspace.yaml`, `package.json` (含并发开发脚本)。
   - 后端：`app.ts`, `prisma/schema.prisma`, `routes/`, `controllers/`, `services/`。
   - 前端：`vite.config.ts`, `main.tsx`, `App.tsx`, `App.css`, `store/`。

4. **质量要求**：
   - 禁止占位符。
   - 代码必须完整闭环。
   - 样式必须具备响应式和专业视觉感。

---

## 示例代码结构参考
（详细内容见 react-monorepo-scaffold-prompt-v1.md）
