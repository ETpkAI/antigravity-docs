# Antigravity 融合编程规范 (Fusion Coding Standards)

本文档概述了 Antigravity 所有开发任务必须遵循的编程规范与最佳实践。本标准融合了**微软 (Microsoft)**、**腾讯 (Tencent)** 和 **阿里巴巴 (Alibaba)** 的业界领先实践，旨在确保代码的高质量、可维护性、安全性与健壮性。

## 1. 命名与风格 (Naming & Style)

### 1.1 命名约定 (Naming Conventions)
*   **见名知意 (Self-Explanatory)**：命名必须清晰且具有描述性。严禁使用 `a`, `b`, `tmp`, `data` 等无意义的名称。
*   **类/类型 (Classes/Types)**：使用 **大驼峰命名法 (PascalCase)**。
    *   示例：`UserController`, `PaymentService`。
*   **方法/变量 (Methods/Variables)**：使用 **小驼峰命名法 (camelCase)** (Java/JS/TS/Go) 或 **蛇形命名法 (snake_case)** (Python/Ruby)。
    *   Java 示例：`getUserById`, `userId`。
    *   Python 示例：`get_user_by_id`, `user_id`。
*   **常量 (Constants)**：使用 **全大写蛇形命名法 (UPPER_SNAKE_CASE)**。
    *   示例：`MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT_MS`。
*   **接口 (Interfaces)**：
    *   C#/.NET：必须以 `I` 开头 (如 `IRepository`)。
    *   Java/TS：通常无需前缀，除非为了区分实现类，或者是为了遵循特定框架约定。
*   **严禁事项 (Prohibited)**：
    *   🚫 **禁止拼音**：严禁使用汉语拼音或中英混合命名（除非是 `Alibaba`, `Tencent`, `Taobao` 等专有名词）。
    *   🚫 **禁止类型前缀/后缀**：避免使用匈牙利命名法或类型指示符（如 `strName`），除非是集合类型的后缀（如 `userList`, `userMap`）有助于理解。
    *   🚫 **禁止特殊字符起止**：严禁以 `_` 或 `$` 开头或结尾，除非是特定语言/框架的强制约定（如 C# 私有字段 `_name` 或 Python 私有变量 `_name`）。

### 1.2 格式化 (Formatting)
*   **行宽限制**：单行代码硬性限制为 **120 字符**。
*   **缩进**：统一使用 **4 个空格**。根据语言标准可做调整（如 JS/TS/YAML 项目中若约定为 2 空格则遵循项目约定）。
*   **大括号风格**：
    *   Java/JS/TS/Go：K&R 风格（左大括号不换行）。
    *   C#：Allman 风格（左大括号独占一行）。
*   **空格使用**：
    *   运算符两侧加空格（`a + b`，而不是 `a+b`）。
    *   逗号/冒号后加空格（`func(a, b)`，`key: value`）。

## 2. 代码质量与架构 (Code Quality & Architecture)

### 2.1 核心原则 (Principles)
*   **KISS (Keep It Simple, Stupid)**：保持简单。复杂的代码难以维护且容易出错。
*   **DRY (Don't Repeat Yourself)**：拒绝重复。将重复逻辑提取为函数或模块。
*   **SOLID**：严格遵守面向对象设计的五大原则：
    *   **SRP**：单一职责原则 (Single Responsibility Principle)。
    *   **OCP**：开闭原则 (Open/Closed Principle)。
    *   **LSP**：里氏替换原则 (Liskov Substitution Principle)。
    *   **ISP**：接口隔离原则 (Interface Segregation Principle)。
    *   **DIP**：依赖倒置原则 (Dependency Inversion Principle)。

### 2.2 模块化 (Modularity)
*   **高内聚，低耦合**：模块应专注于单一功能，并尽量减少对其他模块的依赖。
*   **分层架构**：严格遵循架构分层（如 API层 -> 服务层 -> 数据访问层）。上层调用下层，严禁下层反向调用上层或跨层调用。

### 2.3 拒绝魔法值 (Magic Values)
*   **禁止魔法数字/字符串**：代码逻辑中严禁直接出现未定义的字面量。
*   **必须提取**：将它们提取为具名的**常量 (Constants)** 或 **枚举 (Enums)**。
    *   ❌ 错误：`if (status == 1) ...`
    *   ✅ 正确：`if (status == Status.ACTIVE) ...`

## 3. 健壮性与安全 (Robustness & Security)

### 3.1 防御性编程 (Defensive Programming)
*   **输入校验**：永远不要信任外部输入（用户输入、API 响应、文件内容）。必须校验类型、长度、格式和范围。
*   **空安全 (Null Safety)**：
    *   集合类型避免返回 `null`，应返回空集合。
    *   使用 `Optional` (Java), `?` (C#/TS), 或在访问前显式检查 `None`/`nil`。
    *   **Fail Fast**：遇到无效状态应立即报错，防止错误扩散。

### 3.2 异常处理 (Exception Handling)
*   **禁止空 Catch**：严禁编写空的 `catch` 块。
*   **捕获特定异常**：尽可能捕获具体的异常类型，而不是通用的 `Exception` 或 `Error`。
*   **记录或抛出**：捕获异常后，要么处理并记录日志，要么向上抛出。严禁吞掉异常（Silently Swallowing）。

### 3.3 安全性 (Security)
*   **数据清洗**：在输出到 HTML（防 XSS 攻击）或拼接 SQL（防 SQL 注入）前，必须对数据进行清洗或转义。强制使用参数化查询或 ORM。
*   **最小权限原则**：程序运行应仅赋予完成任务所需的最小权限。

## 4. 注释与文档 (Comments & Documentation)

### 4.1 文档化 (Documentation)
*   **公共接口**：所有公共类和方法必须包含文档注释（Javadoc, Docstring, JSDoc）。
    *   描述**做什么 (What)**、**参数 (Parameters)**、**返回值 (Return Values)** 和 **异常 (Exceptions)**。
*   **自解释代码**：代码本身应足够清晰，使得行内注释仅用于解释极其复杂的逻辑。

### 4.2 行内注释 (Inline Comments)
*   **解释“为什么” (Explain Why)**：注释的核心作用是解释**背后的原因**、**设计决策**、**复杂的算法逻辑**或**权宜之计 (Hack)**。
*   **业务逻辑说明**：如果代码逻辑无法直观体现业务规则，必须通过注释补充说明。

---

**注意**：以上即为“Antigravity 预设”标准。我 (Antigravity) 将在生成代码时严格遵守这些规范。如果现有项目代码与本规范有显著冲突，我会先询问您是进行重构还是保持一致。
