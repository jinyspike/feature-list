本项目使用 feature-list.jsonc 管理功能定义与测试追踪。开发时必须遵循以下流程：

1. **新需求开发** — 需求明确、技术设计完成后，使用 `/feature-list-new`。如果正在使用superpower，等完成design (spec) 文件(YYYY-MM-DD-<topic>-design.md)后再使用。
2. **修复与需求变更** — 在修改代码之前，使用 `/feature-list-fix`。它会先更新 feature list，确认后再改代码。
3. **端到端验证** — new 或 fix 完成后（单元测试通过），使用 `/feature-list-verify` 设计并运行 e2e 测试。

**硬性规则：**
- 渐进式：新功能/修改功能必须先有 feature-list.jsonc 条目，再写代码。旧项目无需补全旧 feature list，但新需求必须使用
- feature-list.jsonc 是单一信息源：需求定义、测试追踪、覆盖状态全在一个文件中
- 修复/变更代码前必须先调用 feature-list-fix 更新 feature list
