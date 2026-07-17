# golden-velocity

`golden-velocity` 是一个 Codex Skill，用来生成和改写符合团队规范的 `golden语法` 代码。

它覆盖两类主要场景：

- 后端 Velocity / 服务脚本：`#set`、`#if`、`#foreach`、`#function`、`$vs.*`、`$form`、`$result`、`$sqlBean`、`SQLTools.*` 等。
- 前台平台 JS / 页面脚本：`gUtil`、`$vm`、`self`、`selfPage`、form/table 控件、按钮、页面事件、弹窗、加载、前台调用服务组件等。

这个 skill 的目标不是输出普通 Java、普通 JavaScript 或泛泛的伪代码，而是尽量贴近团队现有平台写法、ShowDoc 规范和项目里的真实代码风格。

## 主要能力

- 识别并生成后端 Velocity 模板代码，优先使用 `$vs.*` 平台 API。
- 识别并生成前台平台 JS，优先使用 `gUtil`、`$vm`、`self`、`selfPage`、form/table/button 等页面控件 API。
- 支持按执行上下文分流：普通页面事件按前台 JS 写，`beforeSqlSelect` 中出现 `$form`、`$sqlBean`、`$vs.*`、`SQLTools.*` 时按后端 Velocity 写。
- 支持后端两种代码形态：服务组件和过程函数。
- 支持 SQLTools 跨库 SQL 写法，例如 `SQLTools.isNull`、`SQLTools.isEmpty`、`SQLTools.toChar`、`SQLTools.top` 等。
- 支持外部 HTTP 接口调用模板：请求参数封装、请求头封装、`$vs.http.*` 方法选择、响应处理、请求/响应日志、异常处理。
- 支持临时表模板：`#function createTemporaryTable()` + `$vs.dbTools.createTempTable(...)`。
- 支持插入数据和单据号生成规则：不主动处理主键 ID，按单据类型生成单据号。
- 支持含税单价联动计算：含税金额、无税单价、无税金额、税额、本币字段按精度联动。
- 内置性能和代码规范：循环内少查库、少取缓存、少频繁调过程；判空、比较、精度计算、SQL 算术判空等遵循团队规则。
- 当关键业务信息不明确时，先向用户确认，不靠猜。

## 使用方式

在 Codex 中明确提到 `golden` 或 `golden语法` 即可触发，例如：

```text
用 golden 写一个服务组件，前端传客户编码，返回客户信息
```

```text
用 golden 写一个过程函数，传入单据号，返回明细列表
```

```text
用 golden 写一个 SQL 查询，按客户和物料分类汇总金额
```

```text
用 golden 写一个前台 onChange，修改含税单价后联动金额字段
```

```text
用 golden 写一个调用外部接口的方法
```

如果你直接提供一段已有代码，且里面有明显的 Golden 标记，例如 `$vs.*`、`#set`、`$form`、`$result`、`SQLTools.*`、`gUtil`、`$vm`、`selfPage`、form/table 控件等，Codex 也会按这个 skill 的规则来阅读、解释或改写。

## 前后端分流规则

这个 skill 不只按文件后缀判断代码类型，而是按执行上下文和代码标记判断：

- `onCreate`、`onOpen`、`onClick`、`onChange`、`onCheck`、`onUnCheck`、`onAfterLoad`、`onTableReady`、`onDblClickCell`、`onBeforeWinClose` 通常按前台平台 JS 处理。
- `beforeSqlSelect` 如果包含 `$form`、`$sqlBean`、`$vs.*`、Velocity 指令或 `SQLTools.*`，即使文件名像 JS，也按后端 Velocity 处理。
- 前台 JS 使用 `gUtil`、`$vm`、`self`、`selfPage`、form/table 控件。
- 后端 Velocity 使用 `$vs.*`、`$form`、`$result`、`$sqlBean`。
- 如果上下文仍然不明确，应先询问，不混写两套运行时 API。

## 后端规则摘要

- 服务组件用于前端调用，平台固定提供 `$form` 和 `$result`，生成时不额外包 `#function`。
- 过程函数用于内部复用，使用 `#function name($arg1, $arg2)`，参数和返回按需求定义。
- 后端算术统一优先使用 `$vs.util.precise(...)`，并带明确小数位。
- list 有数据判断使用 `$list.size() > 0`；如果可能为空，先用 `$vs.util.isNull(...)` 防护。
- 对象/字符串判空用 `$vs.util.isNull(...)`，对象比较用 `$vs.util.equals(...)`。
- 循环中尽量避免重复查库、重复取缓存、重复调用过程函数。
- 插入数据时不主动设置主键 ID；克隆旧数据插入前清理 `ID`、`FID` 等主键字段。
- 单据号通常通过 `_BILL_TYPE_CODE_`、`BILLTYPE_CODE` 和 `$vs.billNoTools.getBillNo($row)` 生成。

## 前台规则摘要

- 前台判空使用 `gUtil.isNull(...)` / `gUtil.isNotNull(...)`，比较使用 `gUtil.equals(...)`。
- 前台精度计算使用 `gUtil.precise(...)`，不要在浏览器代码里使用 `$vs.util.precise(...)`。
- 前台调用服务组件：同步场景优先 `gUtil.getServerData(...)`，异步场景优先 `gUtil.request(...)`。
- 弹窗、提示、加载、打开页面/窗口、工作流窗口等优先使用平台页面控件 API。
- 表单和表格操作优先使用平台控件方法，例如 `getData()`、`getRow()`、`getSelectRows()`、`setDataValue(...)`、`update(...)` 等。
- 保存逻辑保持单一 `$vm.save(...)` 入口，不把完整保存块复制到多个确认分支里。
- 选择弹窗、脏数据关闭、按钮状态、字段联动等按 `frontend-window-controls.md` 中的模式生成。
- 不凭空发明表格、form、grid 或事件参数；文档和上下文都没有时先询问。

## SQL 规则摘要

- SQL 文本中的跨库函数优先使用 `SQLTools.*`。
- 字段为空判断用 `SQLTools.isEmpty(field)`。
- 字段不为空判断用 `SQLTools.isNotEmpty(field)`。
- SQL 算术字段先用 `SQLTools.isNull(field,0)` 兜底。
- SQL 乘除默认外层使用 `round(..., 2)`。
- 除法要考虑除数为 0，必要时生成 `case when` 防护。
- 主表关联明细表时，主表放在 `inner join` 左侧，避免影响数据权限。
- 普通插入默认不使用 `SQLTools.UUID()` 生成主键，除非用户明确要求数据库层 UUID。

## 目录结构

```text
golden-velocity/
  SKILL.md
  README.md
  agents/
    openai.yaml
  references/
    golden-rules.md
    frontend-page-api.md
    frontend-window-controls.md
    sqltools-reference.md
    vs-service-api.md
```

## 文件说明

- `SKILL.md`：skill 主入口，定义触发条件、核心风格、前后端分流和规则优先级。
- `references/golden-rules.md`：团队 golden 语法详细规范，包含前台、后端、SQL、插入、临时表、外部接口等规则。
- `references/frontend-page-api.md`：API 中心「页面控件」里的 `gUtil` 方法参考。
- `references/frontend-window-controls.md`：项目片段沉淀的前台窗口、表单、表格、按钮、保存流、选择弹窗等模式参考。
- `references/sqltools-reference.md`：SQLTools 跨数据库函数参考。
- `references/vs-service-api.md`：API 中心「服务脚本」里的 `$vs.*` 方法参考。
- `agents/openai.yaml`：用于 Codex/OpenAI 环境识别 skill。

## 安装方式

将本目录放到 Codex skills 目录下：

```bash
~/.codex/skills/golden-velocity
```

如果是从 GitHub 克隆，可以放到：

```bash
git clone <repo-url> ~/.codex/skills/golden-velocity
```

安装后重新打开或刷新 Codex，让 skill 生效。

## 分享方式

可以直接分享整个 `golden-velocity` 目录，也可以打包成压缩包：

```bash
tar --exclude='.DS_Store' --exclude='.git' -czf golden-velocity.tar.gz golden-velocity
```

别人解压后放到自己的 `~/.codex/skills/golden-velocity` 即可使用。

## 注意事项

- 这个 skill 不会自动同步到账号云端；迁移电脑时需要复制目录、GitHub 克隆或解压分享包。
- SQL 文本函数 `SQLTools.*` 和 Velocity 动态查询工具 `$vs.sqlTools.*` 是两类东西，不要混用。
- 前台页面控件 API 和后台 Velocity `$vs.*` API 是两类东西，不要混用。
- 关键业务信息不明确时，应先确认，例如表名、字段名、接口文档、单据类型、匹配键、返回结构、页面控件 ID 等。
- 如果只是安全格式细节，可以做最小合理假设，但要在回答里说明假设。
