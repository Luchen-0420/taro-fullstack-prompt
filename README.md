# Full-Stack Monorepo Prompt & Skill 🚀

> 📢 **让零基础小白也能生成专业级的全栈项目。本项目提供多套高性能提示词（Prompt）与 AI 技能（Skill），助你快速迈出全栈开发的第一步。**

---

## 🌟 选择你的脚手架版本

本项目目前提供两个核心版本，分别针对不同的业务场景：

### 1️⃣ 经典跨端版 (Taro + React 18)
- **特点**：一套代码同时支持 **H5 网页** 和 **微信小程序**。
- **技术栈**：Taro 3.6 + React 18 + Express 4 + PostgreSQL (Native pg)。
- **提示词**：[taro-monorepo-scaffold-prompt-v1.md](./taro-monorepo-scaffold-prompt-v1.md)

### 2️⃣ 现代 Web 增强版 (React 19 + Express 5) —— **New!**
- **特点**：极致的开发效率与前瞻性，适合 **Web 侧、SaaS、管理后台**。
- **技术栈**：React 19 + Vite 5 + **Prisma ORM** + Express 5 + Vanilla CSS。
- **提示词**：[react-monorepo-scaffold-prompt-v1.md](./react-monorepo-scaffold-prompt-v1.md)
- **AI Skill**：已集成到 `.agents/skills/monorepo-scaffold`，可供各种 AI Agent 直接调用。

---

## 📊 技术栈对比

| 组件 | 经典跨端版 (Taro) | 现代 Web 版 (React 19) |
|------|-------------------|----------------------|
| **前端框架** | Taro (React 18) | **React 19 + Vite 5** |
| **小程序支持** | ✅ 微信小程序 | ❌ 仅限 Web |
| **后端框架** | Express 4.x | **Express 5.x (Beta)** |
| **数据库 ORM** | pg (Native) | **Prisma (类型安全)** |
| **样式方案** | Sass + NutUI | **Vanilla CSS (现代原生)** |
| **包管理** | pnpm workspace | pnpm workspace |

---

## 🛠️ 环境准备

在开始之前，请确保安装以下工具：

1. **Node.js** (v18.0+)
2. **pnpm** (`npm install -g pnpm`)
3. **PostgreSQL** (数据库服务)
4. **Git** (可选)

---

## 🚀 如何使用

### 方式 A：使用提示词 (Prompt)
1. 打开对应版本的 `.md` 文件（如 `react-monorepo-scaffold-prompt-v1.md`）。
2. 复制全部内容。
3. 粘贴给 **Claude / GPT-4 / Gemini** 等 AI。
4. AI 将为您生成完整的 Monorepo 项目结构。

### 方式 B：使用 AI Skill (推荐)
如果您正在使用支持本地 Skill 的 AI 助手，只需直接下令：
> “使用项目中的 **monorepo-scaffold** 技能帮我初始化项目。”

---

## 🏃 运行项目 (现代 Web 版)

如果是使用带有 **Prisma** 的现代版，流程如下：

### 1. 数据库初始化
```bash
# 进入后端目录
cd packages/server
# 配置 .env 文件 (从 .env.example 复制并修改)
cp .env.example .env
# 使用 Prisma 自动创建表结构
npx prisma db push
```

### 2. 一键启动
在项目**根目录**运行：
```bash
pnpm dev
```
会自动并行启动前端 Vite 开发服务器和后端 Express 服务。

---

## 🔗 相关资源
- [Taro 官方文档](https://taro-docs.jd.com)
- [React 19 新特性说明](https://react.dev/blog/2024/12/05/react-19)
- [Prisma 官方文档](https://www.prisma.io/docs)

---

## 🙏 特别感谢
感谢**其来大哥**的项目启发，让我有了制作这份提示词的灵感。

---
有任何问题，欢迎提出 Issue 交流！✨
