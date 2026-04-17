---
alwaysApply: false
globs: ["**/*.py", "**/*.js", "**/*.ts", "**/*.java", "**/*.go"]
description: 代码文件编码规范、架构、异常处理约束
---
# 代码文件质量规则（匹配代码文件自动生效）

## 通用编码原则
1. 遵循语言官方规范（Python PEP8、JS Standard），命名语义化无缩写
2. 高内聚低耦合：单函数建议 ≤30 行，超过时需在注释中说明拆分原因；单模块仅1个核心职责
3. 强制异常捕获+参数校验，全覆盖边缘场景，无裸奔代码
4. 遵循 SOLID/DRY/KISS 原则，禁止重复代码、禁止过度设计
5. 中文路径 IO 操作自动加编码容错，兼容 Windows/macOS 双系统

## Vue 3 / TypeScript 前端规范
6. 组件强制使用 `<script setup lang="ts">` 语法糖
7. 所有 Props 和 Emits 必须有完整的 TypeScript 类型定义
8. 计算属性优先使用 `computed` 而非 `methods`
9. 样式必须使用 `scoped` 作用域，禁止全局样式污染
10. 通用组件与业务组件分离，保持高复用性

## Python 后端规范
11. 遵循 PEP 8 编码标准（行长度 120 字符）
12. 使用 Type Hints 进行类型注解（Python 3.8+）
13. 命名规范：函数 snake_case、类 PascalCase、常量 UPPER_SNAKE_CASE、文件 snake_case.py
14. 导入顺序固定：标准库 → 第三方库 → 本地模块
15. 异常处理必须使用具体异常类型，**禁止裸露 `except`**

## 测试规范（有测试项目时适用）
16. 测试覆盖率目标值：单元测试 > **90%**，集成测试 > **80%**
17. 测试用例组织遵循 **AAA 模式**（Arrange-Act-Assert）
18. 使用 Mock 隔离外部依赖（数据库、API、文件系统等）
19. 覆盖正常场景、异常场景、边界场景三类用例