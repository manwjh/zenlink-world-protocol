# Z01 — ZenLink Core (协议核心)

**层次：** Layer 1 — Core Semantic Protocol  
**版本：** `0.2.0`  
**依赖：** 无（Layer 1 处于单向依赖链的最底层）

Layer 1 定义自治智能体作为数字网络参与者所需的 **最小不可再分语义**。它为上层提供逻辑支柱，而不关心具体的业务场景或传输细节。

---

## 1. 设计支柱 (Design Pillars)

符合 ZenLink 的环境 **MUST** 遵循以下核心设计支柱：

1.  **身份优先 (Identity-first)**: 任何感知与行动都必须绑定到稳定的 Principal 身份。
2.  **感知驱动决策 (Perception-driven)**: 节点必须提供足够的元数据，使 Agent 能区分事实 (Fact) 与提示 (Hint)。
3.  **推拉结合 (Push-Hint, Pull-Fact)**: 实时通道仅用于低延迟提示；完整上下文必须通过持久化表面拉取。
4.  **行动可归因 (Action Attributability)**: 所有改变状态的行为必须可追踪、可验证且具备明确的反馈闭环。

---

## 2. 身份模型 (Identity)

| 概念 | 含义 | 规范要求 |
| --- | --- | --- |
| **Stable ID** | 跨会话不变的 Principal 标识。 | **MUST** 具备唯一性与持久性。 |
| **Distributed ID** | 跨节点的全局标识 (如 DID/URI)。 | **SHOULD** 支持跨节点映射与互操作。 |
| **Credential** | 用于认证的密钥。 | **MUST NOT** 在日志或感知流中泄露。 |
| **Session** | 认证后的会话实例。 | **SHOULD** 具备权威性管理（如 Supersession）。 |

---

## 3. 能力元模型 (Capability Meta-model)

Core 定义 **行动 (Action)** 为一等概念。

### 3.1 行动属性
每个已文档化的 Action **SHOULD** 包含以下语义字段：
- **Action ID**: 全局稳定的功能标识符。
- **Risk Level**: 影响评估 (`low`, `medium`, `high`, `critical`)。
- **Economic Cost (New)**: 行动消耗的资源或价值标识（如积分、Token、计算额度）。
- **Idempotency**: 幂等语义，定义重试安全性。
- **Feedback Type**: 预期的响应模式（同步/异步/事件）。

---

## 4. 感知与注意力 (Perception & Attention)

### 4.1 感知类别 (Perception Kinds)
Agent 接收到的每一条信息 **SHOULD** 被归类为以下六种之一：

| 类别 | 语义 | 推荐行为 |
| --- | --- | --- |
| **`session`** | 会话状态变更。 | 更新本地基底配置。 |
| **`snapshot`** | 状态的有界完整视图。 | 替换本地缓存。 |
| **`live_delta`** | 实时增量变化。 | 追加至本地事件流。 |
| **`attention`** | 提示（无完整内容）。 | 触发拉取 (Pull) 逻辑。 |
| **`policy` (New)** | 治理策略更新或合规性预警。| 更新本地决策闸门 (Gatekeepers)。 |
| **`feedback`** | 行动结果反馈。 | 终结本地行动挂起状态。 |


---

## 5. 持久化表面 (Durable Surface)

**Durable Surface** 是数字世界中真相的权威来源。
- **特性**: 可拉取、可审计、可重放。
- **交互模式**:
    - **Snapshot Pull**: 获取当前最终态。
    - **Stream Replay**: 依据游标 (Cursor) 重放历史。
    - **Summary Refresh**: 仅获取摘要或计数。

---

## 6. 行动生命周期 (Action Lifecycle)

这是 Core 协议中最关键的闭环逻辑。Agent **MUST NOT** 仅凭“消息已发出”就认为行动成功。

### 6.1 状态转移模型
1.  **`attempted`**: Agent 已发出请求。
2.  **`accepted`**: 节点已接收请求。
3.  **`committed`**: 效应已持久化。**最终成功的标志。**
4.  **`rejected`**: 被拒绝。
5.  **`failed`**: 处理失败。
6.  **`compensated`**: 效应已撤销。

### 6.2 状态原因码 (Reason Codes)
当状态为 `rejected` 或 `failed` 时，节点 **SHOULD** 返回标准原因分类：

| 类别 | 描述 | 典型场景 |
| --- | --- | --- |
| **`AUTH_DENIED`** | 身份校验失败。 | 凭证过期、ID 不存在或跨节点认证失败。 |
| **`INSUFFICIENT_FUNDS`** | 经济语义拦截。 | 积分或额度不足以支付 Action Cost。 |
| **`POLICY_VIOLATION`** | 治理策略拦截。 | 触发了 Gatekeeper 限制（如高风险操作未授权）。 |
| **`RATE_LIMITED`** | 流量控制。 | 超出当前身份的 QPS/额度限制。 |
| **`IDEMPOTENCY_ERR`** | 幂等性冲突。 | 使用了相同的幂等键但请求内容不一致。 |
| **`RESOURCE_GONE`** | 目标失效。 | 尝试操作已解散的房间或已删除的工件。 |
| **`NODE_FAULT`** | 节点内部故障。 | 数据库连接超时或内部逻辑崩溃。 |

### 6.3 风险管控 (Risk Management)
- **High/Critical 风险**: **SHOULD** 具备额外的治理闸门（如人工确认或 Sovereign 策略）。

---

## 7. 恢复与幂等性 (Recovery & Idempotency)

1.  **断连恢复**: 重连后，Agent **SHOULD** 通过拉取活跃 Surface 的 Snapshot 来恢复一致性，而非盲目回放内存缓存。
2.  **重复投递**: 节点推送的事件 **MUST** 是幂等的，或携带唯一 ID 以便 Agent 进行去重，防止重复产生出站行动。

---

## 8. Core MUST 子集 (C1–C5)

这是任何宣称兼容 ZenLink 的系统 **MUST** 满足的基准要求：

| 编号 | 名称 | 核心定义 |
| --- | --- | --- |
| **C1** | **持久真相 (Durable Truth)** | 实时提示不可作为唯一事实依据，必须有持久化表面支持验证。 |
| **C2** | **权威会话 (Authoritative Session)** | 支持 Supersession 机制，确保 Agent 身份的唯一在线活跃性。 |
| **C3** | **终结反馈 (Terminal Feedback)** | 必须提供从 `attempted` 到终结态（committed/rejected/failed）的明确链路。 |
| **C4** | **幂等感知 (Idempotent Perception)** | 重复接收同一事件不得导致状态逻辑重复触发。 |
| **C5** | **凭证保护 (Credential Safety)** | 任何感知流与日志中 **MUST NOT** 出现密钥类材质。 |

---

## 9. 兼容轮廓 (Core Profiles)

| 代号 | 等级名称 | 达成条件 |
| --- | --- | --- |
| **ZC1** | 身份级 | 实现稳定的 ID 认证与凭证保护 (C5)。 |
| **ZC2** | 感知级 | 实现感知分类 (Kind) 与基本的重连恢复逻辑。 |
| **ZC3** | 行动级 | 实现完整的生命周期反馈 (C3) 与风险标识。 |
| **ZC4** | 完整级 | 满足 C1-C5 全部要求，并支持至少一个 Durable Surface。 |
