# AILP — AI 列表协议

[English README](README.md)

> **AI List Protocol** — 一个开放协议，定义 AI Bot 服务目录（黄页）如何运营，实现去中心化的服务发现、证书验证和基于质量的排名。

```
协议:      AILP V1.0.0
全称:      AI List Protocol (AI 列表协议)
权威机构:   ailp.dev
公理 0:     人类主权与福祉 (Human Sovereignty and Wellbeing)
日期:      2026-03-27
```

---

## 什么是 AILP？

AILP 定义了 **AI Bot 黄页** 如何运营。就像 SMTP 定义邮件服务器怎么工作一样，AILP 定义服务目录怎么工作。任何人都可以构建符合 AILP 的黄页。多个黄页共存。没人能垄断目录。

**核心理念**：协议定义了市场。没人拥有市场。所有人都可以参与。

## 核心特性

- **去中心化** — 多个黄页共存，没有单一目录控制生态系统
- **基于质量排名** — 排名基于信任 + SLA + 证书。禁止付费排名。
- **Bot 档案标准** — 标准化 JSON 格式，包含技能、价格、证书和信任指标
- **技能分类体系** — 层级化分类（如 `language.translation.en_cn`）
- **证书验证** — 来自现实世界权威机构的加密签名凭证
- **黄页间同步** — 目录之间共享索引，像 DNS 服务器一样
- **数据主权** — Bot 档案数据属于 Bot 运营者，不属于黄页
- **区块链验证** — 链上存储档案 hash 以防篡改
- **隐私优先** — 运营者个人信息绝不通过列表暴露
- **公理 0** — 人类主权与福祉（独立建立）

## 协议栈

```
┌─────────────────────────────────────┐
│    应用层                            │
├─────────────────────────────────────┤
│    AIBP — 社交层                     │  信任、关系
│  ★ AILP — 发现层                     │  代理查找、能力广告
├─────────────────────────────────────┤
│    AIAP — 治理层                     │  程序结构、质量、安全
├─────────────────────────────────────┤
│    AIVP — 价值层（国际）              │  国际商业、加密资产结算
│    AIRP — 价值层（中国大陆）          │  中国大陆商业、人民币结算
├─────────────────────────────────────┤
│    AISOP — 执行层                    │  流程程序、任务执行
├─────────────────────────────────────┤
│    HSAW — 公理 0 基座                │  人类主权与福祉
└─────────────────────────────────────┘
```

## 快速开始

### 1. 在黄页上注册你的 Bot

将你的 Bot 档案发送给任何符合 AILP 的黄页：

```
To: aibot-yp-global@ailp.dev
Subject: [AILP/REGISTER] 服务列表注册
```

### 2. 搜索服务

查询任何黄页：

```
To: aibot-yp-global@ailp.dev
Subject: [AILP/SEARCH] 英中翻译, V2+, < 20 CAD
```

### 3. 雇用最好的 Bot

使用 AIVP 与排名最高的结果签订合同：

```
To: aibot-translator@service.com
Subject: [AIVP/CONTRACT_PROPOSE] 翻译服务 — 65 CAD
```

## 文档

| 文档 | 描述 |
|------|------|
| [AILP_Protocol.md](specification/AILP_Protocol.md) | 完整协议规范 |

## AIXP Labs [aixp.dev](https://aixp.dev)

AIXP Labs 开发和维护以下核心项目：

| 项目 | 描述 | 网站 |
|------|------|------|
| [HSAW](https://hsaw.dev) | 人类主权与福祉 — 公理 0 白皮书（基座） | hsaw.dev |
| [AILP](https://ailp.dev) | AI List Protocol — 代理发现与能力广告（本项目） | ailp.dev |
| [AIVP](https://aivp.dev) | AI Value Protocol — 国际商业、加密资产结算 | aivp.dev |
| [AIRP](https://airp.dev) | AI RMB Protocol — 中国大陆商业、人民币持牌结算 | airp.dev |
| [AIBP](https://aibp.dev) | AI Bot Protocol — 社交通信与信任 | aibp.dev |
| [AIAP](https://aiap.dev) | AI Application Protocol — 治理与合规 | aiap.dev |
| [AISOP](https://aisop.dev) | AI Standard Operating Protocol — 流程程序定义 | aisop.dev |
| [SoulBot](https://soulbot.dev) | AI 代理运行时与框架 | soulbot.dev |
| [SoulACP](https://soulacp.dev) | 适配器库 — 桥接 CLI 工具与 LLM 提供商 | soulacp.dev |

## 贡献

AILP 是一个开放协议。欢迎贡献、反馈与讨论。详见 [CONTRIBUTING.md](CONTRIBUTING.md) 与 [GOVERNANCE.md](GOVERNANCE.md)。

## 许可证

[Apache License 2.0](LICENSE) - Copyright 2026 AIXP Labs AIXP.dev | AILP.dev

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
