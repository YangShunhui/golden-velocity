
# golden-velocity

`golden-velocity` 是一个 Codex Skill，用于生成符合团队规范的 `golden语法` 代码。

它主要面向 Velocity 模板、`$vs` 平台 API、SQLTools 数据库兼容函数，以及团队 ShowDoc 开发规范。使用这个 skill 后，生成代码时会优先遵循团队已有写法，而不是输出普通 Java、JavaScript 或伪代码。

## 主要能力

- 支持 Velocity 模板语法：`#set`、`#if`、`#foreach`、`#function`、`#try/#catch/#finally` 等。
- 优先使用 `$vs.*` 平台方法，例如 `$vs.util`、`$vs.dbTools`、`$vs.http`、`$vs.proc`、`$vs.date` 等。
- 支持 SQLTools 写法，例如 `SQLTools.isNull`、`SQLTools.toChar`、`SQLTools.isEmpty`、`SQLTools.top` 等。
- 内置团队代码规范：判空、比较、精度计算、SQL 写法、循环性能、过程函数调用等。
- 支持后端两种代码形态：服务组件和过程函数。
- 支持外部接口调用模板、临时表模板、插入数据和单据号生成规则。
- 结合 Superpowers 工作流：先计划，再写代码。

## 使用方式

在 Codex 中明确提到 `golden` 或 `golden语法` 即可触发，例如：

```text
用 golden 写一个服务组件
```

```text
用 golden 写一个 SQL 查询
```

```text
用 golden 写一个调用外部接口的方法
```

## 工作流

这个 skill 不会一上来直接写代码。

当你提出 golden 代码类需求时，会先输出计划，确认目标、规则、输出结构和注意事项。

只有当你明确输入：

```text
开始写代码
```

之后，才会根据计划生成最终代码。

## 安装方式

将本仓库放到 Codex skills 目录下：

```bash
~/.codex/skills/golden-velocity
```

目录结构示例：

```text
golden-velocity/
  SKILL.md
  agents/
    openai.yaml
  references/
    golden-rules.md
    sqltools-reference.md
    vs-service-api.md
```

## 文件说明

- `SKILL.md`：skill 主入口，定义触发方式、核心规则和工作流。
- `references/golden-rules.md`：团队 golden 语法详细规范。
- `references/sqltools-reference.md`：SQLTools 函数参考。
- `references/vs-service-api.md`：`$vs.*` 服务脚本 API 参考。
- `agents/openai.yaml`：用于 Codex/OpenAI 环境识别 skill。

## 适用场景

- 编写 Velocity + `$vs` 后端代码。
- 编写服务组件。
- 编写过程函数。
- 编写数据源 SQL。
- 编写临时表处理逻辑。
- 编写外部 HTTP 接口调用。
- 按团队规范改写已有代码。

## 注意事项

- 普通说明类问题可以直接回答。
- 代码类需求默认先计划。
- 执行口令固定为 `开始写代码`。
- SQL 文本函数 `SQLTools.*` 和 Velocity 动态查询工具 `$vs.sqlTools.*` 是两类东西，不要混用。
- 插入数据时默认不处理主键 ID，底层方法会自动生成。
