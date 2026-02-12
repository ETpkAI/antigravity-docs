# Antigravity Documentation (Antigravity 文档库)

欢迎来到 Antigravity 文档库。这里存放了所有适用于 Antigravity 开发生态的标准、规范与最佳实践。

这些文档融合了 **微软 (Microsoft)**、**腾讯 (Tencent)** 和 **阿里巴巴 (Alibaba)** 的业界领先经验，旨在为开发团队提供一套统一、高效、高质量的工程化指南。

## 📚 文档索引 (Documentation Index)

### 核心规范 (Core Standards)
*   **[编程规范 (Coding Standards)](coding_standards.md)**
    *   涵盖命名约定、代码风格、架构原则、安全实践等核心编程准则。

### 工程化流程 (Engineering Workflow)
*   **[Git 工作流 (Git Workflow)](git_workflow.md)**
    *   定义了 Git 分支策略 (Git Flow/Trunk Based) 和提交信息规范 (Conventional Commits)。
*   **[测试策略 (Testing Strategy)](testing_strategy.md)**
    *   确立了测试金字塔模型、覆盖率目标及前后端测试工具链。
*   **[开发协同流程 (Development Process)](development_process.md)**
    *   定义了 **多角色圆桌会议 (Multi-Agent Roundtable)**、**模型分配策略 (Model Allocation)** 及角色分工与执行的 SOP 流程。

### 架构与技术栈 (Architecture & Tech Stack)
*   **[架构设计模式 (Architecture Patterns)](architecture_patterns.md)**
    *   提供了标准的前后端项目目录结构和分层架构设计（Clean Architecture）。
*   **[技术栈偏好 (Tech Stack Presets)](tech_stack_presets.md)**
    *   列出了 Antigravity 首选的技术栈组合（如 React, FastAPI, NestJS 等）。

### 其他 (Others)
*   **[文档编写指南 (Documentation Guide)](documentation_guide.md)**
    *   规范了 README、API 文档和 Changelog 的编写标准。

## 🚀 快速环境搭建 (Quick Environment Setup)

为了确保 Antigravity 能发挥最大效能，请确保您的本地环境安装了以下核心工具链。

### 一键安装脚本 (macOS)

复制以下命令并在终端运行，即可完成所有基础工具的安装：

```bash
# 1. 安装 Homebrew (如果尚未安装)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. 配置环境变量 (Apple Silicon)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# 3. 安装核心工具链
brew install git gh node python3
brew install --cask docker

# 4. 登录 GitHub CLI
gh auth login
```

### 验证安装 (Verification)

```bash
git --version
gh --version
docker --version
node --version
python3 --version
```

## 🤝 贡献 (Contributing)

如果您发现任何规范有待改进，欢迎提交 Pull Request 或 Issue。所有的变更都应遵循 [文档编写指南](documentation_guide.md)。

## 📝 许可证 (License)

[MIT License](LICENSE)
