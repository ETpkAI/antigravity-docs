# Antigravity 架构设计模式 (Architecture Patterns)

本规范定义了 Antigravity 项目的默认架构与目录结构，旨在统一开发范式，降低维护成本。

## 1. 核心设计原则 (Core Design Principles)

*   **分层架构 (Layered Architecture)**: 必须严格分层，禁止跨层调用。
    *   **Presentation Layer (表现层)**: 处理用户交互 (UI/API)。
    *   **Application/Service Layer (应用层)**: 处理业务逻辑。
    *   **Domain Layer (领域层)**: 核心业务实体与规则 (可选，适用于 DDD)。
    *   **Infrastructure/Data Layer (基础设施层)**: 数据访问、外部 API 调用。
*   **依赖倒置 (Dependency Inversion)**: 上层模块不应依赖底层模块，二者都应依赖抽象。
*   **单一职责 (Single Responsibility)**: 每个模块/类只做一件事。

## 2. 前端项目结构 (Frontend - React/Vue)

推荐采用 **基于功能 (Feature-based)** 或 **混合模式** 的目录结构。

```text
src/
├── assets/             # 静态资源 (Images, Fonts)
├── components/         # 通用 UI 组件 (Button, Input, Layout)
│   ├── common/         # 全局通用
│   └── layout/         # 布局组件
├── features/           # 业务功能模块 (User, Product, Cart) -> 核心推荐
│   ├── auth/           # 认证模块
│   │   ├── api/        # 该模块的 API 请求
│   │   ├── components/ # 该模块独有的组件
│   │   ├── hooks/      # 该模块的 Hooks
│   │   ├── stores/     # 状态管理
│   │   └── types/      # 类型定义
│   └── product/
├── hooks/              # 全局通用 Hooks
├── lib/                # 第三方库配置/工具 (Axios, Dayjs)
├── pages/              # 路由页面 (Next.js/Router)
├── services/           # 全局 API 服务 (如果未按 features 拆分)
├── stores/             # 全局状态管理 (Redux/Zustand)
├── styles/             # 全局样式
├── types/              # 全局类型定义
└── utils/              # 工具函数 (Helper functions)
```

## 3. 后端项目结构 (Backend - Python/Node.js)

### 3.1 Python (FastAPI/Flask)

```text
app/
├── api/                # API 路由定义 (Endpoints)
│   ├── v1/
│   │   ├── endpoints/
│   │   │   ├── user.py
│   │   │   └── item.py
│   │   └── api.py      # 路由汇总
│   └── deps.py         # 依赖注入 (Dependencies)
├── core/               # 核心配置 (Config, Security, Logging)
├── crud/               # 数据库 CRUD 操作 (Create, Read, Update, Delete)
├── db/                 # 数据库连接与会话
│   ├── base.py         # ORM Base
│   └── session.py
├── models/             # 数据库模型 (ORM Models)
├── schemas/            # Pydantic 数据模型 (DTOs)
├── services/           # 复杂业务逻辑 (Service Layer)
├── tests/              # 测试用例
└── main.py             # 应用程序入口
```

### 3.2 Node.js (NestJS/Express)

NestJS 自带模块化结构，Express 项目推荐仿 NestJS 结构：

```text
src/
├── modules/            # 业务模块 (User, Product)
│   ├── user/
│   │   ├── dto/        # 数据传输对象
│   │   ├── entities/   # 数据库实体
│   │   ├── user.controller.ts # 控制器
│   │   ├── user.service.ts    # 服务
│   │   └── user.module.ts     # 模块定义
├── common/             # 通用模块
│   ├── decorators/     # 装饰器
│   ├── filters/        # 异常过滤器
│   ├── guards/         # 守卫 (Auth)
│   ├── interceptors/   # 拦截器
│   └── pipes/          # 管道 (Validation)
├── config/             # 配置文件
├── database/           # 数据库迁移与配置
└── main.ts             # 应用程序入口
```

## 4. 目录命名规范

*   **文件夹**: 使用 `kebab-case` (如 `user-profile`) 或 `snake_case` (Python 推荐)。
*   **文件**:
    *   JS/TS/React: `camelCase` (如 `userProfile.ts`) 或 `PascalCase` (组件 `UserProfile.tsx`)。
    *   Python: `snake_case` (如 `user_profile.py`)。

## 5. 开发建议

*   **保持扁平**: 除非必要，尽量不要嵌套过深 (超过 3-4 层)。
*   **就近原则**: 将相关的代码 (组件、样式、测试、API) 放在一起，而不是按文件类型分离。
