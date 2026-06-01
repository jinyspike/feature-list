本项目使用 feature-list.jsonc 管理功能定义与测试追踪。开发新功能时必须遵循以下流程：

1. **需求阶段** — 结合用户所提出的需求，使用 `/feature-list-pm`
2. **开发阶段** — 使用 `/feature-list-dev`
3. **QA 阶段** — 使用 `/feature-list-qa`

**硬性规则：**
- 渐进式：新功能/修改功能必须先有 feature-list.jsonc 条目，再写代码。旧项目无需补全旧 feature list，但新需求必须使用
- feature-list.jsonc 是单一信息源：需求定义、测试追踪、覆盖状态全在一个文件中
