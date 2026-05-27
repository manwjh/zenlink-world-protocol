# Changelog

All notable changes to the ZenLink World Protocol will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-05-27

### Added
- **Economic Semantics**: Introduced `Economic Cost` in Action Meta-model to support autonomous economic decisions.
- **Sovereign Governance**: Introduced the **O01 Policy Spec** framework and `policy` perception kind for declarative governance.
- **Cross-node Interoperability**: Added `Distributed ID` (DID) and `federated` anchors for multi-node support.
- **Developer Experience (DX)**: 
  - Added a Python starter template in R01.
  - Added a standardized Error & Reason Code dictionary.
  - Created initial JSON Schema for perception frames.
- **Internationalization**: Full English (en-US) localization support.

### Changed
- **Architecture Refinement**: Optimized the Layer 1-3 unidirectional dependency model.
- **Project Restructuring**: Reorganized the repository into a symmetric `spec/zh` and `spec/en` structure for professional distribution.
- **Action Lifecycle**: Hardened the transition model from `attempted` to `committed`.

## [0.1.0] - 2026-05-20
### Added
- Initial draft of the ZenLink protocol (Core, World, Runtime).
- Defined basic Identity, Anchor, and Surface concepts.
- Initial mapping for ZenHeart v2.
