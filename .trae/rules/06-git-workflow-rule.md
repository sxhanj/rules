---
alwaysApply: false
description: Git 分支策略、提交规范、合并流程、发布管理
---
# Git 工作流规范（涉及 Git 操作时自动生效）

## 1. 分支管理策略

| 分支类型 | 命名规范 | 用途 | 合并目标 |
|----------|----------|------|----------|
| main | `main` | 生产环境代码，受保护不可直接推送 | 仅接受 release/hotfix 合并 |
| develop | `develop` | 开发集成分支，日常开发基准 | 接受 feature 合并 |
| feature | `feature/模块名称-功能描述` | 功能开发分支 | 合并至 develop |
| release | `release/vX.Y.Z` | 发布准备分支 | 合并至 main + develop |
| hotfix | `hotfix/问题描述` | 紧急修复分支 | 合并至 main + develop |

## 2. 提交信息规范（Conventional Commits）

提交信息格式：`<type>: <简短中文描述>`

### Type 类型定义
- **feat**: 新功能（如：feat: 实现用户列表组件基础功能）
- **fix**: 修复 Bug（如：fix: 修复登录页面验证码不显示问题）
- **docs**: 文档更新（如：docs: 添加 API 接口文档）
- **style**: 代码格式调整（如：style: 统一 import 排序顺序）
- **refactor**: 代码重构（如：refactor: 重构用户服务层依赖注入）
- **test**: 测试相关（如：test: 添加用户认证单元测试）
- **chore**: 构建/工具/配置变动（如：chore: 更新 ESLint 配置规则）

### 提交频率要求
- 每个功能点完成后**立即提交**，禁止大量代码堆积后一次性提交
- 提交信息需清晰描述本次变更内容，禁止无意义提交信息（如 "update"、"fix bug"）

## 3. 合并策略与流程

### 标准合并路径
```
feature/* ──→ develop ──→ release/* ──→ main
                    ↑                   │
                    └───────────────────┘ (同步回 develop)
hotfix/* ──→ main + develop (紧急修复双线合并)
```

### 功能分支合并到 develop（3.7 节点检查清单）
合并前必须逐项确认：
- [ ] 所有计划功能已完成实现
- [ ] 单元测试覆盖率 > 90%（有测试项目时适用）
- [ ] 集成测试全部通过
- [ ] 功能测试验收通过
- [ ] 代码规范检查通过（lint/typecheck 无报错）
- [ ] 相关文档已更新完整
- [ ] 无遗留编译错误或警告

## 4. 版本发布规范

### 版本号格式
采用语义化版本号：`v主版本.次版本.修订号`（如 v1.0.0、v2.1.3）

### 版本标签要求
- 必须使用 annotated tag：`git tag -a v1.0.0 -m "Release version 1.0.0"`
- 禁止使用 lightweight tag（无 -a 参数）

### 发布前检查清单
- [ ] 所有功能测试通过
- [ ] 性能指标达标（响应时间 < 100ms、首屏加载 < 2s）
- [ ] 安全检查通过（无严重漏洞）
- [ ] 文档更新完整（README、API 文档、变更日志）
- [ ] 配置文件正确（生产环境配置已就绪）
- [ ] 备份和回滚方案已准备就绪

## 5. 禁止行为
- 禁止直接向 main 分支 push 代码（必须通过 release/hotfix 合并）
- 禁止在 main/develop 分支上直接开发新功能
- 禁止提交包含敏感信息（密码、密钥、Token）的代码
- 禁止强制推送到受保护分支（main/develop/release）
