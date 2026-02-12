# Antigravity 文档编写指南 (Documentation Guide)

清晰、准确的文档是高质量项目的基石。本指南规范了 Antigravity 项目各类文档的编写标准。

## 1. README.md (核心文档)

每个项目的根目录必须包含 `README.md`，作为项目的入口。标准结构如下：

```markdown
# [Project Name]

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Build Status](https://img.shields.io/github/actions/workflow/status/user/repo/ci.yml)

## 简介 (Introduction)
一句话描述项目是做什么的，解决什么痛点。

## 特性 (Features)
*   特性 A
*   特性 B

## 快速开始 (Getting Started)

### 前置条件 (Prerequisites)
*   Node.js >= 18
*   Python >= 3.10

### 安装 (Installation)
```bash
git clone https://github.com/user/repo.git
cd repo
npm install
```

### 运行 (Usage)
```bash
npm run dev
```

## 贡献 (Contributing)
欢迎贡献代码！请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解详情。

## 许可证 (License)
本项目基于 [MIT 许可证](LICENSE) 分发。
```

## 2. API 文档 (API Documentation)

*   **REST API**: 强制遵循 **OpenAPI 3.0+ (Swagger)** 规范。
    *   Python (FastAPI): 代码即文档，自动生成 `/docs`。
    *   Node.js (NestJS): 使用 `@nestjs/swagger` 装饰器自动生成。
    *   手动编写: 使用 YAML 格式编写 `openapi.yaml`。
*   **GraphQL**: 使用 **GraphiQL** 或 **Apollo Sandbox** 提供交互式文档。

## 3. 变更日志 (CHANGELOG.md)

遵循 **[Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)** 规范。

*   **Unreleased**: 尚未发布的变更。
*   **[版本号] - YYYY-MM-DD**: 已发布版本。
    *   **Added**: 新增功能。
    *   **Changed**: 功能变更。
    *   **Deprecated**: 即将移除的功能。
    *   **Removed**: 已移除的功能。
    *   **Fixed**: 修复 Bug。
    *   **Security**: 安全修复。

## 4. 代码注释 (Code Comments)

*   **Docstrings**: 所有公共类、方法必须包含详细的 Docstring (JavaDog/JSDoc)。
*   **TODO**: 使用 `TODO(user): desc` 标记待办事项。
*   **FIXME**: 使用 `FIXME(user): desc` 标记需要修复的问题。

## 5. 语言风格 (Tone & Style)

*   **清晰简洁**: 避免冗长的描述，直奔主题。
*   **统一术语**: 确保同一概念在文档中始终使用相同的术语。
*   **中英文混排**: 英文单词前后加空格 (如 "使用 GitHub Actions 进行部署")。

## 6. Antigravity 交互协议 (Interaction Protocol)

本协议规定了 AI 助手 (Antigravity) 与用户交互的语言标准。

*   **对话语言**: 全程使用 **中文 (Chinese)** 进行交流。
*   **总结语言**: `TaskSummary` 和 `TaskStatus` 等总结性内容，必须完全使用 **中文**。
*   **思考过程**: 在 `<thought>` 块中的思考过程，应**尽量使用中文**，以便于回溯思维路径。
*   **例外情况**: 代码、文件名、专业术语保留英文。
