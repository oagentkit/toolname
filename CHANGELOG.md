# oagentkit-toolname CHANGELOG

> 本文件由 `matrix-tools/scripts/gen_changelogs.py` 从 git 历史生成，按 tag 切段、取每段内的 conventional commit 渲染。

## [v0.2.0] — 2026-11-23

### 新增：仓面补齐——README/AGENTS 面 + go 指令对齐 tier0 地板 + CI 切共享薄调用层

本仓 v0.1.0 发版时只落了 go.mod / toolname.go / toolname_test.go / LICENSE / 自写 CI：
没有 README、没有 AGENTS、没有 CHANGELOG，也没有 GitHub Release——已发布的仓缺少
「它是什么、怎么用、怎么改、怎么发」的入口面。
- README.md（新）：定位（tier 0）、规整规则表、API、迁移指引（自 oekit/pkg/toolname
  归位，API 逐字一致）、边界
- AGENTS.md（新）：分层与依赖、API 设计、测试、发版顺序、仓特有纪律
- 包注释：修正迁出后失效的仓内相对指针——docs/api-compat.md 与 api-lifecycle.yaml
  随包迁出后已不含本包；tooldisclose / ptc 补明是 goagent-kernel 的包
- go.mod：go 1.27.4 → 1.26.0（对齐矩阵 tier 0 地板；声明 1.27.4 的模块在 1.26
  工具链上直接编译失败）
- .github/workflows/ci.yml：自写 CI → 共享薄调用层（oagentkit/.github 的 go-ci.yml@main，
  go-version 1.26），门禁规则本体只在 org 规则仓改一处

## [v0.1.0] — 2026-11-22

- toolname v0.1.0：工具名净化原语归位 oagentkit

自 goagent-kernel 经 oekit/pkg 两度迁移：概念域是工具治理（消费方=工具披露
链/程序化工具编排链），家住 oagentkit；oekit 是纯基础设施不认识工具。
API 逐字未变。
