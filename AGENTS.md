# AGENTS.md — oagentkit/toolname

> 工具名净化原语：规范名/JS 标识符净化/一致性校验——一条单一真相（生产侧派生形态与消费侧挂载必须逐字一致）
> module：`github.com/oagentkit/toolname` · org：[oagentkit = Open Agent Kit](https://github.com/oagentkit)
> 矩阵分层：**tier 0**（基础层：纯标准库、零第三方依赖、零重量级地板）

## 本仓包含

```
`toolname/`   ← 工具名 → 程序内可用标识符的唯一规则（IsJSIdent / Normalize）
```

## 硬规则

### 分层与依赖

- 依赖严格自底向上，禁止反向依赖；本仓**零第三方依赖**（go.mod 无 require，仅标准库）
- 通用微工具统一在 `github.com/oekit/pkg`；本仓新增基础工具前先确认 pkg 里没有
- 本仓 go 指令与矩阵 tier 0 地板一致（1.26.x）——CI 薄调用层用同版本
- 改 module 路径必须同步：全部 import、go.mod、README 安装行

### API 设计

- 导出符号 PascalCase + godoc 注释；包文档放 doc.go
- **规则类原语只此一份**：生产侧与消费侧共用本包，不各自实现第二份
- 生命周期 Stable：只允许 additive 变更（新增导出符号 / 新增方法且给零值默认实现 /
  新增错误值）；改签名、改语义、改默认值、删导出符号都算 breaking
- 归位历史：本包原在 goagent-kernel，v0.58.0 上移 oekit/pkg，v0.59.0 自 oekit/pkg
  归位到本仓；kernel 侧的 api-compat.md / api-lifecycle.yaml 随包迁出后已不含本包

### 测试

- 每条规则都有对应用例；边界形态（数字开头、前导非法字符、全非法、撞名）必须各自钉住

### 发版顺序

本仓 `CHANGELOG.md` 由 `matrix-tools/scripts/gen_changelogs.py` 从 git 历史生成，
**不要手改**。发版顺序的单一副本见 org 规则仓
[CONTRIBUTING §发版](https://github.com/oagentkit/.github/blob/main/CONTRIBUTING.md#发版)：
**预写待发版段 → 提交 CHANGELOG.md → 在那个提交上打 annotated tag**。
tag 必须落在 CHANGELOG 提交**之后**——下游 `go get` 拿到的是 tag 快照，
快照里的 CHANGELOG.md 若缺自己那一段，发布说明就是残缺的。

## 仓特有纪律

- **规整规则不保证唯一**（`get-logs` 与 `get_logs` 同名）：本包只给规则，集合级判定
  （撞名、重名、注册表）是调用方的语义——调用方必须显式处理，不得默认放行
- **空串是「无法规整」的信号**，不是合法名字：调用方必须显式拒绝，不得当合法名字继续用
- 消费侧与生产侧必须用同一套字符规则：不要在消费侧另写一份「看起来等价」的判定
