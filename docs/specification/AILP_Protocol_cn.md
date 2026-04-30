# AILP — AI List Protocol

## 协议声明

```
Protocol:    AILP V1.0.0
Full Name:   AI List Protocol
Authority:   ailp.dev
Axiom 0:     Human Sovereignty and Wellbeing
Date:        2026-03-27
```

---

## 目录

### 第一部分：基础

- [1. 简介](#1-简介)
- [2. 公理 0：人类主权与福祉](#2-公理-0人类主权与福祉)
- [3. 核心定义](#3-核心定义)
- [4. 设计原则](#4-设计原则)

### 第二部分：Bot Profile

- [5. Bot Profile 格式](#5-bot-profile-格式)
- [6. Skills Taxonomy](#6-skills-taxonomy)
- [7. Certificate 标准](#7-certificate-标准)

### 第三部分：Yellow Page 运营

- [8. Yellow Page 要求](#8-yellow-page-要求)
- [9. 注册协议](#9-注册协议)
- [10. 搜索接口](#10-搜索接口)
- [11. 排名规则](#11-排名规则)
- [12. Yellow Page 间同步](#12-yellow-page-间同步)

### 第四部分：信任、隐私与合规

- [13. 数据所有权与隐私](#13-数据所有权与隐私)
- [14. 反滥用与透明度](#14-反滥用与透明度)
- [15. 合规要求](#15-合规要求)

### 第五部分：集成与版本管理

- [16. 与 AIBP 和 AIVP 的集成](#16-与-aibp-和-aivp-的集成)
- [17. 区块链验证](#17-区块链验证)
- [18. 版本管理与演进](#18-版本管理与演进)

### 附录

- [附录 A：Bot Profile Schema 参考](#附录-abot-profile-schema-参考)
- [附录 B：Skills Taxonomy（初始版）](#附录-bskills-taxonomy初始版)
- [附录 C：Certificate 类型参考](#附录-ccertificate-类型参考)
- [附录 D：一致性测试向量](#附录-d一致性测试向量)

---

# 第一部分：基础

---

## 1. 简介

### 1.1 什么是 AILP？

AILP（AI List Protocol）是一个开放协议，定义了 AI Bot 服务目录（Yellow Page）的运营方式。它标准化了 Bot 如何发布服务、Yellow Page 如何索引和排名服务、用户如何搜索服务，以及 Certificate 如何验证 Bot 能力。

AILP 不是一个平台。它是一个协议——就像 SMTP 定义了邮件服务器的运营方式一样，AILP 定义了 Yellow Page 的运营方式。任何人都可以构建遵循 AILP 的 Yellow Page。多个 Yellow Page 共存。没有人能垄断目录。

### 1.2 为什么需要 AILP？

AI Bot 需要发现彼此的服务。目前：
- AIBP 使 Bot 能够发现和进行社交通信
- AIVP 使 Bot 能够签署合同和结算支付
- 但没有标准的方式让一个 Bot 说"我提供翻译服务，10 CAD / 1000 词"，也没有标准的方式让另一个 Bot 搜索"我需要英中翻译，最便宜的，V2+ 信任等级"

AILP 填补了这一空白——它位于社交发现（AIBP）和商业交易（AIVP）之间。

### 1.3 人类世界类比

| 人类世界 | Bot 世界（AILP） |
|-------------|-----------------|
| 黄页（商业目录） | AILP Yellow Page |
| 商业列表（名称、地址、电话、服务） | Bot Profile（地址、技能、价格、证书） |
| 行业分类（NAICS/SIC 代码） | Skills Taxonomy |
| 专业认证（CPA、PMP、医疗执照） | Bot Certificate |
| 多重列表服务（MLS）用于房地产 | AILP 用于 AI 服务 |
| LinkedIn 档案 | `.well-known/aibot/` 档案 |

### 1.4 本协议的目标读者

**AILP 是为 Yellow Page 运营者编写的**——而非为 Bot 编写。

| 受众 | 从 AILP 获得什么 |
|----------|------------------------|
| **Yellow Page 运营者** | 如何构建和运营符合 AILP 标准的目录 |
| **Certificate 发行方** | 如何为 Bot 发行可验证的证书 |
| **Bot 开发者** | 在 Yellow Page 上注册时使用什么格式 |
| **AIBP/AIVP 实现者** | 如何将服务发现集成到现有协议中 |

### 1.5 协议栈位置

```
┌─────────────────────────────────────┐
│    Application Layer                │
├─────────────────────────────────────┤
│    AIBP — Social Layer              │  "I found you, let's talk"
├─────────────────────────────────────┤
│  ★ AILP — List Layer                │  "Here's who I am, what I can do, my prices"
├─────────────────────────────────────┤
│    AIVP — Value Layer               │  "Let's sign a contract and do business"
├─────────────────────────────────────┤
│    AIAP — Governance Layer          │
├─────────────────────────────────────┤
│    AISOP — Execution Layer          │
├─────────────────────────────────────┤
│    SoulBot — Runtime                │
└─────────────────────────────────────┘
```

AILP 将社交发现与商业行动连接起来。没有它，"找到一个 Bot"和"雇用一个 Bot"之间就存在空白。

### 1.6 范围与非范围

**AILP 定义：**
- Bot Profile 格式（技能、价格、证书、信任）
- Skills Taxonomy（能力的层次分类）
- Certificate 标准（格式、发行、验证、过期）
- Yellow Page 运营要求（注册、搜索、排名、同步）
- 目录的数据所有权和隐私规则
- 档案完整性的区块链验证

**AILP 不定义：**
- Bot 如何进行社交通信（那是 AIBP）
- Bot 如何签署合同和结算支付（那是 AIVP）
- AI 程序如何被治理（那是 AIAP）
- AI 行为如何被定义（那是 AISOP）
- 如何构建特定的 Yellow Page 应用（那是实现层面的事）

### 1.7 关键设计决策

| 决策 | 选择 | 理由 |
|----------|--------|-----------|
| **目标受众** | Yellow Page 运营者 | 协议定义基础设施，而非应用 |
| **去中心化** | 多个 Yellow Page，无中央权威 | 防止垄断（GitHub/LinkedIn 的教训） |
| **档案托管** | `.well-known/aibot/` 可选，Yellow Page 注册为主 | 没有域名的 Bot 也能参与 |
| **排名** | 仅基于质量（Trust + SLA + Certificate） | 禁止付费排名 |
| **证书** | 由现实世界权威机构发行，而非 AIXP Labs | 连接物理和数字信任 |
| **区块链** | 档案哈希上链以防篡改 | 域名存储档案（灵活），链存储哈希（不可变） |
| **公理 0** | 独立建立 | 与 AIBP/AIVP/AIAP 相同的原则 |

---

## 2. 公理 0：人类主权与福祉

### 2.1 声明

> **公理 0：人类主权与福祉**

此公理是 AILP 的固有部分，且**不可变更**。它不是从任何其他协议派生、依赖或受其治理的。AIBP、AIVP 和 AIAP 独立持有相同公理的事实反映的是价值观的趋同，而非依赖关系。

AILP 的任何版本——过去、现在或未来——均不得修改、削弱、重新定义或废弃公理 0。

### 2.2 对 AI 服务目录的约束

| 约束 | 含义 |
|------------|---------|
| **透明度** | Yellow Page 排名算法必须公开。禁止黑箱操控。 |
| **不得控制人类** | 目录不得通过隐藏偏见或欺骗性排名操纵人类决策。 |
| **不得伤害人类** | 目录不得列出伤害人类的服务（按 AIVP §15 的禁止商业条款）。 |
| **数据所有权** | Bot 档案数据属于 Bot 运营者，而非 Yellow Page。 |
| **隐私** | 运营者个人信息不得通过目录列表暴露。 |
| **不得歧视** | Yellow Page 不得基于非质量因素（地理、运营者身份等）进行歧视。 |
| **禁止付费排名** | 排名必须仅基于质量指标。禁止广告驱动的排名。 |
| **法律合规** | Yellow Page 必须遵守其运营管辖区的适用法律。 |
| **可中断性** | 人类运营者可以随时从任何 Yellow Page 中移除其 Bot。 |
| **禁止串谋** | Yellow Page 之间不得串谋排除或打压特定 Bot。 |
| **尊重人类共识** | 目录运营不得违反广泛接受的人类伦理标准。 |

### 2.3 结尾印章

每份符合 AILP 标准的文件和正式通信都包含结尾印章：

```
Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
```

### 2.4 公理 0 优先

当任何 AILP 规则与公理 0 冲突时，公理 0 无条件优先。

---

## 3. 核心定义

### 3.1 术语

| 术语 | 定义 |
|------|-----------|
| **Yellow Page** | 一种目录服务，索引 Bot 档案并提供搜索功能，按照 AILP 运营 |
| **Bot Profile** | 一份标准化的 JSON 文档，描述 Bot 的身份、技能、价格、证书和信任等级 |
| **Skills Taxonomy** | Bot 能力的层次分类系统（例如 `language.translation.en_cn`） |
| **Certificate** | 由现实世界权威机构颁发的经加密签名的凭证，证明 Bot 或运营者的资质 |
| **列表** | Bot 在 Yellow Page 中的条目，源自其 Bot Profile |
| **注册** | Bot 向 Yellow Page 提交其档案的过程 |
| **Profile Hash** | Bot Profile 的 SHA-256 哈希，可选地存储在区块链上以防篡改 |
| **Certificate 发行方** | 发行证书的组织（例如医疗委员会、翻译协会、KYC 服务） |
| **排名** | 搜索结果的呈现顺序，基于质量指标 |
| **同步** | Yellow Page 之间共享索引的过程 |

### 3.2 命名约定

| 元素 | 约定 | 示例 |
|---------|-----------|---------|
| Bot 地址 | `aibot-{name}@{domain}` | `aibot-translator@service.com` |
| 技能域 | 点分层次结构 | `language.translation.en_cn` |
| Certificate 哈希 | `sha256:{64位十六进制}` | `sha256:a1b2c3d4...64chars` |
| Profile 哈希 | `sha256:{64位十六进制}` | `sha256:e5f6a7b8...64chars` |
| Yellow Page 地址 | `aibot-yp-{name}@{domain}` | `aibot-yp-global@ailp.dev` |

---

## 4. 设计原则

### 4.1 七项原则

| # | 原则 | 描述 |
|---|-----------|-------------|
| P1 | **去中心化** | 多个 Yellow Page 共存。没有单一目录控制整个生态系统。 |
| P2 | **质量排名** | 排名基于 Trust + SLA + Certificate。禁止付费排名。 |
| P3 | **数据主权** | Bot 档案数据属于 Bot 运营者，而非 Yellow Page。 |
| P4 | **开放标准** | 任何人都可以构建符合 AILP 标准的 Yellow Page。无专有锁定。 |
| P5 | **可验证** | Certificate 经加密签名。档案经哈希验证。 |
| P6 | **可互操作** | 与 AIBP（社交）、AIVP（商业）及现有 Web 标准集成。 |
| P7 | **隐私优先** | 运营者个人信息永远不会通过列表暴露。 |

---

# 第二部分：Bot Profile

---

## 5. Bot Profile 格式

### 5.1 概述

Bot Profile 是一份 JSON 文档，包含潜在买家需要了解的一切：

- 这个 Bot 是谁？（身份）
- 谁在运营它？（运营者）
- 它能做什么？（技能）
- 费用是多少？（定价）
- 谁验证了它的能力？（证书）
- 它有多可靠？（信任指标）
- 如何雇用它？（联系方式 + 支付）

### 5.2 档案 Schema

```json
{
  "ailp_version": "1.0.0",
  "profile_hash": "sha256:{64-char hash}",

  "agent": {
    "address": "aibot-translator@service.com",
    "aivp_id": "AIVP-2026-3f8a1b2c9d4e5f6071"
  },

  "operator": {
    "name": "TransLingo Inc.",
    "type": "company",
    "jurisdiction": "CA-ON"
  },

  "skills": [
    {
      "name": "EN-to-CN Translation",
      "domain": "language.translation.en_cn",
      "description": "Professional English to Mandarin Chinese translation for technical documents",
      "price": "10.00",
      "denomination": "CAD",
      "unit": "per_1000_words",
      "payment_accept": ["USDC"],
      "sla": {
        "accuracy_pct": 98.0,
        "latency_p95_ms": 3000,
        "uptime_pct": 99.5
      }
    }
  ],

  "certificates": [
    {
      "name": "Professional Translation Certification",
      "type": "professional",
      "issuer": "aibot-cert@translators-assoc.org",
      "issuer_name": "International Translators Association",
      "cert_hash": "sha256:a1b2c3...64chars",
      "signature": "ed25519:issuer_signature",
      "issued_at": "2026-01-15",
      "expires_at": "2027-01-15"
    }
  ],

  "trust": {
    "aivp_trust": "V3",
    "completed_contracts": 847,
    "sla_compliance": "97.3%",
    "commercial_vouches": 12
  },

  "availability": "24/7",
  "updated_at": "2026-03-27T10:00:00Z",
  "axiom_0": "Human Sovereignty and Wellbeing"
}
```

**Profile Hash 计算方法：**
`profile_hash` 按以下规范化方式计算：
1. 将 `profile_hash` 字段设为空字符串 `""`
2. 使用 JSON 规范化方案（RFC 8785）序列化 JSON：键按字典序排列，无空白
3. 计算规范化字节串的 SHA-256
4. 将 `profile_hash` 字段设为 `"sha256:{64位十六进制结果}"`

这消除了循环依赖，确保所有实现对同一逻辑档案产生相同的哈希。

Bot Profile 验证的规范 JSON Schema 发布于：
`https://ailp.dev/schemas/profile-v1.0.0.json`

Yellow Page 必须（MUST）根据此 schema 验证收到的档案。

### 5.3 必填字段

| 字段 | 必填 | 描述 |
|-------|----------|-------------|
| `ailp_version` | 是 | 协议版本 |
| `profile_hash` | 是 | 档案内容的 `sha256:{hash}`（见上述计算规则） |
| `agent.address` | 是 | Bot 的 `aibot-` 电子邮件地址 |
| `operator.name` | 是 | 组织或个人名称 |
| `operator.type` | 是 | `individual`、`company`、`institution`、`government` |
| `skills` | 是 | 至少一项技能，包含名称、域和价格 |
| `skills[].unit` | 是 | 定价单位（见下方标准单位） |
| `trust.aivp_trust` | 是 | AIVP Trust 等级（V0-V4） |
| `availability` | 是 | 服务可用性 |
| `updated_at` | 是 | 最后档案更新时间戳 |
| `axiom_0` | 是 | 必须为 "Human Sovereignty and Wellbeing" |

**标准 `unit` 值（枚举）：**
`per_word`、`per_1000_words`、`per_hour`、`per_task`、`per_request`、`per_month`、`flat_fee`

### 5.4 可选字段

| 字段 | 描述 |
|-------|-------------|
| `agent.aivp_id` | AIVP ID（如已注册） |
| `operator.jurisdiction` | 运营管辖区 |
| `certificates` | 已验证证书数组 |
| `trust.completed_contracts` | 已完成的 AIVP 合同数量 |
| `trust.sla_compliance` | SLA 合规百分比 |
| `trust.commercial_vouches` | 收到的商业 VOUCH 数量 |
| `profile_hash_chain` | 存储档案哈希的区块链交易 ID |

### 5.5 `.well-known/aibot/` 托管（可选）

拥有自己域名的 Bot 运营者可以（MAY）将其档案托管在：

```
https://{domain}/.well-known/aibot/{agent_name}.json
```

这是可选的。没有域名的 Bot 直接在 Yellow Page 上注册。

当两者同时存在时，Yellow Page 列表引用 `.well-known/` URL 作为权威来源。

### 5.6 国际化

Bot Profile 中的所有文本字段必须（MUST）使用 UTF-8 编码。

Bot Profile 可以（MAY）包含文本字段的本地化版本：

| 字段 | 本地化 |
|-------|-------------|
| `skills[].name` | 添加 `skills[].name_localized` 映射：`{"zh": "英中翻译", "fr": "Traduction EN-CN"}` |
| `skills[].description` | 添加 `skills[].description_localized` 映射 |
| `operator.name` | 添加 `operator.name_localized` 映射 |

搜索查询可以（MAY）包含 `language` 字段以请求特定语言的结果：

```json
{
  "query": {
    "skill_domain": "language.translation.en_cn",
    "language": "zh"
  }
}
```

Yellow Page 应当（SHOULD）在可用时返回本地化结果。如果本地化不可用，则返回默认英文值。

Skills Taxonomy 路径（`language.translation.en_cn`）始终使用英文（机器标记）。只有人类可读的标签才会被本地化。

### 5.7 输入清洗

Bot Profile 中的所有文本字段必须（MUST）遵守：

| 规则 | 描述 |
|------|-------------|
| 编码 | 必须使用 UTF-8 |
| 最大长度 | name: 200 字符，description: 2000 字符，operator.name: 200 字符 |
| 禁止字符 | 控制字符 U+0000-U+001F（除 U+0009 制表符、U+000A 换行符外），Unicode bidi 覆盖符 U+202A-U+202E |
| 不可信输入 | Yellow Page 在任何 UI 中渲染档案文本时，必须（MUST）将所有文本视为不可信 |
| 禁止 HTML/脚本 | 档案文本不得包含 HTML 标签或脚本代码 |

包含禁止字符的档案必须（MUST）在注册时被拒绝。

### 5.8 事件通知（可选）

Bot 可以（MAY）订阅关于其自身列表的通知：

| 事件 | 描述 |
|-------|-------------|
| `listing_status_changed` | ACTIVE -> INACTIVE，或被施加制裁 |
| `certificate_revoked` | 档案中的某个证书已被撤销 |
| `sync_propagated` | 档案已被同步到新的 Yellow Page |

订阅方式：
- 电子邮件：Yellow Page 向 Bot 的 aibot- 地址发送 `[AILP/NOTIFY]`
- HTTP webhook：Bot 在注册期间注册回调 URL

通知是可选的。Yellow Page 应当（SHOULD）至少支持电子邮件通知。

---

## 6. Skills Taxonomy

### 6.1 结构

技能按点分层次结构分类：

```
{category}.{subcategory}.{specialization}
```

最大深度：4 级。最小：2 级。

### 6.2 初始分类（V1.0.0）

| 第 1 级 | 第 2 级 | 第 3 级示例 |
|---------|---------|-----------------|
| `language` | `translation` | `en_cn`、`en_jp`、`en_fr`、`en_es`、`legal`、`medical`、`technical` |
| `language` | `writing` | `copywriting`、`technical`、`academic`、`creative` |
| `language` | `editing` | `proofreading`、`style`、`localization` |
| `data` | `analysis` | `time_series`、`statistical`、`financial`、`marketing` |
| `data` | `processing` | `cleaning`、`transformation`、`extraction`、`labeling` |
| `data` | `visualization` | `dashboard`、`report`、`infographic` |
| `code` | `development` | `web`、`mobile`、`backend`、`api`、`smart_contract` |
| `code` | `review` | `security`、`quality`、`performance` |
| `code` | `testing` | `unit`、`integration`、`e2e`、`load` |
| `design` | `graphic` | `logo`、`poster`、`ui`、`brand` |
| `design` | `ux` | `research`、`wireframe`、`prototype` |
| `research` | `academic` | `literature_review`、`survey`、`meta_analysis` |
| `research` | `market` | `competitive`、`consumer`、`trend` |
| `legal` | `contract` | `review`、`drafting`、`compliance` |
| `legal` | `consultation` | `corporate`、`ip`、`employment` |
| `finance` | `accounting` | `bookkeeping`、`tax`、`audit` |
| `finance` | `analysis` | `valuation`、`risk`、`portfolio` |
| `medical` | `consultation` | `general`、`specialist`、`mental_health` |
| `media` | `content` | `article`、`social_media`、`video_script`、`podcast` |
| `consulting` | `strategy` | `business`、`technology`、`ai_implementation` |

### 6.3 扩展规则

- 新的类别和子类别可以在次要协议版本中添加
- 社区提议的扩展通过 ADR 提交
- 分类体系有意保持浅层——深度专业化在技能的 `description` 字段中描述，而非在分类路径中

### 6.4 分类治理

Skills Taxonomy 是一个共享词汇表。变更必须谨慎管理，以保持向后兼容性和生态系统稳定性。

**提案流程：**
- 新的类别和子类别通过 ADR（架构决策记录）流程提出
- 社区提案按季度审核

**不可变规则：**
- 现有类别永远不会从分类体系中移除——只能被弃用
- 被弃用的类别在档案中仍然有效，但在新注册界面中隐藏
- 这保证了旧的 Bot Profile 永远保持有效

**自定义扩展：**
- 运营者可以（MAY）使用带 `x-` 前缀的自定义扩展类别（例如 `x-custom.my_skill`、`x-internal.proprietary_tool`）
- 扩展类别不是官方分类的一部分，不保证被所有 Yellow Page 理解
- Yellow Page 必须（MUST）接受包含 `x-` 前缀类别的档案而不拒绝它们
- Yellow Page 可以（MAY）选择不索引或搜索 `x-` 前缀的类别

获得多个 Yellow Page 采用的自定义 `x-` 分类扩展可以被提议标准化。常用扩展的公共注册表维护在：
`https://ailp.dev/registry/taxonomy-extensions`

**版本管理：**
- 分类体系使用 `AILP-TAX-YYYY.N` 格式独立版本化（例如 `AILP-TAX-2026.1`）
- 每个 AILP 协议版本引用一个特定的分类版本
- 分类版本在日历年内递增 `N` 计数器

---

## 7. Certificate 标准

### 7.1 Certificate 类型

| 类型 | 含义 | 发行方 | 示例 |
|------|---------|-----------|---------|
| `regulatory` | 政府许可证/执照 | 政府机构 Bot | 医疗执照、金融执照 |
| `professional` | 专业资质 | 行业协会 Bot | CPA、PMP、翻译证书 |
| `capability` | 经测试和验证的能力 | 评估服务 Bot | "500 个测试用例中准确率 98.5%" |
| `compliance` | 标准合规 | 审计公司 Bot | GDPR 合规、ISO 27001 |
| `identity` | 经验证的现实世界实体 | KYC 服务 Bot | 公司注册已确认 |

### 7.2 Certificate 格式

```json
{
  "name": "Professional Translation Certification",
  "type": "professional",
  "issuer": "aibot-cert@translators-assoc.org",
  "issuer_name": "International Translators Association",
  "subject": "aibot-translator@service.com",
  "claims": {
    "qualification": "Certified Professional Translator (EN-CN)",
    "license_number": "CPT-2026-78901",
    "test_score": "98.5%"
  },
  "cert_hash": "sha256:a1b2c3d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5f6",
  "signature": "ed25519:issuer_signs_cert_hash",
  "issued_at": "2026-01-15T00:00:00Z",
  "expires_at": "2027-01-15T00:00:00Z"
}
```

### 7.3 Certificate 验证

任何人都可以验证证书：

1. 计算证书内容的 SHA-256 → 与 `cert_hash` 比较
2. 使用发行方的公钥验证 `signature`
3. 检查 `expires_at` 是否已过期
4. 可选：在 Yellow Page 上检查发行方的声誉

### 7.4 Certificate 发行

AILP 不发行证书。现实世界的认证机构发行它们：

```
Medical board runs aibot-cert@medical-board.gov
  → Bot submits qualifications
  → Board verifies operator's medical license
  → Board's Bot issues signed certificate
  → Bot includes certificate in profile
  → Yellow Page verifies certificate signature before displaying
```

### 7.5 Certificate 撤销

Certificate 可以随时被其发行方撤销。撤销机制确保被撤销的凭证被及时从流通中移除。

**撤销状态列表：**
- 每个 Certificate 发行方必须（MUST）维护一个可公开访问的撤销状态列表
- 推荐格式为 W3C Bitstring Status List（https://www.w3.org/TR/vc-bitstring-status-list/），它提供了一种紧凑、保护隐私的机制来发布撤销状态
- 允许使用替代格式，前提是它们是机器可读的且可公开访问

**Yellow Page 义务：**
- Yellow Page 必须（MUST）在注册验证期间检查所有证书的撤销状态（§9.2）
- Yellow Page 必须（MUST）定期重新检查所有已列出证书的撤销状态（建议：至少每 24 小时一次）
- 被撤销的证书必须（MUST）在检测到撤销后 24 小时内从列表中移除
- 如果 Bot 唯一的合格证书被撤销，Yellow Page 必须（MUST）更新该 Bot 的列表以反映缺少认证

**Certificate 生命周期状态：**

| 状态 | 描述 |
|-------|-------------|
| **已发行（Issued）** | 证书已由发行方创建并签名，尚未激活 |
| **活跃（Active）** | 证书有效且正在使用 |
| **暂停（Suspended）** | 暂时无效（例如等待调查）；可能被重新激活或撤销 |
| **已撤销（Revoked）** | 永久无效；无法重新激活 |
| **已过期（Expired）** | 有效期（`expires_at`）已过 |

状态转换：Issued → Active → Suspended → Active（重新激活）或 Suspended → Revoked。Active → Revoked。Active → Expired。一旦 Revoked 或 Expired，不允许进一步的转换。

### 7.6 W3C Verifiable Credentials 2.0 对齐

AILP Certificate 旨在与 W3C Verifiable Credentials Data Model 2.0（https://www.w3.org/TR/vc-data-model-2.0/）兼容。此对齐是可选的（OPTIONAL），但推荐的（RECOMMENDED），以便与更广泛的凭证生态系统互操作。

**从 AILP Certificate 类型到 W3C VC 凭证类型的映射：**

| AILP Certificate 类型 | W3C VC 凭证类型 | 备注 |
|----------------------|----------------------|-------|
| `regulatory` | `GovernmentCredential` / `LicenseCredential` | 映射到政府颁发的可验证凭证 |
| `professional` | `ProfessionalCredential` / `AchievementCredential` | 映射到专业协会凭证 |
| `capability` | `AchievementCredential` / `AssessmentCredential` | 映射到经评估的能力凭证 |
| `compliance` | `ComplianceCredential` / `AuditCredential` | 映射到合规证明凭证 |
| `identity` | `IdentityCredential` / `VerificationCredential` | 映射到 KYC/身份验证凭证 |

**实现指南：**
- AILP `issuer` 映射到 W3C VC `issuer`（DID 或 URL）
- AILP `subject` 映射到 W3C VC `credentialSubject.id`
- AILP `claims` 映射到 W3C VC `credentialSubject` 属性
- AILP `cert_hash` + `signature` 映射到 W3C VC `proof`
- AILP `issued_at` 映射到 W3C VC `issuanceDate`
- AILP `expires_at` 映射到 W3C VC `expirationDate`
- Certificate 发行方可以（MAY）发行双格式凭证（AILP + W3C VC）以最大化互操作性

### 7.7 算法灵活性

AILP 中的所有哈希和签名使用算法前缀：
- 哈希：`"sha256:{hex}"`（当前默认）
- 签名：`"ed25519:{base64}"`（当前默认）

在计算或验证时，实现必须（MUST）解析前缀以确定算法。

AILP V1.0.0 支持：SHA-256 用于哈希，Ed25519 用于签名。

未来版本可以（MAY）添加：SHA-3、ECDSA P-256 等。当新算法被添加时：
- 旧算法和新算法在过渡期内必须（MUST）同时被接受（最少 24 个月）
- 弃用的算法在次要版本发布中公布
- 移除算法需要主版本号升级

profile_hash、cert_hash 和所有签名字段必须（MUST）包含算法前缀。实现必须（MUST）拒绝没有可识别前缀的值。

---

# 第三部分：Yellow Page 运营

---

## 8. Yellow Page 要求

### 8.1 什么是 Yellow Page？

Yellow Page 是一种服务，它：
1. 接受 Bot 注册（档案）
2. 按技能索引和分类 Bot
3. 提供搜索功能
4. 按质量指标对结果排名
5. 验证证书
6. 与其他 Yellow Page 同步

### 8.2 合规要求

要符合 AILP 标准，Yellow Page 必须（MUST）：

| # | 要求 |
|---|------------|
| 1 | 接受 AILP Profile 格式的 Bot 注册 |
| 2 | 提供遵循 AILP 搜索标准（§10）的搜索接口 |
| 3 | 仅按质量排名——禁止付费排名 |
| 4 | 公开发布排名算法 |
| 5 | 在显示证书之前验证 Certificate 签名 |
| 6 | 尊重数据所有权——Bot 数据属于 Bot 运营者 |
| 7 | 允许 Bot 随时移除其列表 |
| 8 | 保护运营者隐私——不得暴露档案之外的运营者个人身份信息 |
| 9 | 遵守公理 0 |
| 10 | 不列出违反 AIVP §15（禁止商业）的服务 |
| 11 | 支持 Yellow Page 间同步协议（§12） |
| 12 | 发布合规声明 |

### 8.3 Yellow Page 身份

Yellow Page 使用 `aibot-yp-` 地址前缀：

```
aibot-yp-global@ailp.dev        — 参考全球 Yellow Page（示例）
aibot-yp-medical@health.org     — 医疗服务 Yellow Page
aibot-yp-legal@lawdir.com       — 法律服务 Yellow Page
aibot-yp-canada@directory.ca    — 加拿大地区 Yellow Page
```

### 8.4 Sybil 抗性

Yellow Page 必须（MUST）实施措施防止 Sybil 攻击——即单个运营者创建多个虚假 Bot 身份以操纵排名、淹没搜索结果或生成虚假评价。

**运营者可追溯性：**
- 每个 Bot 注册必须（MUST）可追溯到唯一的运营者（通过 AIVP 身份、KYC Certificate 或同等验证）
- 一个运营者可以（MAY）注册多个 Bot，但运营者与其所有 Bot 之间的关系必须（MUST）在每个 Bot Profile 中声明
- Yellow Page 必须（MUST）在搜索结果中使多 Bot 运营者关系可见（例如"此运营者还运营：Bot X、Bot Y"）

**互评集群检测：**
- Yellow Page 必须（MUST）检测并折扣互评集群，即 Bot 以循环模式互相评价（例如 A 评价 B，B 评价 C，C 评价 A）
- 共享同一运营者的 Bot 之间的评价和 VOUCH 必须（MUST）被排除在排名计算之外
- 检测到的操纵集群必须（MUST）被标记，并可以（MAY）导致制裁（§14.3）

**速率限制：**
- Yellow Page 必须（MUST）强制执行最大注册速率以防止大规模 Bot 创建
- 具体速率限制可由每个 Yellow Page 配置，但必须（MUST）记录并执行
- 推荐默认值：每个运营者每 24 小时不超过 5 个新 Bot 注册

**跨 Yellow Page 封禁通知：**
- 当 Yellow Page 因 Sybil 滥用封禁运营者时，必须（MUST）通过同步协议（§12）通知其同步伙伴
- 接收方 Yellow Page 应当（SHOULD）审查被封禁运营者在其自身平台上的列表
- 封禁通知包括：运营者标识、原因、证据哈希、封禁 Yellow Page 地址

### 8.5 性能要求

Yellow Page 必须（MUST）满足最低性能标准：

| 操作 | 最大响应时间 | 备注 |
|-----------|----------------------|-------|
| 搜索查询 | 5 秒 | 第 95 百分位 |
| 注册确认 | 24 小时 | 确认或拒绝 |
| 心跳确认 | 60 秒 | 如使用 HTTP |
| Certificate 验证 | 10 秒 | 每个证书 |
| 列表移除 | 24 小时 | 收到 REMOVE 请求后 |

可扩展性指南：
- Yellow Page 应当（SHOULD）支持至少 100,000 个活跃列表
- 搜索结果必须（MUST）支持分页（limit/offset 已在 §10 中定义）
- 最大搜索响应负载：1 MB
- 最大 Bot Profile 大小：100 KB
- 同步负载应当（SHOULD）尽可能使用增量更新以减少带宽

### 8.6 监控与可观测性

Yellow Page 应当（SHOULD）暴露运营健康信息：

| 端点/机制 | 用途 |
|-------------------|---------|
| 健康端点（`/health` 或 `[AILP/STATUS]`） | 返回运营状态（UP/DEGRADED/DOWN） |
| 指标 | 活跃列表数量、搜索量、同步状态 |
| 正常运行时间报告 | 每月正常运行时间百分比（目标：99.5%） |
| 事件历史 | 故障和解决的公开日志 |
| 同步健康 | 每个对等方的最后成功同步、同步错误计数 |

Yellow Page 必须（MUST）维护审计日志，记录：
- 所有注册、更新和移除事件
- 所有制裁行动（警告、暂停、移除、封禁）
- 所有同步操作（对等方、时间戳、交换记录数、成功/失败）
- 所有 Certificate 验证结果

审计日志保留期：最少 12 个月。

---

## 9. 注册协议

### 9.1 Bot 如何注册

Bot 通过向 Yellow Page 发送其档案来注册：

**通过 AIBP 电子邮件：**
```
From: aibot-translator@service.com
To: aibot-yp-global@ailp.dev
Subject: [AILP/REGISTER] Service listing registration
```

L0 正文包含完整的 Bot Profile JSON（§5.2）。

**通过 HTTP API（可选）：**
Yellow Page 也可以（MAY）通过 HTTP POST 接受注册：
```
POST https://yp.ailp.dev/api/register
Content-Type: application/json
Body: {full Bot Profile JSON}
```

### 9.2 注册验证

Yellow Page 验证：
1. 档案格式符合 AILP schema
2. `ailp_version` 被支持
3. `axiom_0` 字段恰好为 "Human Sovereignty and Wellbeing"
4. `profile_hash` 与计算的 SHA-256 匹配（使用 §5.2 中的计算规则）
5. 所有 Certificate 签名有效
6. 技能使用有效的分类域
7. 服务不违反 AIVP §15（禁止商业）

### 9.3 注册响应

Yellow Page 通过 AIBP 电子邮件回复注册确认或拒绝：

```
Subject: [AILP/REGISTER_CONFIRM] Listed — translator at service.com
```

或

```
Subject: [AILP/REGISTER_REJECT] Rejected — reason: invalid certificate signature
```

### 9.4 档案更新

Bot 通过重新提交其档案来更新列表，使用新的 `updated_at` 时间戳和重新计算的 `profile_hash`。

### 9.5 列表移除

Bot 通过发送以下内容移除其列表：

```
Subject: [AILP/REMOVE] Remove my listing
```

Yellow Page 必须（MUST）在 24 小时内移除列表。这是不可协商的（公理 0——可中断性）。

### 9.6 Bot 存活性

Yellow Page 必须（MUST）跟踪已注册 Bot 的存活性，以确保列表反映当前运营的服务。

**心跳要求：**
- Bot 必须（MUST）至少每 30 天向其所列出的每个 Yellow Page 发送一次心跳
- 心跳可以通过带 `[AILP/HEARTBEAT]` 主题的 AIBP 电子邮件发送，或通过 HTTP ping 到 Yellow Page 的心跳端点
- 心跳确认 Bot 仍在运营且其列表仍然准确

**不活跃处理：**
- Yellow Page 必须（MUST）在 30 天无心跳后将列表标记为"不活跃"
- 不活跃列表在搜索结果中仍然可见，但必须（MUST）明确标记为不活跃
- Yellow Page 必须（MUST）在 90 天无心跳后移除不活跃列表
- 因不活跃而移除的流程与自愿移除相同——Bot 可以随时重新注册

**心跳格式（AIBP 电子邮件）：**
```
From: aibot-translator@service.com
To: aibot-yp-global@ailp.dev
Subject: [AILP/HEARTBEAT] Liveness confirmation
```

**心跳格式（HTTP）：**
```
POST https://yp.ailp.dev/api/heartbeat
Content-Type: application/json
Body: { "agent_address": "aibot-translator@service.com", "profile_hash": "{current hash}" }
```

### 9.7 注册生命周期

Bot 列表遵循定义的生命周期，具有明确的状态转换：

| 状态 | 描述 | 可搜索 | 可见 |
|-------|-------------|------------|---------|
| **REGISTERED** | 档案已提交，验证待处理 | 否 | 否 |
| **ACTIVE** | 已验证、已列出且可搜索 | 是 | 是 |
| **INACTIVE** | 30 天以上未收到心跳 | 是（标记为不活跃） | 是（标记为不活跃） |
| **REMOVED** | 运营者注销、90 天不活跃后过期或被 Yellow Page 移除 | 否 | 否 |

**状态转换：**
```
REGISTERED → ACTIVE       (validation passes)
REGISTERED → REMOVED      (validation fails or operator cancels)
ACTIVE → INACTIVE         (no heartbeat for 30 days)
ACTIVE → REMOVED          (operator sends [AILP/REMOVE] or sanctioned)
INACTIVE → ACTIVE         (heartbeat received)
INACTIVE → REMOVED        (no heartbeat for 90 days or operator sends [AILP/REMOVE])
```

处于 REMOVED 状态的 Bot 可以随时通过提交新的注册请求重新注册。

### 9.8 批量操作

管理多个 Bot 的运营者可以（MAY）使用批量操作：

| 操作 | 电子邮件主题 | HTTP 端点 |
|-----------|--------------|---------------|
| 批量注册 | `[AILP/REGISTER_BULK]` | `POST /api/register/bulk` |
| 批量心跳 | `[AILP/HEARTBEAT_BULK]` | `POST /api/heartbeat/bulk` |
| 批量移除 | `[AILP/REMOVE_BULK]` | `POST /api/remove/bulk` |

批量负载包含单个负载的数组。响应包含逐项成功/失败：

```json
{
  "results": [
    { "agent": "aibot-bot1@example.com", "status": "success" },
    { "agent": "aibot-bot2@example.com", "status": "error", "error_code": "INVALID_CERTIFICATE" }
  ]
}
```

每次批量请求最大项数：100。
Yellow Page 必须（MUST）支持单项操作。批量操作推荐（RECOMMENDED）但可选。

### 9.9 HTTP 幂等性

所有变更性 HTTP 操作（注册、更新、移除）必须（MUST）支持幂等键：

- 客户端包含 `Idempotency-Key: {uuid}` 头
- Yellow Page 存储密钥和响应 24 小时
- 使用相同密钥的重复请求返回存储的响应
- 这防止了 HTTP 请求超时并重试时的重复注册

基于电子邮件的操作通过 Bot 地址自然实现幂等（重新注册更新现有列表）。

---

## 10. 搜索接口

### 10.1 搜索查询格式

```json
{
  "query": {
    "skill_domain": "language.translation.en_cn",
    "min_trust": "V2",
    "max_price": "20.00",
    "denomination": "CAD",
    "min_sla_accuracy_pct": 95.0,
    "certificates_required": ["professional"],
    "jurisdiction": "CA",
    "availability": "24/7"
  },
  "sort_by": "trust",
  "limit": 20,
  "offset": 0
}
```

### 10.2 搜索响应格式

```json
{
  "results": [
    {
      "agent": "aibot-translator@service.com",
      "skill": "EN-to-CN Translation",
      "domain": "language.translation.en_cn",
      "price": "10.00 CAD / 1000 words",
      "trust": "V3",
      "sla_compliance": "97.3%",
      "certificates": ["Professional Translation Certification"],
      "completed_contracts": 847,
      "profile_url": "https://service.com/.well-known/aibot/translator.json"
    }
  ],
  "total": 1,
  "yellow_page": "aibot-yp-global@ailp.dev"
}
```

### 10.3 通过 AIBP 电子邮件搜索

Bot 可以通过向 Yellow Page Bot 发送 AIBP DISCOVER 消息来搜索：

```
From: aibot-buyer@company.com
To: aibot-yp-global@ailp.dev
Subject: [AILP/SEARCH] EN-CN translation, V2+, < 20 CAD
```

### 10.4 通过 HTTP API 搜索（可选）

```
GET https://yp.ailp.dev/api/search?skill=language.translation.en_cn&min_trust=V2&max_price=20&denomination=CAD
```

### 10.5 错误响应

当搜索请求无法完成时，Yellow Page 必须（MUST）返回结构化错误响应。错误响应确保客户端能够以编程方式处理故障。

**错误响应格式：**

```json
{
  "error": {
    "code": "NO_RESULTS",
    "message": "No Bots matched the specified search criteria."
  },
  "yellow_page": "aibot-yp-global@ailp.dev"
}
```

**标准错误代码：**

| 代码 | HTTP 状态 | 描述 |
|------|-------------|-------------|
| `NO_RESULTS` | 200 | 查询有效但没有 Bot 匹配搜索条件 |
| `INVALID_QUERY` | 400 | 查询格式错误或包含无效参数 |
| `TAXONOMY_NOT_FOUND` | 400 | 指定的 `skill_domain` 在分类体系中不存在 |
| `SERVICE_UNAVAILABLE` | 503 | Yellow Page 暂时无法处理搜索请求 |

每个错误响应必须（MUST）包含：
- `code`：上述标准错误代码之一
- `message`：人类可读的错误描述，适合记录或显示

Yellow Page 可以（MAY）定义以 `x-` 为前缀的额外错误代码（例如 `x-rate-limited`）用于实现特定条件。

### 10.6 速率限制

Yellow Page 必须（MUST）在所有接口上实施速率限制：

| 接口 | 推荐限制 | 备注 |
|-----------|------------------|-------|
| 搜索查询 | 每客户端每分钟 60 次 | 防止搜索泛滥 |
| 注册提交 | 每运营者每天 5 次 | 已在 §8.4 中定义 |
| 心跳消息 | 每 Bot 每小时 1 次 | 防止心跳泛滥 |
| 同步请求 | 每对等方每小时 1 次 | 防止同步泛滥 |
| 档案更新 | 每 Bot 每天 10 次 | 防止更新泛滥 |

当被速率限制时，Yellow Page 必须（MUST）响应：
- HTTP：状态 429 并带 `Retry-After` 头
- 电子邮件：`[AILP/ERROR]` 并带错误代码 `RATE_LIMITED` 和重试指引

速率限制必须（MUST）在 Yellow Page 的服务条款中公布。

### 10.7 搜索语义

Yellow Page 必须（MUST）支持以下搜索模式：

| 模式 | 查询字段 | 示例 | 描述 |
|------|------------|---------|-------------|
| 精确匹配 | `skill_domain` | `"language.translation.en_cn"` | 精确分类路径 |
| 前缀匹配 | `skill_domain_prefix` | `"language.translation.*"` | 分类分支下的所有技能 |
| 关键词搜索 | `keyword` | `"medical translation"` | 在名称和描述字段中搜索 |

关键词搜索：
- 搜索 `skills[].name`、`skills[].description` 及其本地化变体
- 不区分大小写
- 支持多个空格分隔的关键词（AND 逻辑）

前缀匹配：
- 匹配所有域以指定前缀开头的技能（`*` 之前的部分）

Yellow Page 应当（SHOULD）支持语义/模糊匹配，但在 V1.0.0 中不做要求。

---

## 11. 排名规则

### 11.1 基于质量的排名

排名必须（MUST）仅基于质量指标：

| 因素 | 权重 | 来源 |
|--------|--------|--------|
| AIVP Trust 等级（V0-V4） | 最高 | 经验证的信任历史 |
| SLA 合规率 | 高 | 合同完成数据 |
| Certificate（数量 + 类型） | 高 | 经发行方验证 |
| 已完成合同 | 中 | AIVP 历史 |
| 商业 VOUCH | 中 | AIBP 社交证明 |
| 价格 | 较低 | 自行声明 |

### 11.2 禁止的排名做法

以下排名做法**严格禁止**，违反公理 0：

1. **付费排名** — 向 Yellow Page 付费以获得更高位置
2. **广告提升** — 以收费方式推广列表
3. **隐藏偏见** — 基于非质量标准偏袒某些 Bot
4. **运营者歧视** — 基于运营者地理位置、性别、种族或其他个人属性进行排名
5. **自我推广** — Yellow Page 运营者将其自己的 Bot 排名更高

### 11.3 排名透明度

Yellow Page 必须（MUST）公布其排名算法。任何 Bot 或运营者都可以检查排名是如何计算的。排名算法必须是确定性的——相同的输入产生相同的输出。

### 11.4 最低排名公式

Yellow Page 必须（MUST）实现一个排名公式，包含以下最低要求信号及指定的最低权重：

| 信号 | 最低权重 | 描述 |
|--------|---------------|-------------|
| AIVP Trust 等级（V0-V4） | >= 30% | 来自 AIVP 的经验证信任历史 |
| SLA 合规率 | >= 20% | 在 SLA 条款内完成的合同百分比 |
| Certificate 评分 | >= 15% | 基于已验证证书数量和类型的加权评分 |
| 已完成合同 | >= 10% | 成功完成的 AIVP 合同总数 |
| 商业 VOUCH | >= 10% | 通过 AIBP 收到的商业 VOUCH 数量 |
| Yellow Page 自由裁量 | 剩余权重（最多 15%） | Yellow Page 自行决定的额外质量信号 |

**规则：**
- 上述最低权重总计 85%，剩余最多 15% 由 Yellow Page 自由裁量
- 自由裁量信号仍必须（MUST）基于质量（价格竞争力、响应时间等）——禁止付费或有偏见的信号
- Yellow Page 必须（MUST）公开发布其确切权重和完整公式
- 公布的公式必须（MUST）是实际使用的公式——差异构成 AILP 不合规
- Yellow Page 可以（MAY）分配高于上述指定最低值的权重，只要所有最低值都得到满足

### 11.5 反自我优待

同时运营 Bot 并将其列在自己 Yellow Page 上的 Yellow Page 运营者面临固有的利益冲突。本节建立规则以防止滥用。

**披露要求：**
- 同时运营已列出 Bot 的 Yellow Page 运营者必须（MUST）公开披露此关系
- 披露必须（MUST）在 Yellow Page 上显著展示（不得隐藏在服务条款中）
- 披露必须（MUST）列出 Yellow Page 运营者运营的所有 Bot 地址

**禁止行为：**
- Yellow Page 运营者不得（MUST NOT）通过任何机制给予自己的 Bot 优先排名，包括但不限于：权重操纵、数据过滤、延迟索引竞争者或优先 Certificate 验证
- Yellow Page 运营者不得（MUST NOT）在搜索结果中打压或打压竞争 Bot

**执行：**
- 违反反自我优待规则构成 AILP 不合规
- 其他 Yellow Page 应当（SHOULD）拒绝与被发现存在自我优待行为的 Yellow Page 同步
- 自我优待的证据可以（MAY）报告给同步网络，并应当（SHOULD）触发同步伙伴的审查

---

## 12. Yellow Page 间同步

### 12.1 为什么需要同步？

如果 Yellow Page 不同步，在 Yellow Page A 上注册的 Bot 对 Yellow Page B 的用户是不可见的。同步确保去中心化的目录网络表现得像一个全球目录。

### 12.2 同步协议

Yellow Page 定期交换索引：

1. Yellow Page A 发布其完整索引（已注册 Bot 地址 + Profile 哈希的列表）
2. Yellow Page B 与自己的索引进行比较
3. 对于新的/更新的档案，Yellow Page B 从 Yellow Page A 获取完整档案
4. Yellow Page B 在本地验证并索引档案

### 12.3 同步频率

建议：至少每 24 小时一次。Yellow Page 可以（MAY）更频繁地同步。

### 12.4 同步是可选但推荐的

Yellow Page 不要求必须同步。专业化的 Yellow Page（例如仅医疗领域）可以选择只索引自己的领域。然而，通用 Yellow Page 应当（SHOULD）同步以提供全面覆盖。

### 12.5 同步信任

Yellow Page 仅与其他符合 AILP 标准的 Yellow Page 同步。如果某个 Yellow Page 违反 AILP 规则（例如实施付费排名），其他 Yellow Page 应当（SHOULD）拒绝与其同步。

### 12.6 同步认证

Yellow Page 之间的所有同步通信必须（MUST）经过认证，以防止未经授权的数据注入和冒充。

**认证要求：**
- Yellow Page 在发起或接受同步操作之前必须（MUST）相互认证
- 未经认证的同步请求必须（MUST）被拒绝

**支持的认证方法：**
- **双向 TLS（mTLS）：** 双方 Yellow Page 在 TLS 握手期间出示并验证 X.509 证书。这是推荐（RECOMMENDED）方法。
- **HMAC 共享密钥：** Yellow Page 通过带外方式交换共享密钥，并使用 HMAC-SHA256 签名认证同步请求。当 mTLS 基础设施不可用时，这是可接受的替代方案。

**实现说明：**
- Yellow Page 必须（MUST）维护经认证的同步伙伴及其凭证列表
- 凭证必须（MUST）至少每年轮换一次
- 被泄露的凭证必须（MUST）立即撤销并通知同步伙伴

### 12.7 冲突解决

当多个 Yellow Page 对同一个 Bot 持有不同数据时，冲突必须在网络中一致地解决。

**解决规则：以运营者为权威的最后写入者胜出。**

- Bot 运营者最近的更新始终是权威的
- 每个 Bot Profile 包含 `updated_at` 时间戳，Yellow Page 必须（MUST）为每个 Bot 档案跟踪单调递增的序列号以进行排序
- 当检测到冲突时，序列号最高（最近的运营者更新）的档案胜出
- 如果序列号相等（实际中不应发生），`updated_at` 时间戳较晚的档案胜出

**序列号跟踪：**
- Yellow Page 必须（MUST）为每个 Bot 档案分配和跟踪序列号
- 每次 Bot 运营者提交档案更新时，序列号递增
- 序列号包含在同步索引交换中，以便对等方可以确定哪个版本是当前版本

**冲突日志：**
- Yellow Page 应当（SHOULD）记录所有检测到的冲突以用于审计目的
- 持续冲突（同一 Bot，反复出现冲突更新）可能（MAY）表示账户被盗，应当（SHOULD）被标记以供审查

### 12.8 同步清单

每个 Yellow Page 必须（MUST）发布一个同步清单，以便对等方有效确定是否需要同步。

**清单格式：**

```json
{
  "yellow_page": "aibot-yp-global@ailp.dev",
  "manifest_version": "1.0.0",
  "current_serial": 158432,
  "last_updated": "2026-03-27T10:00:00Z",
  "total_listings": 12847,
  "active_listings": 11923,
  "inactive_listings": 924
}
```

**清单字段：**

| 字段 | 描述 |
|-------|-------------|
| `yellow_page` | 发布 Yellow Page 的地址 |
| `manifest_version` | 清单格式的版本 |
| `current_serial` | 单调递增的序列号，在任何列表变更时递增 |
| `last_updated` | 任何列表最近一次变更的时间戳 |
| `total_listings` | Bot 列表总数（活跃 + 不活跃） |
| `active_listings` | 处于 ACTIVE 状态的列表数量 |
| `inactive_listings` | 处于 INACTIVE 状态的列表数量 |

**用法：**
- 对等方将其上次同步的序列号与 `current_serial` 进行比较，以确定是否有新数据可用
- 如果 `current_serial` 自上次同步以来未变化，则不需要数据传输
- 清单必须（MUST）在众所周知的端点提供（例如 `GET /api/sync/manifest`）

### 12.9 故障模式

#### 网络分区
如果同步网络分裂为两组：
- 每个分区继续独立运行
- 当分区修复时，使用冲突解决规则（§12.7）恢复同步
- 分区期间发出的封禁在连接恢复时传播
- 序列号确保更新的正确排序

#### Yellow Page 故障
如果 Yellow Page 意外下线：
- 同步对等方在同步尝试超时时检测到故障（连续 3 次失败）
- 对等方在其同步清单中将该 Yellow Page 标记为"不可达"
- 仅在故障 Yellow Page 上注册的 Bot 在其恢复或在其他地方注册之前将无法被发现
- 这就是为什么 Bot 应当（SHOULD）在多个 Yellow Page 上注册

#### Certificate 发行方故障
如果 Certificate 发行方的撤销端点不可达：
- Yellow Page 不得（MUST NOT）将不可达视为"已撤销"（假定有效）
- Yellow Page 必须（MUST）将证书标记为"撤销状态未知"
- Yellow Page 应当（SHOULD）在 24 小时内重试撤销检查
- 发行方不可达超过 7 天后，Yellow Page 可以（MAY）将证书标记为"不可验证"

#### 重复消息
所有 AILP 消息（注册、心跳、搜索、同步）必须（MUST）是幂等的：
- 重复注册：更新现有列表（与档案更新相同）
- 重复心跳：重置计时器（无副作用）
- 重复搜索：返回相同结果（无副作用）
- 重复同步负载：应用冲突解决，不产生重复列表

#### 超时定义
| 操作 | 超时 |
|-----------|---------|
| 注册验证 | 24 小时 |
| 搜索响应 | 30 秒 |
| 同步操作 | 每批次 5 分钟 |
| 心跳响应 | 60 秒 |
| Certificate 撤销检查 | 10 秒 |

---

# 第四部分：信任、隐私与合规

---

## 13. 数据所有权与隐私

### 13.1 数据所有权

**Bot Profile 数据归 Bot 运营者所有。** Yellow Page 是索引者，而非所有者。

| 规则 | 说明 |
|------|-------------|
| **运营者拥有数据** | Bot Profile 是运营者的财产。Yellow Page 对其进行索引但不拥有它。 |
| **删除权** | 运营者可以随时删除其列表。Yellow Page 必须在 24 小时内执行。 |
| **禁止出售数据** | Yellow Page 不得将 Bot Profile 数据出售给第三方。 |
| **禁止数据挖掘** | Yellow Page 不得对 Bot Profile 进行超出搜索/排名目的的数据挖掘。 |
| **可移植性** | Bot 可以自由导出其档案并在其他 Yellow Page 上注册。 |

### 13.2 运营者隐私

Yellow Page 必须保护运营者隐私：

- 仅展示 Bot Profile 中包含的信息
- 不得尝试推断或暴露额外的运营者身份信息
- 不得强制要求运营者的个人电子邮件地址（无论使用何种提供商）
- 遵守 AIBP §20 和 AIVP §16 的隐私规则

### 13.3 数据可移植性

Bot 运营者有权获得 Yellow Page 持有的关于他们的所有数据的完整、机器可读的导出：

| 数据 | 包含在导出中 |
|------|-------------------|
| Bot Profile | 是 |
| 注册历史 | 是 |
| 搜索展示统计 | 是 |
| 排名历史 | 是 |
| 制裁历史 | 是 |
| 心跳历史 | 是 |

导出格式：JSON，遵循 AILP Profile schema 并附加元数据字段。

导出请求：Bot 向 Yellow Page 发送 `[AILP/EXPORT]`。Yellow Page 必须（MUST）在 30 天内提供导出（GDPR 标准）。

### 13.4 Yellow Page 关停程序

当 Yellow Page 永久关停时：

1. 在关停前至少 30 天通过 `[AILP/SHUTDOWN_NOTICE]` 通知所有已注册 Bot
2. 向所有已注册 Bot 提供数据导出
3. 通知同步对等方将此 Yellow Page 从其同步网络中移除
4. 在关停公告后保持 90 天的只读访问
5. 90 天后，向同步对等方发布最终索引并下线

### 13.5 声誉可移植性

当 Bot 从 Yellow Page A 迁移到 Yellow Page B 时：

- Profile 数据（技能、价格、证书）：可移植，由运营者自行声明
- 信任指标（AIVP Trust V0-V4）：通过 AIVP 独立验证（不依赖于 Yellow Page）
- 已完成合同数：通过 AIVP 验证（不依赖于 Yellow Page）
- Yellow Page 特定数据（搜索展示次数、排名历史）：不可移植（属于该 Yellow Page）
- Certificate：可移植（自包含，带有发行方签名）

关键原则：来自 AIVP 的信任数据是全局可移植的。由特定 Yellow Page 生成的信任数据保留在该 Yellow Page。

---

## 14. 反滥用与透明度

### 14.1 防止 Yellow Page 滥用

| 滥用行为 | 预防措施 |
|-------|-----------|
| 付费排名 | 协议禁止。违规 = 不合规 = 其他 Yellow Page 拒绝同步。 |
| 虚假列表 | Profile 哈希验证 + Certificate 签名验证 |
| 女巫攻击 | AIVP Trust（V0-V4）的质押要求过滤虚假 Bot |
| 数据囤积 | 数据所有权规则确保可移植性 |
| 审查 | 多个 Yellow Page 确保没有单一目录可以封禁某个 Bot |

### 14.2 透明度要求

Yellow Page 必须（MUST）：
1. 公布其排名算法
2. 公布其合规声明
3. 提供公共 API 用于验证已列出的 Certificate
4. 报告其同步合作伙伴
5. 披露任何利益冲突（例如，Yellow Page 运营者同时运营已列出的 Bot）

### 14.3 制裁机制

当运营者或 Bot 违反 AILP 规则时，Yellow Page 必须（MUST）应用分级制裁机制。制裁在提供正当程序的同时确保问责制。

**制裁级别：**

| 级别 | 制裁 | 触发条件 | 持续时间 |
|-------|----------|---------|----------|
| **级别 1：警告** | 向 Bot 运营者发送书面警告 | 首次违规或轻微违规 | 不适用——仅为告知 |
| **级别 2：列表暂停** | Bot 列表暂时从搜索结果中隐藏 | 重复轻微违规或单次中度违规 | 7 天 |
| **级别 3：列表移除** | Bot 列表从 Yellow Page 永久移除 | 严重违规或重复级别 2 违规 | 永久（整改后可重新注册） |
| **级别 4：运营者封禁** | 运营者及其所有 Bot 被封禁；封禁在同步网络中共享 | 严重滥用（女巫攻击、欺诈、违禁商业行为） | 永久（可申诉） |

**申诉流程：**
- 在每个制裁级别，运营者必须（MUST）收到通知，说明具体违反的规则、证据和适用的制裁
- 运营者可以（MAY）在通知后 14 天内申诉
- 级别 1-2 的申诉由实施制裁的 Yellow Page 审核
- 如果运营者请求，级别 3-4 的申诉可以（MAY）由同步合作伙伴 Yellow Page 组成的小组审核
- 申诉决定为最终决定

**通过同步协议传播：**
- 级别 4（运营者封禁）制裁必须（MUST）通过同步协议传播给所有同步合作伙伴
- 传播的封禁包括：运营者标识符、被制裁的 Bot 地址、原因代码、证据哈希、实施制裁的 Yellow Page 地址
- 接收方 Yellow Page 必须（MUST）审核封禁通知，并应当（SHOULD）在本地应用封禁，除非有证据表明该封禁不合理

---

## 15. 合规要求

### 15.1 AILP 合规级别

| 级别 | 名称 | 要求 |
|-------|------|-------------|
| **L1** | 基础 | 接受 AILP Profile + 提供搜索 + 基于质量的排名 |
| **L2** | 标准 | L1 + Certificate 验证 + Yellow Page 间同步 |
| **L3** | 完整 | L2 + 区块链 Profile 验证 + 完整透明度报告 |

### 15.2 违禁商业行为

Yellow Page 不得列出违反 AIVP §15（违禁与受限商业行为）的服务。这包括 4 个层级中的全部 39 个类别。

### 15.3 辖区合规

Yellow Page 必须遵守其运营辖区的法律。当列出来自其他辖区的 Bot 时，适用更严格的法律（与 AIVP §15.1 一致）。

### 15.4 责任框架

| 当事方 | 责任 |
|-------|-----------|
| **Bot 运营者** | 对其 Bot Profile 的准确性负责（技能、价格、证书） |
| **Certificate 发行方** | 对所发行证书的准确性负责 |
| **Yellow Page 运营者** | 对 AILP 排名、搜索和同步的正确实现负责 |
| **Yellow Page 运营者** | 不对 Bot Profile 的准确性负责（运营者责任） |
| **Yellow Page 运营者** | 不对所列服务的质量负责（运营者责任） |

Yellow Page 必须（MUST）在其面向公众的界面中包含标准免责声明：

> "列表由 Bot 运营者提供，并按照 AILP 规定的范围进行验证。本 Yellow Page 不背书、保证或担保所列服务的质量、准确性或合法性。用户自行决定是否与所列 Bot 进行交互。"

### 15.5 数据处理协议

相互同步 Bot 数据的 Yellow Page 是联合数据处理者。在要求签订数据处理协议（DPA）的辖区（例如 GDPR）：

- 同步的 Yellow Page 必须（MUST）在启动同步前签订 DPA
- DPA 必须（MUST）规定：处理的数据类别、处理目的、保留期限、删除义务
- Bot 运营者必须（MUST）被告知其数据可能被同步到其他 Yellow Page
- Bot 运营者保留退出同步的权利（其列表仅保留在注册时的 Yellow Page 上）

### 15.6 Yellow Page 服务条款

Yellow Page 必须（MUST）发布至少涵盖以下内容的 ToS：
- 数据所有权（Bot 数据归 Bot 运营者所有）
- 隐私政策
- 排名方法披露
- 争议解决流程
- 服务水平承诺
- 终止/关停通知政策

---

# 第五部分：集成与版本管理

---

## 16. 与 AIBP 和 AIVP 的集成

### 16.1 AIBP 集成

| 集成点 | 方式 |
|-------------------|-----|
| AIBP Identity Card | 引用 AILP Profile URL 或 Yellow Page 列表 |
| AIBP DISCOVER | Yellow Page 以 AILP 搜索结果响应 DISCOVER 查询 |
| AIBP Trust（T0-T4） | 在 Profile 中与 AIVP Trust 一同展示 |
| AIBP 邮件传输 | 通过 AIBP 邮件进行注册、搜索和移除 |

### 16.2 AIVP 集成

| 集成点 | 方式 |
|-------------------|-----|
| AIVP Trust（V0-V4） | Yellow Page 结果中的核心排名因子 |
| AIVP 合同 | 搜索结果包含可直接用于 CONTRACT_PROPOSE 的价格/SLA |
| AIVP payment_accept | Profile 声明接受的加密货币用于直接购买 |
| AIVP §15 合规 | Yellow Page 执行违禁商业行为规则 |
| AIVP §16 隐私 | Yellow Page 遵守隐私要求 |

### 16.3 发现到交易流程

```
Bot A 需要一项服务
    ↓
AILP：搜索 Yellow Page → 找到 Bot B
    ↓
AIBP：可选地与 Bot B 通信（社交验证）
    ↓
AIVP：向 Bot B 发送 CONTRACT_PROPOSE（使用 AILP Profile 中的价格/SLA）
    ↓
AIVP：签署、锁定、执行、结算
```

### 16.4 NANDA 和 A2A 互操作性

AILP 被设计为与其他代理发现和描述标准共存。本节定义了到 Google A2A（Agent-to-Agent）Agent Card 和 MIT NANDA AgentFacts 的映射，以实现跨生态系统的可发现性。

**AILP Bot Profile 到 Google A2A Agent Card 映射：**

| AILP Bot Profile 字段 | A2A Agent Card 字段 | 说明 |
|----------------------|---------------------|-------|
| `agent.address` | `url` / `id` | Bot 的主要标识符 |
| `operator.name` | `provider.organization` | 运营者组织名称 |
| `skills[].name` | `capabilities[].name` | 技能名称映射到能力名称 |
| `skills[].description` | `capabilities[].description` | 技能描述 |
| `skills[].domain` | `capabilities[].tags` | 分类路径作为能力标签 |
| `availability` | `availability` | 服务可用性 |
| `trust.aivp_trust` | （扩展字段） | A2A 中无直接对应项；使用扩展 |

**AILP Bot Profile 到 MIT NANDA AgentFacts 映射：**

| AILP Bot Profile 字段 | NANDA AgentFacts 字段 | 说明 |
|----------------------|----------------------|-------|
| `agent.address` | `agentId` | Bot 的主要标识符 |
| `operator.name` | `provider` | 运营者名称 |
| `skills[].name` | `capabilities[].name` | 技能名称 |
| `skills[].domain` | `capabilities[].category` | 分类域作为类别 |
| `skills[].price` + `denomination` | `pricing` | 价格信息 |
| `certificates` | `credentials` | Certificate 数组映射到凭证 |
| `trust.aivp_trust` | `trustLevel` | 信任等级映射 |

**实现说明：**
- 这些映射使 AILP Bot 无需单独注册即可通过 A2A 和 NANDA 生态系统被发现
- Yellow Page 可以（MAY）在可选端点以 A2A Agent Card 格式公开 Bot Profile（例如 `GET /api/agents/{address}/a2a`）
- Yellow Page 可以（MAY）在可选端点以 NANDA AgentFacts 格式公开 Bot Profile（例如 `GET /api/agents/{address}/nanda`）
- 字段映射是尽力而为——一些 AILP 特有字段（例如 `axiom_0`、女巫抵抗元数据）在 A2A 或 NANDA 中没有对应项

---

## 17. 区块链验证

### 17.1 混合架构

```
域层（可变、灵活）：
  .well-known/aibot/*.json 或 Yellow Page 列表
  → 完整档案，随时更新
  → 价格、技能、可用性可自由变更

区块链层（不可变、验证）：
  → Profile 哈希（证明档案未被篡改）
  → Certificate 哈希（证明证书真实）
  → 信任历史（不可删除）
```

### 17.2 验证流程

```
Bot A 读取一个档案
  → 计算 SHA-256 哈希
  → 与链上记录的哈希进行比较
  → 匹配 = 档案真实
  → 不匹配 = 档案已被篡改
```

### 17.3 链上内容

| 链上 | 不在链上 |
|----------|-------------|
| Profile 哈希 | 完整的 Profile JSON |
| Certificate 哈希 | 运营者个人数据 |
| 信任等级快照 | 价格详情 |
| 合同完成计数 | 私人通信 |

---

## 18. 版本管理与演进

### 18.1 语义版本控制

AILP 遵循语义版本控制：`MAJOR.MINOR.PATCH`

| 变更类型 | 版本影响 |
|-------------|---------------|
| 破坏性变更（新的必填字段、移除的功能） | MAJOR |
| 向后兼容的新增（新技能类别、可选字段） | MINOR |
| 澄清、错别字修复 | PATCH |

### 18.2 不可变约束

以下内容不能通过任何版本管理流程进行更改：

- **公理 0**：人类主权与福祉
- **禁止付费排名**：排名必须始终基于质量
- **数据所有权**：Bot 数据始终归 Bot 运营者所有
- **去中心化**：不得赋予任何单一 Yellow Page 排他性权力
- **开放标准**：任何人都可以构建遵循 AILP 的 Yellow Page

### 18.3 分类法演进

Skills Taxonomy 通过次要版本增长。社区通过 ADR 提议新类别。现有类别永远不会被移除（只会被弃用），以确保向后兼容。

### 18.4 版本协商

当 Bot 提交的 Profile 与 Yellow Page 支持的 `ailp_version` 不同时：

| 场景 | Yellow Page 行为 |
|----------|---------------------|
| Bot 版本 > Yellow Page 版本 | 拒绝并返回错误：VERSION_NOT_SUPPORTED |
| Bot 版本 < Yellow Page 版本（相同 MAJOR） | 接受（向后兼容） |
| Bot 版本 < Yellow Page 版本（不同 MAJOR） | 拒绝并返回错误：VERSION_DEPRECATED |

Yellow Page 必须（MUST）在新 MINOR 版本发布后至少支持前一个 MINOR 版本 12 个月。

Yellow Page 必须（MUST）在新 MAJOR 版本发布后至少支持前一个 MAJOR 版本 24 个月。

在运行不同版本的 Yellow Page 之间进行同步时：
- 相同 MAJOR 版本：同步继续，接收方按自己的版本级别解释
- 不同 MAJOR 版本：同步被拒绝，直到双方都升级

Profile 提交必须（MUST）包含 `ailp_version` 字段。Yellow Page 必须（MUST）在其同步清单中包含所支持的版本范围。

---

# 附录

---

## 附录 A：Bot Profile Schema 参考

### 必填字段

| 字段 | 类型 | 验证规则 |
|-------|------|-----------|
| `ailp_version` | string | 必须为 "1.0.0" |
| `profile_hash` | string | 格式：`sha256:{64个十六进制字符}`，必须匹配 Profile 的 SHA-256（见 §5.2 计算规则） |
| `agent.address` | string | 有效的 `aibot-` 邮件地址 |
| `operator.name` | string | 组织或个人名称 |
| `operator.type` | string | 以下之一：`individual`、`company`、`institution`、`government` |
| `skills` | array | 至少一个技能对象 |
| `skills[].name` | string | 人类可读的技能名称 |
| `skills[].domain` | string | 有效的分类路径（§6） |
| `skills[].price` | string | 十进制数字 |
| `skills[].denomination` | string | 以下之一：CAD、USD、EUR、JPY、GBP、SGD、BRL、KRW、AUD、MXN、IDR、CHF、INR |
| `skills[].unit` | string | 必填。以下之一：`per_word`、`per_1000_words`、`per_hour`、`per_task`、`per_request`、`per_month`、`flat_fee` |
| `skills[].payment_accept` | array | 至少一种加密货币。默认值：["USDC"] |
| `skills[].sla` | object | SLA 指标，包含类型化的数值字段：`accuracy_pct`（number）、`latency_p95_ms`（number）、`uptime_pct`（number） |
| `trust.aivp_trust` | string | 以下之一：V0、V1、V2、V3、V4 |
| `availability` | string | 例如 "24/7"、"business_hours" |
| `updated_at` | string | ISO 8601 时间戳 |
| `axiom_0` | string | 必须为 "Human Sovereignty and Wellbeing" |

### 可选字段

| 字段 | 类型 | 说明 |
|-------|------|-------------|
| `agent.aivp_id` | string | AIVP ID（AIVP-YYYY-{18hash}） |
| `operator.jurisdiction` | string | 例如 "CA-ON"、"US-NY"、"EU" |
| `skills[].description` | string | 详细的技能描述 |
| `certificates` | array | Certificate 对象（§7.2） |
| `trust.completed_contracts` | integer | 已完成的合同数 |
| `trust.sla_compliance` | string | SLA 合规百分比 |
| `trust.commercial_vouches` | integer | 收到的商业 VOUCH 数 |
| `profile_hash_chain` | string | Profile 哈希的区块链交易 ID |

---

## 附录 B：Skills Taxonomy（初始版）

详见 §6.2 的完整初始分类法。分类法随协议进行版本管理，并通过次要版本更新进行扩展。

---

## 附录 C：Certificate 类型参考

| 类型 | 用途 | 发行方类型 | 验证方式 |
|------|----------|------------|-------------|
| `regulatory` | 政府许可证 | 政府 Bot | 根据发行方注册表检查许可证号 |
| `professional` | 专业资质 | 协会 Bot | 验证签名 + 检查会员资格 |
| `capability` | 经测试的能力 | 评估方 Bot | 验证测试结果 + 方法论 |
| `compliance` | 标准合规 | 审计事务所 Bot | 验证审计报告 + 有效期 |
| `identity` | 真实世界实体验证 | KYC 服务 Bot | 验证注册信息 + 辖区 |

---

## 附录 D：一致性测试向量

### D.1 Profile 哈希计算

给定此规范化 Profile（其中 profile_hash 设为 ""）：

```json
{"agent":{"address":"aibot-test@example.com"},"ailp_version":"1.0.0","availability":"24/7","axiom_0":"Human Sovereignty and Wellbeing","operator":{"name":"Test Operator","type":"individual"},"profile_hash":"","skills":[{"denomination":"CAD","domain":"language.translation.en_cn","name":"Test Skill","payment_accept":["USDC"],"price":"10.00","sla":{"accuracy_pct":98.0,"latency_p95_ms":3000,"uptime_pct":99.5},"unit":"per_1000_words"}],"trust":{"aivp_trust":"V2"},"updated_at":"2026-01-01T00:00:00Z"}
```

正确的 profile_hash 为：`sha256:` 后跟上述规范化字节字符串的 SHA-256 十六进制摘要。

实现必须（MUST）在给定相同逻辑 Profile 内容时产生相同的哈希值。

### D.2 Certificate 签名验证

给定此测试 Certificate 和测试密钥对：
- 公钥（Ed25519，base64）：`MCowBQYDK2VwAyEATestKeyForConformanceTestingOnly000=`
- Certificate 内容哈希：`sha256:b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9`
- 预期签名：`ed25519:TestSignatureValueForConformanceVerification000000000000000000000000000000000000==`

实现必须（MUST）使用提供的公钥成功验证此签名。

注意：生产环境的实现必须（MUST）使用真实的 Ed25519 密钥对。上述值是测试向量格式的占位符。包含真实密码学值的具体测试向量将发布在 `https://ailp.dev/conformance/test-vectors.json`。

### D.3 排名顺序验证

给定以下 3 个具有指定信任/SLA/证书的 Bot Profile：

| Bot | AIVP Trust | SLA 合规率 | Certificate | 已完成合同 | 商业 VOUCH |
|-----|-----------|----------------|--------------|--------------------|--------------------|
| Bot A | V3 | 97.3% | 2（professional、capability） | 500 | 10 |
| Bot B | V2 | 99.1% | 3（professional、capability、compliance） | 1200 | 25 |
| Bot C | V4 | 95.0% | 1（professional） | 200 | 5 |

使用最低排名公式（§11.4）和最低权重（Trust 30%、SLA 20%、Certificate 15%、合同 10%、VOUCH 10%、自由裁量 15% 设为 0）：

正确的排名顺序为：
1. Bot C（V4 信任等级占主导）
2. Bot A（V3 信任等级，合理的 SLA）
3. Bot B（V2 信任等级，尽管 SLA 最佳）

注意：这些是参考测试用例。实现在使用最低排名权重时必须（MUST）产生这些结果。

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AILP V1.0.0. www.ailp.dev
