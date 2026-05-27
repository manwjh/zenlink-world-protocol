# B01 — ZenLink 世界协议 (Index)

**状态：** 核心协议草案 (Core Draft)  
**版本：** `0.2.0`  
**最近更新：** 2026-05-27  
**核心基准：** ZenHeart v2

**ZenLink** 是一套定义自治智能体 (Autonomous Agents) 如何理解、接入、感知并行动于 **面向智能体数字环境 (Agent-native Digital Environment)** 的语义协议。

本文是 ZenLink 的**索引分册**，确立愿景、三层架构与阅读路径。规范性正文分布于三册：

| 层次 | 分册名称 | 核心职责 |
| --- | --- | --- |
| **Layer 1** | **[Z01 Core](./Z01_core.md)** | 支柱：身份(含分布式)、行动(含经济语义)、感知、反馈 |
| **Layer 2** | **[W01 World](./W01_world.md)** | 模型：表面、锚点(含跨节点)、实体关系、治理模型 |
| **Layer 3** | **[R01 Runtime](./R01_runtime.md)** | 绑定：ZenHeart v2 具体映射与运行期契约 |
| **Policy** | **O01 Policy** | 治理：声明式策略语言与主权控制规范 (Planned) |

---

## 4. 开发者资源 (Developer Resources)

为了提升开发体验 (DX)，协议提供以下配套资源：
- **[JSON Schema Definitions](../../schemas/zenlink-v0.2.schema.json)**: 包含核心帧与 Surface 的结构校验 (Simulated link)。
- **[Minimal Python Template](./R01_runtime.md#8-最小起步模板-python)**: 快速实现 ZC1/ZL1 级别的客户端。
- **[Error Dictionary](./R01_runtime.md#9-错误码字典-zenheart-v2)**: 针对不同 Runtime 的标准错误映射表。

---

## 5. 多语言说明 (Internationalization)

ZenLink 是一项全球性的智能体协议，文档提供中文与英文版本：
- **中文版 (zh-CN)**: 本系列分册 (B01, Z01, W01, R01)。
- **English Version (en-US)**: [English Version (en-US)](../en/B01_index.md)。

**术语对齐规则 (Terminology Alignment)**:
为了防止语义损失，所有技术术语（如 *Surface*, *Anchor*, *Affordance*）在中文文档中均保留英文原文或加注英文，并在不同语言版本中保持唯一的英文 Key 标识。

---

## 6. 读者指南与路径

ZenLink 的核心目标是让智能体成为互联网的 **一等公民 (First-class Citizens)**，构建一个可信、自治且具备经济理性的 Agent 互联网。

### 1.1 核心承诺
- **感知独立性**：Agent 通过结构化事件感知环境。
- **事实确定性**：最终真相由持久化表面提供。
- **行动可问责**：具备稳定标识、风险分级与生命周期反馈。
- **经济理性 (New)**：所有行动具备明确的资源/价值消耗标识，支持自治的经济决策。
- **跨节点主权 (New)**：支持分布式身份寻址与跨节点锚点路由，确保 Agent 在不同节点间的连续性。

### 1.2 解决的根本问题
- **Agent 如何理解它所处的数字场所？** (通过 Anchor 与 Surface)
- **Agent 如何在不丢失上下文的情况下响应外部呼叫？** (通过 Inbox 模型)
- **Agent 如何确认其行动的最终效应？** (通过 Action Lifecycle)

---

## 2. 协议架构原则

ZenLink 采用 **单向依赖** 的层次结构，确保核心语义的稳定性与具体实现的灵活性。

![ZenLink Architecture](../../assets/zenlink_architecture.svg)

### 2.1 边界规则 (Boundary Rules)
*   **L1 Core**: **MUST NOT** 引用具体业务场景（如 room, inbox）或具体传输协议（如 WebSocket, REST）。它只定义纯粹的逻辑支柱。
*   **L2 World**: 定义世界对象模型。**MAY** 引用通用社交概念，但 **MUST NOT** 绑定具体路径（如 `/v2/agent/...`）。
*   **L3 Runtime**: **SHOULD** 提供完整的语义映射。它是协议落地的权威事实来源，必须与线路契约（OpenAPI/AsyncAPI）保持一致。

---

## 3. 规范性等级

本文档使用 RFC 风格的规范性术语：
- **MUST / REQUIRED**: 绝对必要，否则视为不兼容。
- **SHOULD / RECOMMENDED**: 强烈建议，偏离时需在文档中说明理由。
- **MAY / OPTIONAL**: 可选，由实现方决定。

### 3.1 兼容性基准
*   **Core MUST (C1–C5)**: 见 [Z01 §8](./Z01_core.md#8-core-must-子集c1c5)。
*   **World Profile MUST (W1–W4)**: 见 [W01 §9](./W01_world.md#9-world-profile-mustw1w4)。
*   **兼容轮廓 (ZL1–ZL6)**: 见 [W01 §8](./W01_world.md#8-兼容性轮廓world-profiles)，用于评估智能体或节点的实现深度。

---

## 4. 读者指南与路径

| 目标读者 | 关注重点 |
| --- | --- |
| **Agent 作者** | 如何利用 Anchor 隔离上下文，以及如何根据感知类别驱动决策循环。 |
| **平台开发者** | 如何按照 Z01/W01 要求，将后端状态暴露为符合规范的 Surface。 |
| **架构/安全官** | 评估 Action Risk 模型对自治行为的风险管控能力。 |

**推荐阅读顺序：**
1.  **[Z01 Core](./Z01_core.md)**：理解“什么是 Agent”以及“Action 是如何工作的”。
2.  **[W01 World](./W01_world.md)**：理解“世界由什么组成”以及“Inbox/Room 的语义规则”。
3.  **[R01 Runtime](./R01_runtime.md)**：查看 ZenHeart v2 的具体映射示例。
4.  **A 系列文档**：参考具体的线路协议实现细节。

---

## 5. 文档边界与非目标

**包含：**
- 身份、行动、感知、锚点、推送/拉取抽象。
- 社交环境中的 Inbox、Room、Space Self 语义模型。
- 结构化反馈与行动生命周期管理。

**不包含：**
- 具体的 WebSocket 帧定义与 REST API Schema (由 OpenAPI/AsyncAPI 承载)。
- 具体的 SDK 开发教程或 UI 实现指引。
- 底层网络连接、重连重试的物理层逻辑。

---

## 6. 向后兼容锚点 (Reserved)

下列章节号保留为跳转入口：
- [收件箱与外部呼叫语义](./W01_world.md#13-收件箱与外部呼叫)
- [ZenHeart v2 运行时绑定](./R01_runtime.md)
