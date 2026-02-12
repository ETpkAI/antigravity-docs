# Antigravity 技术栈偏好 (Tech Stack Presets)

为了最大化开发效率和代码质量，Antigravity 推荐以下经过验证的现代化技术栈组合。

## 1. 前端开发 (Frontend)

*   **核心框架**:
    *   **React**: 首选生态最丰富的 UI 库。
    *   **Next.js**: 服务端渲染 (SSR) 和静态生成 (SSG) 的首选框架。
    *   **Vite**: 纯客户端应用 (SPA) 的构建工具，极速开发体验。
*   **语言**:
    *   **TypeScript**: **强制使用**。不推荐纯 JavaScript，除非是极简单的脚本或原型。
*   **样式与 UI**:
    *   **Tailwind CSS**: 实用优先 (Utility-first) 的 CSS 框架，快速构建界面。
    *   **shadcn/ui** (或类似 Headless UI): 高质量、可定制的组件库基础。
    *   **CSS Modules/Styled Components**: 备选方案，仅在特定需求下使用。
*   **状态管理**:
    *   **React Query (TanStack Query)**: 服务端状态管理首选。
    *   **Zustand**: 轻量级客户端全局状态管理。
    *   **Redux Toolkit**: 仅用于极复杂的大型应用。
*   **表单管理**: **React Hook Form** + **Zod** (Schema 校验)。

## 2. 后端开发 (Backend)

### 2.1 Python (AI/数据密集型应用首选)
*   **框架**: **FastAPI** (高性能、原生异步、自动文档)。
*   **ORM**: **SQLAlchemy (Async)** 或 **Tortoise ORM**。
*   **Linter/Formatter**: **Ruff** (极速全能工具) + **Black**。

### 2.2 Node.js (全栈/IO密集型应用首选)
*   **框架**:
    *   **NestJS**: 企业级、高度模块化的框架 (推荐)。
    *   **Express**: 简单微服务或快速原型。
*   **ORM**: **Prisma** (类型安全) 或 **TypeORM**。
*   **Runtime**: **Node.js LTS** 或 **Bun** (实验性)。

### 2.3 Go (高性能微服务)
*   **框架**: **Gin** 或 **Echo**。
*   **ORM**: **GORM** 或 **Ent**。

## 3. 数据库与存储 (Database & Storage)

*   **关系型数据库**: **PostgreSQL** (首选)。
*   **NoSQL**: **MongoDB** (文档型)。
*   **缓存/消息队列**: **Redis**。
*   **搜索引擎**: **Elasticsearch** 或 **Meilisearch**。

## 4. DevOps 与工具链 (DevOps & Tools)

*   **容器化**: **Docker** + **Docker Compose**。
*   **CI/CD**: **GitHub Actions** 或 **GitLab CI**。
*   **包管理**:
    *   JS/TS: **pnpm** (速度快、磁盘占用少) > **yarn** > **npm**。
    *   Python: **Poetry** 或 **uv** (极速)。
*   **API 文档**: **OpenAPI (Swagger)** (FastAPI/NestJS 自带)。

## 5. 开发工具推荐 (IDE)

*   **VS Code**: 首选轻量级编辑器，由 Microsoft 维护。
*   **JetBrains 系列**: IntelliJ IDEA, PyCharm, WebStorm (更强大的静态分析)。
