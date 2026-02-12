# Antigravity Git 工作流规范 (Git Workflow Standards)

本规范旨在统团队的代码版本管理流程，确保协作效率、代码质量和历史记录的清晰性。

## 1. 分支策略 (Branching Strategy)

我们需要采用 **Git Flow** (适用于复杂项目) 或 **Trunk Based** (适用于快速迭代项目) 的混合模式。默认推荐以下分支结构：

*   **`main` (或 `master`)**: 主分支。**受保护分支**。
    *   存放随时可部署到生产环境的代码。
    *   严禁直接 Push，必须通过 Pull Request (PR) 合并。
*   **`develop`**: 开发主分支。**受保护分支**。
    *   日常开发的汇总分支。
    *   部署到测试环境 (Staging) 的代码来源。
*   **`feature/*`**: 功能分支。
    *   从 `develop` 检出。
    *   命名规范：`feature/功能名称` (如 `feature/login-page`, `feature/user-api`)。
    *   开发完成后合并回 `develop`。
*   **`fix/*` (或 `bugfix/*`)**: 修复分支。
    *   用于修复非紧急 Bug。
    *   命名规范：`fix/bug描述` (如 `fix/header-alignment`)。
*   **`hotfix/*`**: 紧急修复分支。
    *   从 `main` 检出，用于修复生产环境的严重 Bug。
    *   修复后同时合并回 `main` 和 `develop`。

## 2. 提交规范 (Commit Convention)

采用 **[Conventional Commits](https://www.conventionalcommits.org/)** 规范。提交信息格式如下：

```text
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

### 2.1 Type (必填)

*   **`feat`**: 新功能 (Feature)。
*   **`fix`**: 修复 Bug。
*   **`docs`**: 仅文档变更 (Documentation)。
*   **`style`**: 代码格式调整 (不影响逻辑，如空格、分号)。
*   **`refactor`**: 代码重构 (既不修复 Bug 也不添加功能)。
*   **`perf`**: 性能优化。
*   **`test`**: 测试相关 (添加或修改测试用例)。
*   **`chore`**: 构建过程或辅助工具变动 (如依赖更新)。
*   **`build`**: 影响构建系统或外部依赖的更改。
*   **`ci`**: CI 配置文件或脚本的更改。

### 2.2 Scope (选填)

用于说明 commit 影响的范围，如 `api`, `auth`, `ui` 等。

### 2.3 Subject (必填)

简短描述变更内容 (50 字符以内)。必须使用祈使句（如 "Add login button" 而非 "Added login button"）。

### 示例

```text
feat(auth): 添加 JWT 登录验证功能

实现用户登录接口，包含 Token 生成与校验逻辑。
Closes #123
```

```text
fix(ui): 修复移动端导航栏重叠问题
```

## 3. Pull Request (PR) 流程

1.  **提交 PR**: Feature 分支开发完成后，向 `develop` 提交 PR。
2.  **CI 检查**: 确保自动化测试 (Unit Test) 和 Lint 检查通过。
3.  **代码审查 (Code Review)**: 至少需要 1 名其他开发者 Review 通过。
    *   重点检查：逻辑正确性、代码规范 (Coding Standards)、潜在 Bug。
4.  **合并策略**:
    *   **Squash and Merge**: 推荐。将 Feature 分支的多个 commit 压缩为一个，保持主分支历史整洁。
    *   **Rebase and Merge**: 可选。保持线性历史。
    *   **Merge Commit**: 尽量避免，除非需要保留分支历史。

## 4. 最佳实践 (Best Practices)

*   **原子提交 (Atomic Commits)**: 每个 commit 只做一件事情，且能通过编译和测试。
*   **勤拉取 (Pull Often)**: 频繁从 `develop` 拉取最新代码 (Rebase 优先)，避免大规模冲突。
*   **不提交生成文件**: `node_modules`, `dist`, `.env` 等文件绝对不能提交（确保 `.gitignore` 配置正确）。
*   **Rebase over Merge**: 在本地分支同步上游代码时，优先使用 `git Pull --rebase`，保持提交历史呈线性。
