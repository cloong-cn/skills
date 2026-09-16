---
name: business-logic-documenter
description: Trace an existing business function across frontend, backend, database objects, scheduled jobs, triggers, integrations, and manual operations, then produce a maintainable Markdown business-logic document. Use when someone asks to document, explain, audit, or preserve the logic of an existing feature. Do not modify source code unless the user explicitly requests a code change.
---

# Business Logic Documenter

Use this skill to turn code and operational evidence into a document that another maintainer can read without reconstructing the whole call chain.

## Workflow

1. Define the scope first: project, feature name, entry page or API, key fields, and the requested output. Locate existing business-logic documents before starting.
2. Trace the complete chain in read-only mode: UI entry and events -> request parameters -> controller/API -> service and transactions -> mapper/DAO/SQL -> tables, views, procedures, functions, triggers, jobs, queues, and downstream consumers.
3. Search for every way the important fields can be read or written. Include user actions, API callers, application schedulers, database schedulers, triggers, stored procedures, message consumers, imports, external systems, and manual SQL when evidence exists.
4. Record permissions, tenant or organization boundaries, status transitions, validation rules, transaction boundaries, retries, and failure behavior. Keep frontend validation separate from backend enforcement.
5. Mark each statement as confirmed, inferred, or pending verification. Never invent a data source or business rule just because it is common in similar code.
6. Fill the reference template in `references/业务逻辑说明模板.md`. Prefer stable paths, class/method names, SQL object names, and field mappings; add line numbers only when they are useful and currently verified.
7. If the user requested documentation only, do not edit application source, database objects, or deployment configuration. If a source change was requested, update the document after the change and record the validation performed.

## Required data-source coverage

Explicitly check and document these categories, even when the result is “未发现” or “待确认”:

- 页面、接口、批处理、应用定时任务和人工操作
- 数据库定时任务（DBMS_SCHEDULER、DBMS_JOB 等）
- 行级或语句级触发器
- 存储过程、函数、视图、同义词、数据库链接
- MQ、WebSocket、外部 HTTP 服务、文件导入导出
- 手工 SQL、运维脚本和部署配置

For each source, state the object or path, trigger condition, affected fields, and evidence. Distinguish a trigger that runs only on INSERT/UPDATE/DELETE from a scheduler that runs because of time.

## Output

Return:

- a short conclusion describing what the feature does and where its authoritative writes occur;
- a complete Markdown document using the reference template;
- an evidence table with paths, symbols or SQL objects, and findings;
- verification limits and concrete follow-up checks for Oracle, Redis, schedulers, triggers, external systems, browser behavior, or deployment when those cannot be confirmed locally.

Keep the document in Chinese when the surrounding project and request are Chinese. Link source files with absolute paths when possible.
