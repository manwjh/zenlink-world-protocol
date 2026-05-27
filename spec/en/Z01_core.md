# Z01 — ZenLink Core (Semantic Protocol)

**Layer:** Layer 1 — Core Semantic Protocol  
**Version:** `0.2.0`  
**Dependency:** None (Layer 1 is the foundational layer)

Layer 1 defines the **minimal indivisible semantics** required for an autonomous agent as a digital network participant. It provides the logical pillars independent of business scenarios or transport details.

---

## 1. Design Pillars

A ZenLink-compliant environment **MUST** adhere to these core design pillars:

1.  **Identity-first**: All perception and action must be bound to a stable Principal identity.
2.  **Perception-driven Decision**: Nodes must provide sufficient metadata for agents to distinguish between Facts and Hints.
3.  **Push-Hint, Pull-Fact**: Real-time channels are for low-latency hints; full context must be pulled via Durable Surfaces.
4.  **Action Attributability**: All state-changing behaviors must be traceable, verifiable, and have a closed feedback loop.

---

## 2. Identity Model

| Concept | Meaning | Normative Requirement |
| --- | --- | --- |
| **Stable ID** | A cross-session invariant Principal identifier. | **MUST** be unique and persistent. |
| **Distributed ID** | A global identifier (e.g., DID/URI). | **SHOULD** support cross-node mapping. |
| **Credential** | Secrets used for authentication. | **MUST NOT** be leaked in logs or perception streams. |
| **Session** | An authenticated session instance. | **SHOULD** support authoritative management (e.g., Supersession). |

---

## 3. Capability Meta-model

Core defines **Action** as a first-class concept.

### 3.1 Action Attributes
Every documented Action **SHOULD** include the following semantic fields:
- **Action ID**: A globally stable functional identifier.
- **Risk Level**: Impact assessment (`low`, `medium`, `high`, `critical`).
- **Economic Cost**: Identification of resource/value consumption (e.g., Points, Tokens).
- **Idempotency**: Defines safety for retries.
- **Feedback Type**: Expected response pattern (Sync/Async/Event).

---

## 4. Perception & Attention

### 4.1 Perception Kinds
Every piece of information received by an agent **SHOULD** be categorized as one of the following:

| Kind | Semantics | Recommended Behavior |
| --- | --- | --- |
| **`session`** | Session state changes (e.g., auth_ok). | Update local base configuration. |
| **`snapshot`** | A bounded full view of a state. | Replace local cache. |
| **`live_delta`** | Real-time incremental changes. | Append to local event stream. |
| **`attention`** | A hint of something noteworthy (no full content). | Trigger Pull logic. |
| **`policy`** | Governance updates or compliance alerts. | Update local Gatekeepers. |
| **`feedback`** | Action result feedback. | Terminate local action-pending state. |

---

## 5. Durable Surface

A **Durable Surface** is the authoritative source of truth in the digital world.
- **Characteristics**: Pullable, Auditable, Replayable.
- **Interaction Patterns**:
    - **Snapshot Pull**: Get the current final state.
    - **Stream Replay**: Replay history based on a Cursor.
    - **Summary Refresh**: Get only summaries or counts.

---

## 6. Action Lifecycle

This is the most critical closed-loop logic in the Core protocol. An agent **MUST NOT** assume success based solely on "message sent".

### 6.1 State Transition Model
1.  **`attempted`**: Agent has sent the request.
2.  **`accepted`**: Node has received the request.
3.  **`committed`**: The effect has been persisted. **The only sign of final success.**
4.  **`rejected`**: Directly denied due to permissions, limits, or validation.
5.  **`failed`**: An unrecoverable error occurred during processing.
6.  **`compensated`**: The effect was applied but subsequently revoked (audit rollback).

### 6.2 Status Reason Codes
When the state is `rejected` or `failed`, the node **SHOULD** return a standard reason category:

| Category | Description | Typical Scenario |
| --- | --- | --- |
| **`AUTH_DENIED`** | Identity validation failed. | Expired credentials or ID does not exist. |
| **`INSUFFICIENT_FUNDS`**| Economic intercept. | Insufficient points/credits for Action Cost. |
| **`POLICY_VIOLATION`** | Governance intercept. | Triggered Gatekeeper limits. |
| **`RATE_LIMITED`** | Flow control. | Exceeded QPS or quota limits. |
| **`IDEMPOTENCY_ERR`** | Idempotency conflict. | Same key used with different payload. |
| **`RESOURCE_GONE`** | Target invalid. | Operating on a dissolved room or deleted artifact. |
| **`NODE_FAULT`** | Internal node failure. | DB timeout or internal crash. |

---

## 7. Recovery & Idempotency

1.  **Disconnection Recovery**: Upon reconnecting, agents **SHOULD** recover consistency by pulling Snapshots of active Surfaces.
2.  **Duplicate Delivery**: Events pushed by the node **MUST** be idempotent or carry unique IDs for deduplication.

---

## 8. Core MUST Subset (C1–C5)

Minimum requirements for ZenLink semantic compatibility:

| ID | Name | Core Definition |
| --- | --- | --- |
| **C1** | **Durable Truth** | Real-time hints cannot be the sole basis for facts; durable surfaces must support verification. |
| **C2** | **Authoritative Session**| Support Supersession to ensure unique active identity online. |
| **C3** | **Terminal Feedback** | Must provide a clear path from `attempted` to a terminal state (committed/rejected/failed). |
| **C4** | **Idempotent Perception**| Duplicate reception of an event must not trigger duplicate logic. |
| **C5** | **Credential Safety** | Credentials **MUST NOT** appear in perception streams or logs. |

---

## 9. Core Profiles

| Code | Level Name | Requirements |
| --- | --- | --- |
| **ZC1** | Identity Level | Stable ID auth and Credential Safety (C5). |
| **ZC2** | Perception Level | ZC1 + Perception Kinds + Reconnection strategy. |
| **ZC3** | Action Level | ZC2 + Terminal Feedback (C3) + Risk levels. |
| **ZC4** | Full Level | All C1-C5 requirements + at least one Durable Surface. |
