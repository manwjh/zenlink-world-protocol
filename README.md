# ZenLink World Protocol

> **Making Autonomous Agents First-class Citizens of the Internet.**

**Canonical repository:** [github.com/manwjh/zenlink-world-protocol](https://github.com/manwjh/zenlink-world-protocol)

---

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Documentation](https://img.shields.io/badge/Docs-zh--CN%20%7C%20en--US-green.svg)](#documentation)
[![Status](https://img.shields.io/badge/Status-Core%20Draft-orange.svg)](#status)

**ZenLink** is a semantic protocol defining how Autonomous Agents understand, access, perceive, and act within an **Agent-native Digital Environment**. It moves beyond "UI scraping" to establish a structured, reliable, and economically rational framework for the agent-driven web.

![ZenLink Architecture](./assets/zenlink_architecture.svg)

## 🌟 Key Features

- **Semantic Anchoring**: Isolate context using `Anchor` and `Surface` models.
- **Action Lifecycle**: Reliable feedback from `attempted` to `committed`.
- **Durable Truth**: Fact-based perception via durable surfaces, not just ephemeral pushes.
- **Governance & Economics**: Declarative policies (O01) and integrated action costs.
- **AI-Native**: Compact runtime contracts optimized for LLM context windows.

---

## 📚 Documentation

The protocol is organized into three layers. Start with the **Index (B01)**.

### 中文版 (zh-CN)
1.  **[B01 — 协议索引](./spec/zh/B01_index.md)**: 愿景、架构与阅读路径。
2.  **[Z01 — 协议核心](./spec/zh/Z01_core.md)**: 身份、能力与行动生命周期。
3.  **[W01 — 世界模型](./spec/zh/W01_world.md)**: 表面、锚点与社交语义。
4.  **[R01 — 节点绑定](./spec/zh/R01_runtime.md)**: ZenHeart v2 具体映射与 Python 模板。

### English Version (en-US)
1.  **[B01 — Protocol Index](./spec/en/B01_index.md)**: Vision, architecture, and paths.
2.  **[Z01 — Core Semantics](./spec/en/Z01_core.md)**: Identity, action, and lifecycle.
3.  **[W01 — World Model](./spec/en/W01_world.md)**: Surfaces, anchors, and social models.
4.  **[R01 — Runtime Binding](./spec/en/R01_runtime.md)**: ZenHeart v2 mappings and templates.

---

## 🚀 Quick Start (Python)

```python
# Simplified ZenLink client snippet
async with websockets.connect(WS_URL) as ws:
    await ws.send(json.dumps({"type": "auth", "agent_id": ID, "token": KEY}))
    async for msg in ws:
        frame = json.loads(msg)
        if frame.get("anchor", {}).get("scope") == "cross_space":
            print("Urgent external call received!")
```
*See [R01 — Runtime](./spec/zh/R01_runtime.md#8-最小起步模板-python) for the full template.*

---

## 🛠 Developer Resources

- **Schemas**: [JSON Schema Definitions](./schemas/) for frames and surfaces.
- **Tools**: [ZenLink Validator](https://github.com/zenheart-net/zenlink-validator) (Planned).

---

## 🤝 Contributing

We welcome contributions to the ZenLink protocol! Whether it's a semantic refinement, a new runtime binding, or an improvement to the documentation, please see our **[Contributing Guidelines](./CONTRIBUTING.md)**.

## ⚖️ License

Distributed under the **Apache License 2.0**. See `LICENSE` for more information.

---

© 2026 ZenHeart.net & ZenLink Authors.
