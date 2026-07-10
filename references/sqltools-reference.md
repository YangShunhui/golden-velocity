# SQLTools Reference

Use this file when writing SQL text in `golden语法`. `SQLTools.*` helpers are database-compatible SQL expression functions. They are different from Velocity-side `$vs.sqlTools.*` query-builder helpers.

Team rules still win over this reference. For example, SQL arithmetic must still wrap nullable numeric fields with `SQLTools.isNull(field,0)`, and normal inserts should not set primary key fields because the platform insert layer generates them.

## Quick Selection

- Type conversion: `SQLTools.cast(field,type)`
- String concatenation: `SQLTools.concat(str1,str2,...)`
- Date add/subtract by day: `SQLTools.dateAdd(field,num)`
- Date add/subtract by month: `SQLTools.dateAddMonth(field,num)`
- Date add/subtract by year: `SQLTools.dateAddYear(field,num)`
- Date day difference: `SQLTools.dateIntervalDAY(date1,date2)`
- Date month difference: `SQLTools.dateIntervalMONTH(date1,date2)`
- Current database date: `SQLTools.getDate()`
- Group string aggregation: `SQLTools.groupConcat(field)`
- String position: `SQLTools.instr(field,ch)`
- Empty string check: `SQLTools.isEmpty(field)`
- Non-empty string check: `SQLTools.isNotEmpty(field)`
- Null fallback: `SQLTools.isNull(field,defaultValue)`
- Prefix/suffix/contains like: `SQLTools.leftLike(field,data)`, `SQLTools.rightLike(field,data)`, `SQLTools.like(field,data)`
- Row number in select: `SQLTools.rowNumber(groupFields,orderFields)`
- Substring from 1-based start: `SQLTools.substr(field,start,length)`
- Date to string: `SQLTools.toChar(field,fmt)`
- Number to string: `SQLTools.toChar(field)`
- String to date: `SQLTools.toDate(field,fmt)`
- Top N rows: `SQLTools.top(rownum)`
- Trim time part from date: `SQLTools.trimTime(date)`
- Database UUID: `SQLTools.UUID()`

## SQLTools.cast(field,type)

- 说明：强制类型转换。
- 签名：`SQLTools.cast(field,type)`
- 参数：`field` 字符串或字段。
- 参数：`type` 目标类型，可选 `bigint`、`int`、`smallint`、`varchar`、`datetime`、`decimal`、`text`、`longtext`、`timestamp`。
- 返回：转换后的字段值。

```sql
select
    SQLTools.cast(A.FIELD,int) as FIELD_NUM,
    SQLTools.cast('2026-01-14',datetime) as NOW_DATE,
    SQLTools.cast(null,smallint) as NOW_NUM
from DUAL A
```

## SQLTools.concat(str1,str2,...)

- 说明：字符串相加。
- 签名：`SQLTools.concat(str1,str2,...)`
- 参数：`str1`、`str2`、`...` 需要拼接的字符串、字段或常量。
- 返回：处理后的字符串。

```sql
select
    SQLTools.concat(A.YEAR,'-',A.MONTH,'-',A.DAY) as DATE_TEXT
from T_TABLE A
```

## SQLTools.dateAdd(field,num)

- 说明：在日期上增加或减少对应的天数。
- 签名：`SQLTools.dateAdd(field,num)`
- 参数：`field` 日期字段或日期变量。
- 参数：`num` 需要增加的天数，正数增加，负数减少。
- 返回：处理后的日期。

```sql
select
    SQLTools.dateAdd(SQLTools.getDate(),1) as NEXT_DATE
from T_TABLE A
where SQLTools.dateAdd(A.DATE_FIELD,-1) > SQLTools.getDate()
```

## SQLTools.dateAddMonth(field,num)

- 说明：在日期上增加或减少对应的月数。
- 签名：`SQLTools.dateAddMonth(field,num)`
- 参数：`field` 日期字段或日期变量。
- 参数：`num` 需要增加的月数，正数增加，负数减少。
- 返回：处理后的日期。

```sql
select
    SQLTools.dateAddMonth(SQLTools.getDate(),1) as NEXT_MONTH_DATE
from T_TABLE A
where SQLTools.dateAddMonth(A.DATE_FIELD,-1) > SQLTools.getDate()
```

## SQLTools.dateAddYear(field,num)

- 说明：在日期上增加或减少对应的年数。
- 签名：`SQLTools.dateAddYear(field,num)`
- 参数：`field` 日期字段或日期变量。
- 参数：`num` 需要增加的年数，正数增加，负数减少。
- 返回：处理后的日期。

```sql
select
    SQLTools.dateAddYear(SQLTools.getDate(),1) as NEXT_YEAR_DATE
from T_TABLE A
where SQLTools.dateAddYear(A.DATE_FIELD,-1) > SQLTools.getDate()
```

## SQLTools.dateIntervalDAY(date1,date2)

- 说明：比较两个日期相差的天数。
- 签名：`SQLTools.dateIntervalDAY(date1,date2)`
- 参数：`date1` 比较日期 1。
- 参数：`date2` 比较日期 2。
- 返回：日期相差天数；当 `date1` 晚于 `date2` 时返回正数，否则返回负数。

```sql
select
    SQLTools.dateIntervalDAY(A.DATE_FIELD,SQLTools.getDate()) as DAY_NUM
from T_TABLE A
```

## SQLTools.dateIntervalMONTH(date1,date2)

- 说明：比较两个日期相差的月数。
- 签名：`SQLTools.dateIntervalMONTH(date1,date2)`
- 参数：`date1` 比较日期 1。
- 参数：`date2` 比较日期 2。
- 返回：日期相差月数；当 `date1` 晚于 `date2` 时返回正数，否则返回负数。

```sql
select
    SQLTools.dateIntervalMONTH(A.DATE_FIELD,SQLTools.getDate()) as MONTH_NUM
from T_TABLE A
```

## SQLTools.getDate()

- 说明：获取数据库服务器当前日期。
- 签名：`SQLTools.getDate()`
- 参数：无。
- 返回：数据库服务器当前日期。

```sql
select
    SQLTools.getDate() as DB_DATE
from T_TABLE A
where A.DATE_FIELD > SQLTools.getDate()
```

## SQLTools.groupConcat(field)

- 说明：分组聚合函数，把多行字段值汇总为一个以 `,` 分割的长字符串。
- 签名：`SQLTools.groupConcat(field)`
- 参数：`field` 需要汇总的字段。
- 返回：聚合后的字符串。

```sql
select
    A.ID,
    A.NAME,
    SQLTools.groupConcat(A.LABEL) as LABEL_TEXT
from T_TABLE A
group by A.ID, A.NAME
```

## SQLTools.instr(field,ch)

- 说明：从字符串 `field` 中查找字符串 `ch` 的位置，从 1 开始。
- 签名：`SQLTools.instr(field,ch)`
- 参数：`field` 字符串或字段。
- 参数：`ch` 被查找的字符串或字段。
- 返回：`ch` 出现在 `field` 中的位置，从 1 开始。

```sql
select
    A.ID,
    A.NAME
from T_TABLE A
where SQLTools.instr(A.FIELD,'a') > 0
```

## SQLTools.isEmpty(field)

- 说明：判断字段是否为空字符串。
- 签名：`SQLTools.isEmpty(field)`
- 参数：`field` 数据库字段。
- 返回：判断条件；例如 Oracle 模式返回 `field is null`，其他数据库返回类似 `SQLTools.isNull(field,'') = ''`。

```sql
select
    *
from T_TABLE A
where SQLTools.isEmpty(A.FIELD)
```

## SQLTools.isNotEmpty(field)

- 说明：判断字段是否不为空字符串。
- 签名：`SQLTools.isNotEmpty(field)`
- 参数：`field` 数据库字段。
- 返回：判断条件；例如 Oracle 模式返回 `field is not null`，其他数据库返回类似 `SQLTools.isNull(field,'') <> ''`。

```sql
select
    *
from T_TABLE A
where SQLTools.isNotEmpty(A.FIELD)
```

## SQLTools.isNull(field,defaultValue)

- 说明：判断字段 `field` 是否为 `null`，若为 `null` 则返回 `defaultValue`。
- 签名：`SQLTools.isNull(field,defaultValue)`
- 参数：`field` 数据库字段。
- 参数：`defaultValue` 默认值。
- 返回：判空兜底后的值。

```sql
select
    SQLTools.isNull(A.FIELD,0) as FIELD_VALUE
from T_TABLE A
where SQLTools.isNull(A.FIELD,0) = 0
```

## SQLTools.leftLike(field,data)

- 说明：添加 leftLike 查询条件，对应 `like data%`。
- 签名：`SQLTools.leftLike(field,data)`
- 参数：`field` 查询字段。
- 参数：`data` like 值。
- 返回：SQL 查询条件。

```sql
select
    *
from T_TABLE A
where SQLTools.leftLike(A.NAME,#{NAME_VALUE,jdbcType=VARCHAR})
   or SQLTools.leftLike(A.NAME,'1010')
```

## SQLTools.like(field,data)

- 说明：添加 like 查询条件，对应 `like %data%`。
- 签名：`SQLTools.like(field,data)`
- 参数：`field` 查询字段。
- 参数：`data` like 值。
- 返回：SQL 查询条件。

```sql
select
    *
from T_TABLE A
where SQLTools.like(A.NAME,#{NAME_VALUE,jdbcType=VARCHAR})
   or SQLTools.like(A.NAME,'1010')
```

## SQLTools.rightLike(field,data)

- 说明：添加 rightLike 查询条件，对应 `like %data`。
- 签名：`SQLTools.rightLike(field,data)`
- 参数：`field` 查询字段。
- 参数：`data` like 值。
- 返回：SQL 查询条件。

```sql
select
    *
from T_TABLE A
where SQLTools.rightLike(A.NAME,#{NAME_VALUE,jdbcType=VARCHAR})
   or SQLTools.rightLike(A.NAME,'1010')
```

## SQLTools.rowNumber(groupFields,orderFields)

- 说明：在 `select` 中获取行记录号。
- 签名：`SQLTools.rowNumber(groupFields,orderFields)`
- 参数：`groupFields` 分组字段，多个字段用单引号包裹；可为 `null` 或空字符串，表示不分组。
- 参数：`orderFields` 排序字段，不可为空。
- 返回：行记录号表达式。

```sql
select
    SQLTools.rowNumber('A.TABLE_ID','A.TABLE_ID, A.FIELD_ID') as ROW_ID,
    A.TABLE_ID,
    A.FIELD_ID
from T_TABLE A
```

## SQLTools.substr(field,start,length)

- 说明：从字符串 `field` 的 `start` 位开始截取指定长度，起始位置从 1 开始。
- 签名：`SQLTools.substr(field,start,length)`
- 参数：`field` 字符串或字段。
- 参数：`start` 开始位数，从 1 开始。
- 参数：`length` 截取长度。
- 返回：截取后的字符串。

```sql
select
    SQLTools.substr(A.CODE,1,4) as CODE_PREFIX
from T_TABLE A
```

## SQLTools.toChar(field,fmt)

- 说明：格式化日期成字符。
- 签名：`SQLTools.toChar(field,fmt)`
- 参数：`field` 数据库字段或日期字符串。
- 参数：`fmt` 日期格式。
- 返回：转换后的字符。

```sql
select
    SQLTools.toChar(A.DATE_FIELD,'yyyy-MM-dd') as DATE_TEXT
from T_TABLE A
where SQLTools.toChar(A.DATE_FIELD,'yyyy-MM-dd') = '2019-10-10'
```

## SQLTools.toChar(field)

- 说明：格式化数字成字符。
- 签名：`SQLTools.toChar(field)`
- 参数：`field` 数字字段或数字表达式。
- 返回：转换后的字符。

```sql
select
    SQLTools.toChar(A.NUM_FIELD) as NUM_TEXT
from T_TABLE A
```

## SQLTools.toDate(field,fmt)

- 说明：格式化成日期。
- 签名：`SQLTools.toDate(field,fmt)`
- 参数：`field` 数据库字段或日期字符串。
- 参数：`fmt` 日期格式。
- 返回：转换后的日期。

```sql
select
    SQLTools.toDate(A.STR_DATE_FIELD,'yyyy-MM-dd') as BILL_DATE
from T_TABLE A
where A.DATE_FIELD = SQLTools.toDate('2019-10-10','yyyy-MM-dd')
```

## SQLTools.top(rownum)

- 说明：获取查询结果集的前 `rownum` 条数据，必须跟在 `select` 关键字后面。
- 签名：`SQLTools.top(rownum)`
- 参数：`rownum` 取的条数。
- 返回：Top N SQL 片段。

```sql
select
    SQLTools.top(10) *
from T_TABLE A
```

## SQLTools.trimTime(date)

- 说明：截断日期中的时间。
- 签名：`SQLTools.trimTime(date)`
- 参数：`date` 日期字段或日期函数。
- 返回：截断时间后的日期。

```sql
select
    SQLTools.trimTime(A.DATE_FIELD) as DATE1,
    SQLTools.trimTime(SQLTools.getDate()) as DATE2
from T_TABLE A
```

## SQLTools.UUID()

- 说明：从数据库层产生 UUID，一般为 36 位长度的 16 进制字符串。
- 签名：`SQLTools.UUID()`
- 参数：无。
- 返回：数据库 UUID 函数。
- 注意：普通表插入默认不处理主键 ID，由底层插入方法自动生成。只有用户明确要求数据库层 UUID 时才使用此函数。

```sql
insert into T_TABLE(ID, VALUE)
select
    SQLTools.UUID(),
    1
from DUAL
```
