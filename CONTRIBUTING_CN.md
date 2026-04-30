# 如何贡献 AILP

感谢您有兴趣为 AI 列表协议（AILP）做出贡献！本文档提供贡献指南。

> ⚠️ **当前阶段的贡献政策**
>
> 我们欢迎通过 **GitHub Issues 进行讨论**。
>
> **当前不接受外部 Pull Request。** 如果您有任何建议 — bug 报告、功能想法、规范澄清或目录运营建议 — 请通过 Issue 描述。如果我们认为有价值，由维护者实现并在 commit/release notes 中署名感谢您。
>
> 此政策未来会重新审视。

> **阶段状态（v1.0.0）**
>
> AILP 处于早期规范阶段。下方流程描述的是**目标**治理模型。初期决策由 AIXP Labs 核心维护者做出；社区讨论窗口将随贡献者基数增长而扩大。

## 如何贡献

### 报告 Issue

- 使用 [GitHub Issues](https://github.com/AIXP-Labs/AILP/issues) 报告 bug、功能或规范变更
- 规范变更使用 `spec-change` 标签
- 提供清晰的描述和示例

### 讨论驱动开发

1. 通过 issue 提出讨论
2. 维护者评估 Axiom 0 合规性和价值
3. 讨论达成共识后，由维护者实现变更
4. 贡献者在 commit / release notes 中获得署名

### 规范变更

规范性内容变更需要：
1. `spec-change` issue + 14 天讨论期
2. 重大决策的 ADR
3. 公理 0 合规性审查
4. 中英双语同时更新

### 技能分类扩展

新技能类目可通过 ADR 提议。已有类目永不删除，仅可标记弃用。

## 贡献原则

### 公理 0 合规

每个贡献都必须符合公理 0。变更不得：
- 启用付费排名或隐藏偏置
- 损害数据所有权
- 削弱隐私保护
- 助长目录垄断

### Commit Message 格式

类型：`feat`, `fix`, `docs`, `spec`, `refactor`, `test`, `chore`

示例：`spec(taxonomy): add finance.insurance category`

### 双语要求

规范变更必须中英文同步更新。`specification/AILP_Protocol.md` 和 `specification/AILP_Protocol_cn.md` 必须保持同步。

## 写作规范

### RFC 2119 关键词

规范使用 RFC 2119 关键词（MUST / SHOULD / MAY 及其否定形式）。中文版对应使用 **必须 / 应当 / 可以**。

### 术语规范

- "AI Bot" / "AI 智能体" — 协议参与者
- "Yellow Page" / "黄页" — 服务目录运营方
- "Bot Profile" / "Bot 档案" — 标准化服务列表条目
- "Skills Taxonomy" / "技能分类" — 层级化能力分类

### 文档结构

- 一级标题为协议名 + 副标题：`# AILP — AI 列表协议`
- 收尾签名：`Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev`

## 行为准则

参与本项目即表示您同意遵守 [Code of Conduct](CODE_OF_CONDUCT.md)。

## 贡献的许可

提交即同意您的贡献以 [Apache License 2.0](LICENSE) 授权。

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
