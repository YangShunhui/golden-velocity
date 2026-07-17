---
name: golden-velocity
description: Use when the user asks for golden语法, golden syntax, Velocity + $vs style, or the team's ShowDoc rules for frontend JavaScript, page controls, SQL, backend code, service components, process functions, temporary tables, external interfaces, or code rewrites. Also use automatically when inspecting, reviewing, learning from, or rewriting scanned files whose content clearly contains Golden backend markers such as Velocity directives, $vs.*, $form, $result, $sqlBean, or SQLTools.*, or Golden frontend markers such as gUtil, $vm, selfPage, platform form/table controls, and page event scripts.
---

# Golden Syntax

Use this skill when the user explicitly asks for `golden语法`, clearly wants this platform style, or supplies/scans files whose content is recognizably Golden frontend JavaScript or backend Velocity.

Do not trigger from ordinary JavaScript alone. Require a coherent platform signal such as multiple related Golden markers, a recognized page event context, or established `$vs`/Velocity usage.

## Core output style

- Output Velocity template code for backend tasks and platform frontend JavaScript for page-control tasks. Do not output unrelated Java or JS pseudocode.
- Prefer these directives when they fit:
  - `#set`
  - `#if`
  - `#elseif`
  - `#else`
  - `#foreach`
  - `#continue`
  - `#break`
  - `#function`
  - `#while`
  - `#try`
  - `#catch`
  - `#finally`
  - `#end`
- Every line should end with `;` when the statement form expects one.
- Keep formatting tidy. Matching `#if` and `#end` must align.

## Execution-context routing

- Route by execution context and code markers, not by file extension alone.
- Treat `onCreate`, `onOpen`, `onClick`, `onChange`, `onCheck`, `onUnCheck`, `onAfterLoad`, `onTableReady`, `onDblClickCell`, and `onBeforeWinClose` handlers as platform frontend JavaScript unless the artifact proves otherwise.
- Treat `beforeSqlSelect` handlers containing `$form`, `$sqlBean`, `$vs.*`, Velocity directives, or `SQLTools.*` query fragments as backend Velocity even when the filename ends in `.js`.
- Use browser-side `gUtil`, `$vm`, form/table controls, `self`, and `selfPage` only in frontend JavaScript. Use `$vs.*`, `$form`, `$result`, and `$sqlBean` only in backend Velocity.
- If the execution context is still ambiguous after inspecting the surrounding page and script, ask the user before generating code.

## Frontend JavaScript essentials

- Use `gUtil.isNull(...)`, `gUtil.isNotNull(...)`, and `gUtil.equals(...)` for frontend null and value checks.
- Use `gUtil.precise(...)` with the page's established precision variables for frontend business arithmetic; never use `$vs.util.precise(...)` in browser code.
- Prefer platform `$vm`, form, table, button, dialog, loading, and service-component APIs over raw DOM, `window`, or hand-built utilities.
- Keep the `$vm.openDialog(...)` invocation head on one line by default, including the callback declaration; start new lines inside the callback body. Split the invocation only when an argument is itself complex or the user requests another format.
- Keep one `$vm.save(...)` entry point. Separate validation and confirmation branches from the save-success body; never copy the complete save block into each branch.
- Remove `console`, `debugger`, unexplained timer polling, and direct DOM manipulation unless the user explicitly requires them or the platform has no equivalent.

## Priority rules

When rules conflict, apply them in this order:

1. ShowDoc constraints: forbidden patterns, performance rules, SQL constraints
2. ShowDoc code conventions
3. Existing snippet-backed Velocity and `$vs.*` APIs
4. Minimal context-based completion that still stays inside the same style

Do not mix in unrelated frameworks or another template language.

## Required conventions

- Do not guess missing business-critical details when generating Golden code. Ask the user first when table names, field names, service type, interface contract, bill type, matching keys, calculation inputs, or other business-impacting details are unclear.
- Only make minimal reasonable assumptions for safe formatting or style defaults that do not change the business result, and state those assumptions in the response.
- Object or string null checks: `$vs.util.isNull($obj)`
- List has-data checks: `$list.size() > 0`
- If the list may be null, guard it before calling `size()`: `!$vs.util.isNull($list) && $list.size() > 0`
- Object comparison: `$vs.util.equals(...)`
- Numeric comparison may use `==`
- String comparison should use `equals`
- Map/object assignment should prefer cloning with `$vs.util.mapClone(...)` rather than direct aliasing when copying data
- Arithmetic operations should default to `$vs.util.precise($num1,$num2,$stropt)` rather than raw numeric operators. In business code, treat all add/subtract/multiply/divide style numeric calculations as precision-sensitive unless there is a clear non-numeric reason not to.
- Numeric calculations should carry explicit decimal precision
- When showing or inspecting variable values, prefer `$vs.log.info(...)`
- Remove temporary debug output such as `console` or `debugger` unless the user explicitly asks to keep them
- In `if` expressions, use `||` for or and `&&` for and
- When an inclusive-tax unit price changes, recalculate dependent inclusive amount, exclusive-tax unit price, exclusive-tax amount, and tax amount together.
- For tax conversion, calculate the divisor with `$taxrate = $vs.util.precise($row.GOODS_TAXRATE, 1, '+')`.
- Use `$vs.decimalTools.money_decimalP` for amount fields and `$vs.decimalTools.exprice_decimalP` for exclusive-tax unit price fields.
- If local-currency fields exist, recalculate local unit prices and amounts from the original-currency fields multiplied by the exchange rate.
- For external HTTP interface calls, use `#try/#catch/#finally`, build request parameters through a separate method, choose the `$vs.http.*` method from the interface document, process the response through a separate method, and save request/response logs in `#finally`.
- For external HTTP calls, build `$encode`, `$contextType`, and `$header` from the interface document. Default to `"UTF-8"` and `"application/json"` only when the document does not specify them.
- For interface logs, truncate serialized request and response payloads to 2000 characters before writing `LOG_REQUEST` or `LOG_RESPONSE`.

## Backend code types

- Golden backend code has two forms: service components and process functions.
- Service components are called by the frontend. The platform provides exactly two fixed parameters: `$form` for frontend input and `$result` for data returned to the frontend.
- When generating a service component, output only the business body. Do not wrap it in `#function service($form, $result)`.
- Service components should read frontend values from `$form` and write response values into `$result`.
- Process functions are reusable backend functions. They may define any number of parameters and may either return data or perform work without returning.
- When generating a process function, use `#function name($arg1, $arg2)` and choose parameters from the request.
- If the user asks for Golden backend code without specifying a type, default to a process function.
- If the user mentions frontend calls, `$form`, `$result`, or returning data to the frontend, generate a service component.

## Temporary table rules

- When backend logic needs temporary tables, prefer a dedicated `#function createTemporaryTable()` to create them in one place.
- Use `$vs.dbTools.createTempTable(...)` for `CREATE TEMPORARY TABLE ...`; do not use plain `$vs.dbTools.execute(...)` for temporary table creation.
- Wrap multi-line temporary-table SQL in backticks.
- Temporary table names should use uppercase underscore style and usually end with `_TMP`.
- Temporary table fields should include the type, `DEFAULT NULL`, and `COMMENT`.
- Do not add primary keys, indexes, or constraints unless the user explicitly asks for them.
- If later logic depends on a temporary table, call `createTemporaryTable()` before inserting into or querying from the temporary table.

## Report temporary-table pattern

- Use this pattern for complex reports that combine multiple sources, need staged aggregation, or must be compatible with MySQL temporary-table limits.
- Split the report into two Golden files:
  - a process-function file that creates and fills temporary tables
  - a report-query file that invokes the process function and only queries completed temporary tables
- In the process file, create all temporary tables first, prepare shared data such as settlement dates, then call focused `insert...Data($form)` methods by source or business segment.
- Each segment should use one `INSERT INTO TEMP_TABLE (...) SELECT ...` and insert only fields supplied by that segment. Do not add large groups of `0 AS FIELD_NAME` placeholders.
- In the report-query file, use `WITH XXX_SUM_DATA AS (...)` to aggregate the temporary table first, then calculate final fields and apply main report filters in the outer query.
- MySQL must not read and write the same temporary table in one SQL statement. When later logic needs dimensions from the main temporary table, first copy them into a staging table such as `XXX_BASE_TMP` or `XXX_SCOPE_TMP`.
- Do not reuse a CTE that depends on a temporary table across multiple `UNION ALL` branches. Materialize the source into another temporary table, then run independent insert statements when multiple difference rows are required.
- `createTempTable(...)` may implicitly commit. Create report temporary tables before business DML that must remain rollback-safe.

## Preferred process patterns

- For sync-style processes, prefer this shape when it fits:
  - query source list
  - query target list
  - build target map
  - decide insert / update / skip
  - batch insert / batch update
- When the target map already stores the full row object, prefer reading dependent fields from that object rather than maintaining duplicate field-only maps.
- When source and target tables share many fields with the same names, compare these two approaches first:
  - `$vs.util.mapClone(...)` plus `remove(...)` plus a few overrides
  - manual field-by-field assignment
  Use the clearer one for the actual data size and risk.
- Do not treat `mapClone(...)` as a hard default. If the object is large, the field mismatch risk is high, or local docs warn about memory pressure, fall back to explicit field mapping.
- When inserting with `$vs.dbTools.insert(...)` or `$vs.dbTools.batchInsert(...)`, do not set primary key fields. The platform insert layer generates them automatically.
- If source data or cloned rows contain primary key fields such as `ID` or `FID`, remove them before insert or batch insert.
- Generate bill numbers from the bill type when the target table has a bill-code field. Use `_BILL_TYPE_CODE_`, `BILLTYPE_CODE`, and `$vs.billNoTools.getBillNo($row)`.
- When generating bill numbers using temporary helper fields such as `_BILL_TYPE_CODE_` or `BILLTYPE_CODE`, remove those temporary keys before `insert(...)`, `batchInsert(...)`, or `batchUpdate(...)`.

## Performance and process rules

- Avoid repeated cache access inside loops. Move stable reads outside the loop or reuse via a map.
- Minimize queries inside loops.
- Minimize process calls inside loops.
- If a loop must call a process function, prefer:

```velocity
#set($proc = $vs.proc.find('...'));
$proc.method();
```

- Do not prefer `$vs.proc.invoke(...)` for loop-heavy code because it is slower.
- If `$vs.date.getDbDate()` is needed in a loop, read it once outside the loop.
- Map keys should use string-like keys, not numeric keys.
- When choosing a sync or update key, prefer the business-unique key first. Add date or primary-key conditions only when the data model requires them.

## SQL and datasource rules

- Use aliases for datasource tables; do not keep repeating full table names.
- In SQL text expressions, prefer cross-database `SQLTools.*` helpers for date, string, null, type-conversion, pagination, and row-number operations.
- Do not confuse SQL text helpers `SQLTools.*` with Velocity query-builder helpers `$vs.sqlTools.*`.
- For empty-field checks in SQL, use `SQLTools.isEmpty(...)`
- For non-empty-field checks in SQL, use `SQLTools.isNotEmpty(...)`
- In SQL arithmetic expressions, wrap nullable numeric fields with `SQLTools.isNull(field,0)` before using `+`, `-`, `*`, or `/`.
- In SQL multiplication and division expressions, wrap the result with `round(..., 2)` by default.
- SQL addition and subtraction do not require `round(..., 2)` by default unless the business field is an amount, price, or the user asks for fixed precision.
- In SQL division, guard against zero denominators with `case when` or an equivalent filter when the denominator may be zero.
- Avoid database-specific functions such as `ifnull`, `nvl`, `date_add`, or `to_date` when a `SQLTools.*` helper exists.
- Do not generate `SQLTools.UUID()` for primary keys during normal inserts; the platform insert layer generates primary keys unless the user explicitly asks for database-layer UUIDs.
- In joins between a main table and detail table, keep the main table on the left side of `inner join` so data permission behavior stays correct.
- Bill numbering rules should assume numbering starts from `1` unless the user says otherwise.
- When the requirement is "take the last valid row per group", compare these approaches first:
  - SQL window functions such as `ROW_NUMBER() OVER (...)`
  - process-side map or grouping de-duplication
  Prefer the SQL window approach when the database can express the grouping cleanly and the query remains readable.

## API preference

- Prefer the team's existing `$vs.*` capabilities before inventing helpers.
- Precision variables should use the standard decimal fields from the reference file.
- For detailed API families, custom helper methods, and rules, read [references/golden-rules.md](references/golden-rules.md).
- For frontend JavaScript page-control methods such as dialogs, loading, page/window operations, frontend service-component calls, permissions, system variables, and frontend utilities, read [references/frontend-page-api.md](references/frontend-page-api.md).
- For frontend window scripts using `$vm`, `self`, `selfPage`, forms, tables, buttons, lifecycle events, save flows, or selection dialogs, read [references/frontend-window-controls.md](references/frontend-window-controls.md).
- For exact `$vs.*` method signatures, parameters, return types, or method selection, read [references/vs-service-api.md](references/vs-service-api.md).
- For SQL text helper signatures and examples such as `SQLTools.toChar(...)`, `SQLTools.isNull(...)`, or `SQLTools.top(...)`, read [references/sqltools-reference.md](references/sqltools-reference.md).
- Do not mix frontend page-control APIs with backend Velocity `$vs.*` APIs.
- If the `$vs` API reference conflicts with the team Golden rules, follow the team Golden rules first.
- If the `SQLTools.*` reference conflicts with the team SQL rules, follow the team SQL rules first.
- For external HTTP calls, use the interface document and [references/vs-service-api.md](references/vs-service-api.md) to choose the most suitable `$vs.http.*` method.

## When coverage is incomplete

- Stay in Velocity + `$vs` style for backend code and platform page-control style for frontend JavaScript.
- Extend naming conservatively to match the existing ecosystem.
- Do not fall back to normal Java/JS pseudocode unless the user explicitly asks for a non-golden version.
