# Business Logic Documenter

这是一个用于整理现有项目业务逻辑的 Codex Skill。它会沿着“页面或接口 -> 后端服务 -> SQL/数据库对象 -> 定时任务、触发器和下游系统”的链路取证，并生成中文 Markdown 文档，默认附一张基于已确认逻辑的简洁 Mermaid 主流程图。

## 目录

- [SKILL.md](./SKILL.md)：Skill 工作流程与输出要求
- [references/业务逻辑说明模板.md](./references/业务逻辑说明模板.md)：可长期维护的文档模板
- [prompt.md](./prompt.md)：不使用 Skill 时也可以直接粘贴的提示词
- [agents/openai.yaml](./agents/openai.yaml)：Codex 的显示信息和默认提示词

## 使用

在 Codex 中调用：

`$business-logic-documenter`

也可以直接描述：

> 请梳理这个功能的完整业务逻辑，追踪前端、接口、服务、SQL、数据库定时任务、触发器和下游写入，并按模板生成文档；无法确认的内容标为待确认。

默认只做代码和配置审计，不修改业务源码。只有用户明确要求时才修改源代码、数据库对象或部署配置。

## 维护约定

文档应记录证据路径、关键类/方法/SQL 对象、字段读写、权限与数据范围、所有数据来源、验证结果和未确认项。流程图只表达已确认的主路径，复杂流程拆分，未确认内容明确标记。数据库定时任务、触发器、手工 SQL 等无法从应用仓库确认时，必须明确列出后续核查动作。

## License

本目录使用仓库根目录的 PolyForm Noncommercial 1.0.0 许可。商业使用需要版权方另行书面许可，详见根目录 [LICENSE](../LICENSE)。
