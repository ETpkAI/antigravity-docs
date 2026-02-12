# Antigravity 测试策略 (Testing Strategy)

高质量的软件离不开全面的测试。本策略定义了 Antigravity 项目的测试标准、工具链及最佳实践。

## 1. 测试金字塔 (The Testing Pyramid)

我们遵循测试金字塔原则，合理分配测试资源：

```text
      / \
     / E2E \       (少量, 慢, 昂贵)
    /-------\
   / Integration \     (适中)
  /---------------\
 /      Unit       \   (大量, 快, 廉价)
/-------------------\
```

*   **单元测试 (Unit Tests)**: 占总测试量的 70%。针对最小可测单元 (函数/类/组件) 进行隔离测试。
*   **集成测试 (Integration Tests)**: 占 20%。测试模块间的交互 (API -> DB, Frontend -> Backend)。
*   **端到端测试 (E2E Tests)**: 占 10%。模拟真实用户行为，测试整个系统的主流程。

## 2. 覆盖率目标 (Coverage Goals)

*   **核心业务逻辑**: > **90%** (Domain Layer, Utils)。
*   **API/Service**: > **80%**。
*   **UI 组件**: > **60%** (重点测交互和状态逻辑，样式变动大可略过)。
*   **总覆盖率**: 建议保持在 **80%** 以上。低于 70% 的提交应被 CI 拒绝。

## 3. 测试工具链 (Toolchain)

### 3.1 前端 (Frontend)
*   **单元/集成框架**: **Vitest** (首选, 极速) 或 **Jest**。
*   **React 组件测试**: **React Testing Library** (推荐, 关注行为而非实现细节)。
*   **E2E 框架**: **Playwright** (更现代, 跨浏览器) 或 **Cypress**。

### 3.2 后端 (Backend - Python)
*   **核心框架**: **pytest** (首选, 插件丰富)。
*   **API 测试**: **FastAPI TestClient** (基于 `httpx`)。
*   **Mock 工具**: `unittest.mock` 或 `pytest-mock`。
*   **覆盖率**: `pytest-cov`。

### 3.3 后端 (Backend - Node.js)
*   **核心框架**: **Jest** 或 **Vitest**。
*   **API 测试**: **Supertest**。

## 4. 最佳实践 (Best Practices)

*   **TDD (测试驱动开发)**: 鼓励先写测试，再写实现。Red -> Green -> Refactor。
*   **Mock 外部依赖**: 单元测试必须 Mock 数据库、外部 API、文件系统等，保证测试速度和独立性。
*   **测试命名**: 使用 `Given-When-Then` 风格或描述性语句。
    *   ❌ `test_login`
    *   ✅ `should_return_token_when_credentials_are_valid`
*   **CI 集成**: 所有测试必须在 CI (GitHub Actions) 中自动运行，失败则禁止合并 PR。
