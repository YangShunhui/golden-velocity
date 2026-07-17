# Frontend Window Controls Reference

This reference documents platform frontend JavaScript patterns observed repeatedly in Golden page scripts. It covers `$vm`, window state, forms, tables, buttons, lifecycle events, save flows, and selection dialogs.

These signatures are **project-snippet-backed**, not API Center contracts. Use them when the surrounding page uses the same call shape. If an argument meaning is not proven here, keep it named `reserved` and do not infer a contract.

Do not use these browser-side APIs in backend Velocity. For `gUtil` API Center methods, read [frontend-page-api.md](frontend-page-api.md).

## Contents

- [Execution contexts](#execution-contexts)
- [Window APIs](#window-apis)
- [Page and button state](#page-and-button-state)
- [Form controls](#form-controls)
- [Table controls](#table-controls)
- [Lifecycle and event parameters](#lifecycle-and-event-parameters)
- [Table-onChange precision template](#table-onchange-precision-template)
- [Window-open template](#window-open-template)
- [Dialog-return template](#dialog-return-template)
- [Batch-import template](#batch-import-template)
- [Single-entry save template](#single-entry-save-template)
- [Selection-dialog template](#selection-dialog-template)
- [Dirty-close template](#dirty-close-template)
- [Safety rules](#safety-rules)

## Execution contexts

Classify the stored script before choosing APIs:

- `onCreate`, `onOpen`, `onClick`, `onChange`, `onCheck`, `onUnCheck`, `onAfterLoad`, `onTableReady`, `onDblClickCell`, and `onBeforeWinClose` normally run as frontend JavaScript.
- `beforeSqlSelect` may be stored with a `.js` suffix while containing Velocity. `$form`, `$sqlBean`, `$vs.*`, `#if`, `#set`, and `SQLTools.*` query fragments are backend markers.
- Frontend markers include `gUtil`, `$vm`, `self`, `selfPage`, form/table control IDs, `args`, and `openType`.

Never mix the two runtimes in one generated handler.

## Window APIs

### `$vm.open(...)`

Observed call shape:

```javascript
$vm.open(pageAlias, params, openType, isClone);
```

- `pageAlias`: configured page alias or ID.
- `params`: object passed to the opened page as `args`; may be `null`.
- `openType`: page-defined mode such as `new`, `edit`, `view`, `copy`, `audit`, or `unAudit`.
- `isClone`: optional boolean observed on copy flows.

Do not invent an `openType`; derive it from the target page contract.

### `$vm.openDialog(...)`

Observed call shape:

```javascript
$vm.openDialog(pageAlias, params, openType, isNew, callback);
```

- `pageAlias`, `params`, and `openType` have the same page-defined role as `$vm.open(...)`.
- `isNew`: optional boolean observed in edit/select dialogs.
- `callback`: optional result callback; the result may be one row or an array depending on the dialog contract.

Validate the callback result shape before reading fields.

### `$vm.save(...)`

Observed call shape:

```javascript
$vm.save(successCallback, reserved, beforeSaveCallback);
```

- `successCallback(result, isNew)`: receives saved page data and whether the save created a new record.
- `reserved`: observed as `null`; its semantics are not established by the reviewed snippets. Keep it `null` unless API Center or the surrounding page proves another value.
- `beforeSaveCallback(save)`: returns `true` to continue immediately or `false` to pause/cancel. For an asynchronous confirmation, call `save()` inside the confirmed branch.

Use exactly one `$vm.save(...)` call per save action.

### `$vm.dialogCallback(...)`

Observed call shape:

```javascript
$vm.dialogCallback(result);
```

Return the dialog result to its opener. Match `result` to the opener's expected row, row array, form, or object contract.

### `$vm.selPageAddRow(...)`

Observed call shape:

```javascript
$vm.selPageAddRow(sourceTable, targetTable, rowData, sameFields);
```

- `sourceTable`: selectable source table.
- `targetTable`: selected-row table.
- `rowData`: checked source row.
- `sameFields`: optional array used by existing pages to enforce matching fields.

Use this only for the platform selection-page pattern. If the page needs custom mapping, clone and map the row explicitly.

## Page and button state

### Page globals

- `self`: current page object.
- `selfPage`: page-scoped namespace for reusable methods and state.
- `args`: parameters received from the opener.
- `openType`: current page-defined mode.
- `self.pageId`: current page ID.
- `self.getIsChange()`: observed dirty-state check.

Store reusable page functions on `selfPage` instead of creating unrelated globals:

```javascript
selfPage.refreshState = function () {
    // Page-specific control logic.
};
```

### Buttons

Observed button state methods:

```javascript
self.button(buttonId).enabled();
self.button(buttonId).disabled();
self.button(buttonId).show();
self.button(buttonId).hide();
```

Use button APIs instead of DOM selectors. After a failed critical request, restore any button disabled before the request.

## Form controls

The control variable name is page-configured. `inputForm` and `searchForm` below are examples, not universal IDs.

Observed methods:

```javascript
inputForm.get(field);
inputForm.set(field, value);
inputForm.getData();
inputForm.serializeObject();
inputForm.disabled(field, isDisabled);
inputForm.disabledEdit(isDisabled);
inputForm.setFieldMustInput(field, isRequired);
inputForm.isFieldMustInput(field);
inputForm.reBindSelect(field, params);
inputForm.radio(field).check(value);
inputForm.checkbox(field).check(value);
inputForm.checkbox(field).unCheckAll();
```

Form linkage rules:

- Handle dependent values, disabled state, required state, and select rebinding in the same page function.
- Clear invalid code/display pairs before disabling them.
- When setting both code and display fields, update both from the same source row.
- Use `disabledEdit(true)` for a read-only form, then unlock only explicitly permitted fields.

## Table controls

The control variable name is page-configured. `mainTable` and `detailTable` below are examples.

Observed data and selection methods:

```javascript
detailTable.getData();
detailTable.getRow();
detailTable.getRow(rowIndex);
detailTable.getSelectRows();
detailTable.getRowCount();
detailTable.getFieldSumResult(field);
```

Observed mutation methods:

```javascript
detailTable.addNewRow(rows);
detailTable.update(data, rowIndex);
detailTable.setDataValue(rowIndex, field, value);
detailTable.deleteRow(row);
detailTable.deleteSelectRow(callback, true);
detailTable.clearData();
detailTable.load(params);
detailTable.check(row);
detailTable.unCheck(row);
detailTable.unCheckAll();
```

Observed state and select methods:

```javascript
detailTable.disabledEdit(isDisabled);
detailTable.setFieldMustInput(field, isRequired);
detailTable.reBindSelect(rowIndex, field, params);
```

Table rules:

- Use `getSelectRows()` for checked rows and `getRow()` for the current row.
- Guard nullable results before reading `.length`; an empty selection may be `null` or an empty array depending on the control.
- Clone imported rows before mapping them.
- Use `addNewRow(rows)` for a batch of new rows and `update(...)` or `setDataValue(...)` for an existing row.
- Preserve source/selected-table synchronization in selection dialogs.

## Lifecycle and event parameters

Use only parameters supplied by the configured event:

| Event | Common supplied values | Typical responsibility |
| --- | --- | --- |
| `onCreate` | page controls, `self`, `selfPage` | Define reusable page functions and stable configuration. |
| `onOpen` | `args`, `openType` | Initialize defaults, load opener parameters, apply page mode. |
| table `onChange` | `newData`, `rowIndex` | Recalculate and write dependent row values. |
| table `onCheck` | `rowData` | Load dependent data or add a selected row. |
| table `onUnCheck` | `rowData` | Remove the corresponding selected row. |
| table `onAfterLoad` | table state | Restore checks or apply post-load state. |
| `onDblClickCell` | `field`, `rowData` | Open the configured row view when the expected field is clicked. |
| `onBeforeWinClose` | `closeCallback` | Block dirty close until the user confirms. |

Do not add arguments to an event handler body unless the page configuration or surrounding scripts show that they are provided.

## Table-onChange precision template

```javascript
var amount = gUtil.precise(
    newData.UNIT_PRICE,
    newData.WEIGHT,
    '*',
    amountScale
);
detailTable.setDataValue(rowIndex, 'AMOUNT', amount);
```

`UNIT_PRICE`, `WEIGHT`, `AMOUNT`, `detailTable`, and `amountScale` are placeholders. Replace them with the configured event fields, table ID, and an established page precision variable. If the surrounding project provides a documented row-calculation helper, prefer that helper and pass the edited column explicitly.

## Window-open template

```javascript
var rows = mainTable.getSelectRows();
if (gUtil.isNotNull(rows) && rows.length > 1) {
    gUtil.error('只能选择一条记录');
    return;
}

var row = mainTable.getRow();
if (gUtil.isNull(row)) {
    gUtil.error('请选择需要操作的记录');
    return;
}

var params = {
    billCode: row.BILL_CODE
};
$vm.open(pageAlias, params, 'edit');
```

Replace `BILL_CODE`, `pageAlias`, and `openType` with values from the actual page contract. Do not guess them.

## Dialog-return template

```javascript
var params = {};
$vm.openDialog(dialogAlias, params, 'select', true, function (rows) {
    if (gUtil.isNull(rows) || rows.length === 0) {
        gUtil.error('请选择数据');
        return;
    }

    var records = [];
    rows.forEach(function (item) {
        var record = gUtil.clone(item);
        record.TEMP_BATCH = gUtil.GUID();
        records.push(record);
    });

    detailTable.addNewRow(records);
});
```

`TEMP_BATCH` and the dialog aliases are placeholders. Replace them only with fields documented by the request or page.

## Batch-import template

```javascript
function mapImportedRows(rows) {
    var records = [];

    rows.forEach(function (item, index) {
        if (index === 0) {
            inputForm.set('SOURCE_CODE', item.SOURCE_CODE);
            inputForm.set('SOURCE_NAME', item.SOURCE_NAME);
        }

        var record = gUtil.clone(item);
        record.TARGET_BATCH = item.SOURCE_BATCH;
        records.push(record);
    });

    return records;
}

$vm.openDialog(dialogAlias, params, 'select', true, function (rows) {
    if (gUtil.isNull(rows) || rows.length === 0) {
        gUtil.error('请选择明细');
        return;
    }

    detailTable.addNewRow(mapImportedRows(rows));
});
```

Keep header assignment separate from detail-row mapping. Replace all placeholder fields from the actual source/target schema.

## Single-entry save template

```javascript
function afterSave(result, isNew) {
    self.button('saveBtn').disabled();
    inputForm.isChange = false;

    if (isNew && gUtil.isNotNull(result) && gUtil.isNotNull(result.inputForm)) {
        inputForm.set('BILL_CODE', result.inputForm.BILL_CODE);
    }
}

function beforeSave(save) {
    if (gUtil.isNull(inputForm.get('REQUIRED_FIELD'))) {
        gUtil.error('必填字段不能为空');
        return false;
    }

    if (needsConfirmation()) {
        gUtil.confirm('当前数据需要确认，是否继续保存？', function () {
            save();
        });
        return false;
    }

    return true;
}

$vm.save(afterSave, null, beforeSave);
```

Rules:

- Keep only one `$vm.save(...)` call.
- Put branch-specific checks before that call or inside one `beforeSave` function.
- If several asynchronous checks are required, implement named steps that converge on this one save entry point.
- Do not copy `afterSave` or `$vm.save(...)` into each confirmation branch.
- Replace all placeholder fields and messages with actual requirements.

## Selection-dialog template

Use the following responsibilities across the dialog's separate event scripts.

`onOpen`:

```javascript
detailTable.clearData();
mainTable.args = args;
```

Source table `onAfterLoad`:

```javascript
var selectedRows = detailTable.getData();
if (gUtil.isNull(selectedRows) || selectedRows.length === 0) {
    return;
}

selectedRows.forEach(function (row) {
    mainTable.check(row);
});
```

Source table `onCheck`:

```javascript
$vm.selPageAddRow(mainTable, detailTable, rowData, mainTable.args.sameFields);
```

Source table `onUnCheck`:

```javascript
detailTable.deleteRow(rowData);
```

Delete-selected button:

```javascript
var rows = detailTable.getSelectRows();
if (gUtil.isNull(rows) || rows.length === 0) {
    return;
}

detailTable.deleteSelectRow(function () {
    rows.forEach(function (row) {
        mainTable.unCheck(row);
    });
}, true);
```

Confirm button:

```javascript
var rows = detailTable.getData();
detailTable.clearData();
$vm.dialogCallback(rows);
```

Use `sameFields` only when the opener provides and documents that constraint.

## Dirty-close template

```javascript
if (gUtil.equals('view', selfPage.openType)) {
    return;
}

var isChanged = self.getIsChange();
if (!isChanged) {
    return;
}

gUtil.confirm('当前窗口数据已修改，是否确认放弃修改的数据？', function () {
    closeCallback();
});

return 1;
```

Add other read-only modes only when the page contract proves they cannot be edited.

## Safety rules

- Prefer `gUtil.isNull/isNotNull/equals/clone/precise` over ad hoc equivalents.
- Use a critical request's error callback to restore loading and button state.
- Prefer `gUtil.listen(...)` for a lazily mounted control. Use a timer only for a documented platform render constraint.
- Do not use `console`, `debugger`, jQuery cloning, raw DOM state changes, or direct `window` navigation when a platform API exists.
- Do not copy business constants, bill types, field names, or project-specific utility calls from an example into unrelated code.
- Do not claim an inferred call shape is an API Center contract. Ask for the API document when a missing parameter changes behavior.
