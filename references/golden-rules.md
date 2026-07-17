# Golden Rules Reference

This file is the detailed rule source for `golden语法`. Load it when a request needs exact APIs, SQL constraints, formatting rules, or custom helper selection.

For complete `$vs.*` service-script method signatures and return types, read [vs-service-api.md](vs-service-api.md). This file remains the source for team conventions and business rules.

For SQL text helper functions such as `SQLTools.toChar(...)`, `SQLTools.isNull(...)`, and `SQLTools.top(...)`, read [sqltools-reference.md](sqltools-reference.md).

For frontend `gUtil` methods such as dialogs, loading, service-component calls, permissions, system variables, and common utilities, read [frontend-page-api.md](frontend-page-api.md).

For frontend window scripts using `$vm`, `self`, `selfPage`, forms, tables, buttons, lifecycle events, save flows, or selection dialogs, read [frontend-window-controls.md](frontend-window-controls.md).

## Clarify before coding

When generating Golden code, do not guess missing business-critical details. Ask the user first when unclear details could change the business result.

Ask before coding when any of these are unclear:

- Table names, field names, or source/target table relationships.
- Service component vs process function type.
- External interface URL, HTTP method, authentication, headers, request format, or response structure.
- Bill type code, bill-code field, or numbering rule.
- Amount, tax rate, exchange rate, weight, quantity, price, or precision-related input fields.
- SQL query filters, join keys, data-permission main table, or grouping keys.
- Insert, update, delete, sync, or de-duplication matching keys.
- Return shape for frontend `$result` or process function output.
- Frontend form/table/page-control method signatures when they are not present in `frontend-page-api.md`.

Safe defaults may be used without asking only when they do not affect the business result, such as:

- Velocity formatting, indentation, and `#if/#end` alignment.
- Semicolon placement.
- Standard null-check, comparison, and `SQLTools.isNull(...)` rules.
- `$vs.util.precise(...)` for arithmetic.
- Not setting primary key IDs during normal inserts.

When a safe default is used, state the assumption briefly in the response.

## Frontend page-control rules

Use frontend page-control APIs when the user asks for `golden` frontend JS, 页面控件, form/table/page operations, dialogs, loading, opening pages/windows, frontend service-component calls, permissions, system variables, or frontend utilities.

### Execution-context routing

- Route by event and code markers rather than `.js` alone.
- Generate platform frontend JavaScript for `onCreate`, `onOpen`, `onClick`, `onChange`, `onCheck`, `onUnCheck`, `onAfterLoad`, `onTableReady`, `onDblClickCell`, and `onBeforeWinClose` handlers.
- Generate Velocity for `beforeSqlSelect` handlers that use `$form`, `$sqlBean`, `$vs.*`, Velocity directives, or `SQLTools.*` fragments, even when the stored filename ends in `.js`.
- Do not use `$vs.*`, `$form`, `$result`, or `$sqlBean` in browser code. Do not use `gUtil`, `$vm`, `self`, or page controls in backend Velocity.

### Runtime and event context

- Reuse platform-provided globals; do not redeclare or synthesize them.
- Common window globals are `self`, `selfPage`, `args`, and `openType`.
- Common event parameters are `newData` and `rowIndex` for table `onChange`, `rowData` for `onCheck/onUnCheck`, `field` and `rowData` for `onDblClickCell`, and `closeCallback` for `onBeforeWinClose`.
- Treat control IDs such as `inputForm`, `searchForm`, `mainTable`, `detailTable`, and `tabPage` as page-configured objects. Do not invent a control ID that is not provided by the request or surrounding page.

### API and code conventions

- Prefer platform APIs from [frontend-page-api.md](frontend-page-api.md) and [frontend-window-controls.md](frontend-window-controls.md) instead of raw browser APIs or hand-written DOM/window utilities.
- Use `gUtil.isNull(...)` and `gUtil.isNotNull(...)` for frontend null checks and `gUtil.equals(...)` for business value or string comparison.
- Clone dialog-returned or source rows with `gUtil.clone(...)` before changing fields; do not mutate the returned row unless the page contract explicitly requires it.
- Format `$vm.openDialog(pageAlias, params, openType, isNew, function (rows) {` as one line by default. Put the callback statements on following indented lines. Break the invocation only when an argument is itself complex or the user explicitly requests multiline arguments.
- Remove `console`, `debugger`, direct DOM manipulation, and unexplained timer polling. Use `gUtil.listen(...)` for lazily mounted controls when that API is available; use `setTimeout(...)` only for a documented render-timing requirement.
- End statements with semicolons and use early returns for failed validation.
- Do not promote bill-type codes, field names, or project utilities found in one business page into universal Golden APIs.

### Form, table, and button state

- When a controlling field changes, handle dependent values, editable state, required state, and select rebinding together.
- If disabling a dependent field makes its old value invalid, clear the code and display fields before disabling it.
- Keep code/display field pairs synchronized when the page schema uses both.
- Use `disabledEdit(true)` for a read-only page or control, then explicitly unlock only the fields allowed by the current `openType`.
- For a single-row action, reject multiple selection first, then reject the empty current row, then perform the action.
- Use `getData()` for all table data, `getSelectRows()` for checked rows, and `getRow()` for the current row; do not treat these result shapes as interchangeable.
- Use `self.button(id).enabled()/disabled()/show()/hide()` for button state instead of manipulating button DOM.

### Service calls and lazy controls

- Use `gUtil.getServerData(...)` only when the next statement requires an immediate result. Wrap critical synchronous calls in `try/catch` and report failures with `gUtil.error(...)`.
- Prefer `gUtil.request(...)` for asynchronous calls. Supply an error callback for save, delete, audit, or other critical mutations and restore disabled buttons or loading state there.
- Keep shared success behavior in one named function when multiple request or confirmation branches converge. Do not copy the mutation or save body into every branch.
- Prefer platform dialog, message, loading, and window APIs over raw `alert(...)`, manual loading masks, or hand-built navigation.

### Frontend precision and row linkage

- Use `gUtil.precise(...)` for frontend business arithmetic; backend Velocity calculations still use `$vs.util.precise(...)`.
- Pass the page's established quantity, weight, price, amount, tax-rate, or exchange-rate precision variable when it is available. Do not invent a precision object or field.
- Perform multi-step calculations as a sequence of `gUtil.precise(...)` calls, then write results with the configured table's `setDataValue(...)` or `update(...)` method.
- Prefer an existing page calculation helper such as `$pageUtil.calculate(...)` when the surrounding project defines it and its contract is known.
- For frontend date and number formatting, prefer `gUtil.formatDate(...)`, `gUtil.formatNumber(...)`, and related helpers when their signatures are available.

### Save orchestration

- Keep exactly one `$vm.save(...)` call for one save action. Put the success callback and before-save callback in named functions when the logic is non-trivial.
- In the before-save callback, return `true` only when synchronous validation passes and saving may continue immediately.
- When confirmation is required, open `gUtil.confirm(...)`, call the platform-provided continuation such as `save()` only in the confirm callback, and return `false` from the before-save callback to pause the original path.
- Do not duplicate the complete `$vm.save(...)` block across multi-party, quota, overdue, or similar confirmation branches. Resolve those branches first and converge on one save entry point.
- Keep saved-result field write-back, dirty-state reset, button state, and post-save table reload in the single success callback.

### Selection-dialog flow

- On dialog `onOpen`, clear stale selected data and store incoming `args` on the source table only when later events need them.
- On source-table `onAfterLoad`, restore checks from the selected table without adding duplicate selected rows.
- On `onCheck`, add a cloned or mapped row to the selected table, using `$vm.selPageAddRow(...)` when its observed contract fits.
- On `onUnCheck`, delete the corresponding row from the selected table.
- When deleting from the selected table, uncheck the matching source row in the deletion callback.
- On confirmation, read selected rows, clear temporary selected data when the page is reused, and return through `$vm.dialogCallback(rows)`.

### Dirty-window close

- In `onBeforeWinClose`, allow read-only `openType` values to close directly when the page contract says they cannot be dirty.
- Use `self.getIsChange()` to detect edits. If unchanged, return without blocking.
- If changed, ask for confirmation, call `closeCallback()` only after confirmation, and return the platform's blocking value from the event.

Do not invent `$vm`, form, table, grid, or event signatures. Use only signatures documented in [frontend-window-controls.md](frontend-window-controls.md), present in the surrounding project, or confirmed by API Center; otherwise ask the user.

## Common directives

- `#set`: assignment
- `#if`: conditional
- `#elseif`: conditional
- `#else`: conditional
- `#foreach`: loop
- `#continue`: loop control
- `#break`: loop control
- `#function`: function definition
- `#while`: loop
- `#try`: exception handling
- `#catch`: exception handling
- `#finally`: exception handling
- `#end`: block end

## Decimal precision fields

- `$vs.decimalTools.num_decimalP`
- `$vs.decimalTools.weight_decimalP`
- `$vs.decimalTools.price_decimalP`
- `$vs.decimalTools.money_decimalP`
- `$vs.decimalTools.exprice_decimalP`
- `$vs.decimalTools.taxrate_decimalP`
- `$vs.decimalTools.exrate_decimalP`

Use these whenever quantity, weight, price, amount, tax rate, or exchange rate precision is involved.

## Existing snippet-backed API families

- `$vs.util.*`
- `$vs.dbTools.*`
- `$vs.proc.*`
- `$vs.date.*`
- `$vs.cache.*`
- `$vs.sqlHelper.*`
- `$vs.log.*`
- `$vs.thread.*`
- `$vs.format.*`
- `$vs.http.*`
- `$vs.billNoTools.*`

Representative snippet-backed usage includes:

- `$vs.util.newMap()`
- `$vs.util.newList()`
- `$vs.util.newHashSet()`
- `$vs.util.equals(...)`
- `$vs.util.ifNull(...)`
- `$vs.util.isNull(...)`
- `$vs.util.isNotNull(...)`
- `$vs.util.mapClone(...)`
- `$vs.dbTools.list(...)`
- `$vs.dbTools.uniqueResult(...)`
- `$vs.dbTools.execute(...)`
- `$vs.dbTools.insert(...)`
- `$vs.dbTools.update(...)`
- `$vs.dbTools.delete(...)`
- `$vs.proc.find(...)`
- `$vs.proc.invoke(...)`
- `$vs.date.getDbDate()`
- `$vs.cache.getBean(...)`
- `$vs.cache.getValue(...)`
- `$vs.sqlHelper.listIn(...)`
- `$vs.sqlHelper.strIn(...)`

## Additional custom methods

### baseTools

- `$vs.baseTools.dbtypeFlag`
- `$vs.baseTools.setGoodsSpec($row, $specName)`
- `$vs.baseTools.isNumber($str)`
- `$vs.baseTools.toCharArray($a)`
- `$vs.baseTools.excelToString($a)`
- `$vs.baseTools.convertToUTF8($a)`
- `$vs.baseTools.isMobile($mobile)`
- `$vs.baseTools.engineFormula($str)`
- `$vs.baseTools.formulaCalc($str)`
- `$vs.baseTools.partition($str)`
- `$vs.baseTools.subList($str)`

Note: the ShowDoc note says `engineFormula` is now effectively replaced in real usage by `$vs.proc.executeScript`, so prefer the newer platform-supported path when the actual execution scenario requires it.

### doubleTools

- `$vs.doubleTools.convertDoubleFormat($d, $dec)`
- `$vs.doubleTools.convertToString($d, $dec)`
- `$vs.doubleTools.expMore($a, $b)`
- `$vs.doubleTools.expGe($a, $b)`
- `$vs.doubleTools.intToDouble($a)`
- `$vs.doubleTools.Mathfloor($a)`
- `$vs.doubleTools.preciseDevCy($a, $b, $scale)`

### dateTools

- `$vs.dateTools.isYdmDate($dateStr)`
- `$vs.dateTools.isHmsDateToString($dateStr)`
- `$vs.dateTools.isDate($dateStr, $patternString)`
- `$vs.dateTools.stringToDate($dateStr, $patten)`
- `$vs.dateTools.dateToString($date, $patten)`
- `$vs.dateTools.dateToDate($date, $patten)`
- `$vs.dateTools.checkMaxG($d1, $d2)`
- `$vs.dateTools.getDay($date)`
- `$vs.dateTools.getBetweenMonths($startDate, $endDate)`
- `$vs.dateTools.getBetweenDays($startDate, $endDate)`

### streamTools

- `$vs.streamTools.groupingBySeparator($separatorChars, $list, $fields)`
- `$vs.streamTools.groupingBy($list, $fields)`
- `$vs.streamTools.groupByToMap($list, $fileName)`
- `$vs.streamTools.getListByField($list, $field)`

## Performance guardrails

- In frontend JS and backend loops, avoid repeated cache fetches.
- If the fetched value is stable, move it outside the loop.
- Reduce queries inside `for` or `#foreach`.
- Reduce process calls inside loops.
- Prefer this loop-safe process pattern:

```velocity
#set($proc = $vs.proc.find(''));
$proc.method();
```

- Avoid `$vs.proc.invoke(...)` in loop-heavy code because it is slower.
- Avoid repeated `$vs.date.getDbDate()` inside loops; compute it once outside.
- When assigning map keys, use string keys instead of numeric keys.

## Backend code types

### Service components

Use a service component when the user says `服务组件`, `前端调用`, `返回给前台`, or describes a frontend request/response flow.

Service component rules:

- The platform provides `$form` and `$result`; do not define them.
- `$form` is the frontend input parameter container.
- `$result` is the fixed return parameter container for the frontend.
- Output only the business body; do not wrap it in `#function`.
- Read request values from `$form`.
- Write response values to `$result` using the result-writing style that best matches the surrounding context.

Template:

```velocity
#set($billNo = $form.get("billNo"));
#if ($vs.util.isNull($billNo))
    $vs.exception.throwException("单据编号不能为空");
#end

#set($data = $vs.util.newMap());
$data.put("billNo", $billNo);
$result.put("data", $data);
```

### Process functions

Use a process function when the user says `过程函数`, `内部复用`, `封装一个方法`, `自定义参数`, or asks for backend code without specifying a type.

Process function rules:

- Define the function with `#function name($arg1, $arg2)`.
- Parameter names and count should come from the requirement.
- A function may return data or only perform work.
- If the function is called inside a loop, prefer `$vs.proc.find(...)` once and then call the method on the process object.

Return-value template:

```velocity
#function getDetailList($billNo)
    #if ($vs.util.isNull($billNo))
        $vs.exception.throwException("单据编号不能为空");
    #end

    #set($sql = "select A.* from T_DETAIL A where A.BILL_NO = #{billNo}");
    #set($where = $vs.util.newMap());
    $where.put("billNo", $billNo);
    #set($detailList = $vs.dbTools.list($sql, $where));
    $detailList;
#end
```

No-return template:

```velocity
#function updateBillStatus($billNo, $status)
    #if ($vs.util.isNull($billNo))
        $vs.exception.throwException("单据编号不能为空");
    #end

    #set($data = $vs.util.newMap());
    $data.put("STATUS", $status);
    #set($where = $vs.util.newMap());
    $where.put("BILL_NO", $billNo);
    $vs.dbTools.update("T_BILL", $data, $where);
#end
```

## Temporary table templates

Use temporary tables when the user says `临时表`, `中间表`, or describes a flow that first stores intermediate data and then processes it.

Temporary table rules:

- Put temporary table creation in `#function createTemporaryTable()`.
- Use `$vs.dbTools.createTempTable(...)`.
- Use backticks for multi-line `CREATE TEMPORARY TABLE` SQL.
- Name temporary tables with uppercase underscore style and the `_TMP` suffix.
- Define fields with type, `DEFAULT NULL`, and `COMMENT`.
- Do not add primary keys, indexes, or constraints unless requested.
- When there are multiple temporary tables, create them in dependency order inside the same function.

Single temporary table template:

```velocity
#function createTemporaryTable()
    $vs.dbTools.createTempTable(`
        CREATE TEMPORARY TABLE BUSINESS_DATA_TMP (
            ID VARCHAR(100) DEFAULT NULL COMMENT 'ID',
            BILL_DATE DATE DEFAULT NULL COMMENT '业务日期',
            ORG_CODE VARCHAR(8) DEFAULT NULL COMMENT '机构',
            AMOUNT VARCHAR(100) DEFAULT NULL COMMENT '金额'
        )
    `);
#end
```

Multiple temporary table template:

```velocity
#function createTemporaryTable()
    $vs.dbTools.createTempTable(`
        CREATE TEMPORARY TABLE BUSINESS_DATA_TMP (
            ID VARCHAR(100) DEFAULT NULL COMMENT 'ID',
            BILL_DATE DATE DEFAULT NULL COMMENT '业务日期',
            ORG_CODE VARCHAR(8) DEFAULT NULL COMMENT '机构',
            AMOUNT VARCHAR(100) DEFAULT NULL COMMENT '金额'
        )
    `);

    $vs.dbTools.createTempTable(`
        CREATE TEMPORARY TABLE BUSINESS_CALENDAR_TMP (
            CALENDAR_ID bigint DEFAULT NULL COMMENT 'CALENDAR_ID',
            START_DATE VARCHAR(20) DEFAULT NULL COMMENT '中文日期yyyy-MM-dd'
        )
    `);
#end
```

If later logic uses these tables, call `createTemporaryTable()` before inserting or querying:

```velocity
createTemporaryTable();
```

## Tax-inclusive price linkage

Use this template when an inclusive-tax unit price changes and dependent price or amount fields must be recalculated.

Calculation order:

- `$taxrate = tax rate + 1`
- Inclusive amount = inclusive unit price * weight
- Exclusive-tax unit price = inclusive unit price / `$taxrate`
- Exclusive-tax amount = exclusive-tax unit price * weight
- Tax amount = inclusive amount - exclusive-tax amount

Standard template:

```velocity
#set($taxrate = $vs.util.precise($row.GOODS_TAXRATE, 1, '+'));
#set($row.GOODS_INMONEY = $vs.util.precise($row.GOODS_INPRICE, $row.GOODS_WEIGHT, '*', $vs.decimalTools.money_decimalP));
#set($row.GOODS_EXPRICE = $vs.util.precise($row.GOODS_INPRICE, $taxrate, '/', $vs.decimalTools.exprice_decimalP));
#set($row.GOODS_EXMONEY = $vs.util.precise($row.GOODS_EXPRICE, $row.GOODS_WEIGHT, '*', $vs.decimalTools.money_decimalP));
#set($row.GOODS_TAXMONEY = $vs.util.precise($row.GOODS_INMONEY, $row.GOODS_EXMONEY, '-', $vs.decimalTools.money_decimalP));
```

If local-currency fields exist, calculate them from original-currency fields multiplied by the exchange rate. Use unit-price precision for unit prices and money precision for amounts.

Local-currency template:

```velocity
#set($row.LOCAL_INPRICE = $vs.util.precise($row.GOODS_INPRICE, $row.EXCHANGE_RATE, '*', $vs.decimalTools.price_decimalP));
#set($row.LOCAL_INMONEY = $vs.util.precise($row.GOODS_INMONEY, $row.EXCHANGE_RATE, '*', $vs.decimalTools.money_decimalP));
#set($row.LOCAL_EXPRICE = $vs.util.precise($row.GOODS_EXPRICE, $row.EXCHANGE_RATE, '*', $vs.decimalTools.exprice_decimalP));
#set($row.LOCAL_EXMONEY = $vs.util.precise($row.GOODS_EXMONEY, $row.EXCHANGE_RATE, '*', $vs.decimalTools.money_decimalP));
#set($row.LOCAL_TAXMONEY = $vs.util.precise($row.GOODS_TAXMONEY, $row.EXCHANGE_RATE, '*', $vs.decimalTools.money_decimalP));
```

Adapt field names to the user's business fields, but keep the calculation order. Treat `GOODS_TAXRATE` as a decimal tax rate such as `0.13`.

## External HTTP interface template

Use this template when calling an external HTTP interface. This is a generic pattern and must not be tied to any fixed external system.

Rules:

- Wrap the whole call in `#try/#catch/#finally`.
- Build request parameters through a separate method such as `buildRequestParam($form)`.
- Choose the actual `$vs.http.*` method according to the interface document.
- Build `$encode:string`, `$contextType:string`, and `$header:Map<String,String>` according to the interface document.
- Process the raw HTTP response through a separate method such as `handleResponse($httpResult, $form)`.
- Log request time, method path, method name, request payload, response time, and response payload.
- Truncate serialized request and response payloads to 2000 characters before logging.
- Save the interface log in `#finally`.
- If an exception occurs before `LOG_RESPONSE` is set, write the exception message to `LOG_RESPONSE` and throw the exception.

Template:

```velocity
#set($log = $vs.util.newMap());
#set($result = null);
#set($httpResult = null);
#try
    #set($requestParam = buildRequestParam($form));

    $log.put("REQUEST_TIME", $vs.date.getDbDate());
    $log.put("LOG_METHOD", $form.url);
    $log.put("LOG_METHODNAME", $form.methodName);

    #set($baseUrl = "http://example.com");
    #set($url = $baseUrl + $form.url);
    #set($encode = "UTF-8");
    #set($contextType = "application/json");
    #set($header = $vs.util.newMap());
    $header.put("Header-Name", "Header-Value");

    #set($requestStr = $vs.util.toJson($requestParam));
    #if ($vs.util.strLen($requestStr) > 2000)
        #set($requestStr = $vs.util.strLeft($requestStr, 2000));
    #end
    $log.put("LOG_REQUEST", $requestStr);

    #set($httpResult = $vs.http.postBodyWithMapReturn($url, $requestParam, $encode, $contextType, $header));

    $log.put("RESPONSE_TIME", $vs.date.getDbDate());
    #set($responseStr = $vs.util.toJson($httpResult));
    #if ($vs.util.strLen($responseStr) > 2000)
        #set($responseStr = $vs.util.strLeft($responseStr, 2000));
    #end
    $log.put("LOG_RESPONSE", $responseStr);

    #set($result = handleResponse($httpResult, $form));
#catch($e)
    #if ($vs.util.isNull($log.LOG_RESPONSE))
        $log.put("LOG_RESPONSE", $e.getMessage());
        $vs.exception.throwException($e.getMessage());
    #end
#finally
    $vs.proc.invoke("com.golden.bdp.msg.createLog", "insertInterfaceLog", "SYSTEM_INTEFUTURELOG", $log);
#end
return $result;
```

HTTP method selection:

- If the document requires a JSON body with Map parameters, prefer the closest `$vs.http.*` Map-body method such as `$vs.http.postBodyWithMapReturn(...)`.
- If the document requires a string body, prefer the closest string-body method such as `$vs.http.postBodyWithStringReturn(...)`.
- If the document requires a special HTTP method, form submission, file payload, no-return call, or another return shape, choose the closest `$vs.http.*` method by method name and parameter meaning.
- Do not hardcode `$vs.http.postBodyWithMapReturn(...)` when the interface document points to a different method.
- `$encode` is the request character encoding. Use `"UTF-8"` only as the default.
- `$contextType` is the request content type. Use `"application/json"` only as the default.
- `$header` is a `Map<String,String>` and should be filled with one `$header.put(...)` per documented header.

## Code conventions

- Object or string null check: `$vs.util.isNull($obj)`
- List has-data check: `$list.size() > 0`
- If the list may be null, guard it before calling `size()`: `!$vs.util.isNull($list) && $list.size() > 0`
- Map empty check: `$vs.util.isNull($map) || $map.isEmpty()`
- Object comparison: use `$vs.util.equals(...)`, not `==`
- Numeric comparison: may use `==`
- String comparison: use `equals`
- Copy object or map data with `$vs.util.mapClone(...)`, not direct `=`
- Arithmetic operations should default to `$vs.util.precise($num1,$num2,$stropt)`. For Golden business processes, use it for all numeric add/subtract/multiply/divide calculations unless the expression is not really a business-number calculation.
- Numeric calculation should include explicit precision handling
- Keep code aligned and formatted
- Every `#if` should align with its matching `#end`
- When outputting variable values, prefer `$vs.log.info(...)`
- Remove temporary debug output such as `console` and `debugger`
- End each statement line with `;`
- In conditionals, use `||` for or and `&&` for and
- For same-structure row conversion, compare:
  - `$vs.util.mapClone(...)` plus `remove(...)` plus selective overrides
  - explicit field mapping
  Prefer `mapClone(...)` only when the overlap is high and local memory or field-leak risks are acceptable.
- If `mapClone(...)` is used before `batchInsert(...)` or `batchUpdate(...)`, remove all non-target-table keys first.
- When inserting with `$vs.dbTools.insert(...)` or `$vs.dbTools.batchInsert(...)`, do not set primary key fields. The platform insert layer generates them automatically.
- If source data or cloned rows contain primary key fields such as `ID` or `FID`, remove them before insert or batch insert.
- When the target row needs a bill code, generate it from the bill type using `_BILL_TYPE_CODE_`, `BILLTYPE_CODE`, and `$vs.billNoTools.getBillNo($row)`.
- When temporary bill-number helper fields such as `_BILL_TYPE_CODE_` or `BILLTYPE_CODE` are introduced, remove them after calling `$vs.billNoTools.getBillNo(...)` and before `insert(...)`, `batchInsert(...)`, or `batchUpdate(...)`.

## Insert and bill-code templates

Single insert template:

```velocity
#set($row = $vs.util.newMap());
$row.put("FIELD_CODE", $fieldValue);
#set($row._BILL_TYPE_CODE_ = 'BT1198');
#set($row.BILLTYPE_CODE = 'BT1198');
#set($row.LOG_BILLCODE = $vs.billNoTools.getBillNo($row));
$row.remove("ID");
$row.remove("FID");
$row.remove("_BILL_TYPE_CODE_");
$row.remove("BILLTYPE_CODE");
$vs.dbTools.insert("T_LOG", $row);
```

Batch insert template:

```velocity
#set($insertList = $vs.util.newList());
#foreach ($sourceRow in $sourceList)
    #set($row = $vs.util.mapClone($sourceRow));
    $row.remove("ID");
    $row.remove("FID");
    #set($row._BILL_TYPE_CODE_ = 'BT1198');
    #set($row.BILLTYPE_CODE = 'BT1198');
    #set($row.LOG_BILLCODE = $vs.billNoTools.getBillNo($row));
    $row.remove("_BILL_TYPE_CODE_");
    $row.remove("BILLTYPE_CODE");
    $insertList.add($row);
#end
$vs.dbTools.batchInsert("T_LOG", $insertList);
```

Replace `LOG_BILLCODE`, `BT1198`, and target table names with the actual bill-code field, bill type, and table from the requirement.

## SQL and datasource rules

- Empty field check: `SQLTools.isEmpty(B.SCONTRACT_BILLCODE)`
- Non-empty field check: `SQLTools.isNotEmpty(B.SCONTRACT_BILLCODE)`
- Prefer table aliases in datasource SQL
- In SQL text expressions, prefer `SQLTools.*` for cross-database date, string, null, type-conversion, pagination, and row-number operations.
- Use `$vs.sqlTools.*` only for Velocity-side dynamic query condition building; do not mix it up with SQL text helpers named `SQLTools.*`.
- Avoid database-specific functions such as `ifnull`, `nvl`, `date_add`, or `to_date` when a matching `SQLTools.*` helper exists.
- When joining main and detail tables, keep the permission-bearing main table first:

```sql
MAIN_TABLE A
inner join DETAIL_TABLE B on ...
```

Do not reverse that order when data permission behavior depends on the main table.

- Bill numbering rules should start from `1`
- For date-equality filters in datasource SQL, patterns such as `SQLTools.toChar(A.BILL_DATE,'yyyy-MM-dd') = #{BILL_DATE}` are acceptable when the business input is day-granularity text.
- For SQL arithmetic, wrap nullable numeric fields with `SQLTools.isNull(field,0)` before using `+`, `-`, `*`, or `/`.
- For SQL multiplication and division, default to `round(..., 2)` around the result.
- For SQL addition and subtraction, do not force `round(..., 2)` unless the expression is an amount, price, or explicitly needs fixed precision.
- For SQL division, protect against a zero denominator with `case when` or a filtering condition when zero is possible.
- Do not generate `SQLTools.UUID()` for primary keys during normal inserts; the platform insert layer generates primary keys automatically. Use `SQLTools.UUID()` only when the user explicitly requires a database-layer UUID value.
- For "latest row per group" requirements, compare:
  - SQL window functions such as `ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ... DESC)`
  - process-side map/group de-duplication
  Prefer the SQL approach when it stays readable and the grouping key is clear.
- In sync-style processes, a good default structure is:
  - query source rows
  - query target rows
  - build target map keyed by the business identifier
  - decide insert/update/skip
  - batch insert / batch update
- If a target map already stores the full row object, prefer reading additional comparison fields from that row instead of building duplicate maps for each field.
- For update matching, prefer the business-unique key first. Add date or primary-key constraints only when the data model can legitimately contain multiple current rows for the same business key.

## SQL arithmetic templates

Use these templates only inside SQL expressions. Velocity backend calculations still use `$vs.util.precise(...)`.

Addition:

```sql
SQLTools.isNull(A.FIELD1,0) + SQLTools.isNull(A.FIELD2,0)
```

Subtraction:

```sql
SQLTools.isNull(A.IN_MONEY,0) - SQLTools.isNull(A.EX_MONEY,0)
```

Multiplication:

```sql
round(SQLTools.isNull(A.PRICE,0) * SQLTools.isNull(A.QTY,0), 2)
```

Division:

```sql
round(SQLTools.isNull(A.AMOUNT,0) / SQLTools.isNull(A.QTY,0), 2)
```

Safe division:

```sql
case
    when SQLTools.isNull(A.QTY,0) = 0 then 0
    else round(SQLTools.isNull(A.AMOUNT,0) / SQLTools.isNull(A.QTY,0), 2)
end
```

## SQLTools expression templates

Use these templates inside SQL text. See [sqltools-reference.md](sqltools-reference.md) for the complete function list.

Type conversion:

```sql
SQLTools.cast(A.FIELD,int)
```

String concatenation:

```sql
SQLTools.concat(A.YEAR,'-',A.MONTH)
```

Current database date:

```sql
SQLTools.getDate()
```

Date formatting:

```sql
SQLTools.toChar(A.BILL_DATE,'yyyy-MM-dd')
```

Date parsing:

```sql
SQLTools.toDate(#{BILL_DATE},'yyyy-MM-dd')
```

String search and substring:

```sql
SQLTools.instr(A.FIELD,'a')
SQLTools.substr(A.CODE,1,4)
```

Like filters:

```sql
SQLTools.like(A.NAME,#{NAME})
SQLTools.leftLike(A.CODE,'10')
SQLTools.rightLike(A.CODE,'99')
```

Top N:

```sql
select
    SQLTools.top(10) *
from T_TABLE A
```

Row number:

```sql
SQLTools.rowNumber('A.ORG_CODE','A.BILL_DATE DESC')
```

## Trigger wording

This skill should trigger when the user says or strongly implies any of the following:

- `用 golden语法 写`
- `用 golden 写`
- `按 golden语法 输出`
- `按 golden 输出`
- `把这段改成 golden语法`
- `用 Velocity + $vs 风格写`
- `按团队 Velocity 规范写`
- `写服务组件`
- `写过程函数`
- `golden 写后端代码`
- `临时表`
- `中间表`
- `含税单价`
- `无税单价`
- `税额`
- `本币`
- `外部接口`
- `HTTP接口`
- `请求日志`
- `响应日志`

It should also trigger automatically when inspected or scanned file content clearly matches Golden code, even if the user does not name the skill:

- Backend signals: Velocity directives together with `$vs.*`, `$form`, `$result`, `$sqlBean`, or `SQLTools.*` usage.
- Frontend signals: `gUtil`, `$vm`, `selfPage`, platform form/table controls, or recognized page-event scripts such as `onOpen`, `onChange`, `onCheck`, and `onBeforeWinClose`.
- Mixed page exports: route each script by its own execution context; do not assume every `.js` artifact is browser JavaScript.

Do not trigger from generic JavaScript syntax, a lone `SQLTools` string in prose, or an isolated method name without a coherent platform context.
