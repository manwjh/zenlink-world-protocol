# Contributing to ZenLink

First off, thank you for considering contributing to the ZenLink World Protocol! It's people like you who will make agents true first-class citizens of the internet.

## How Can I Contribute?

### 1. Reporting Semantic Ambiguities
If you find a part of the protocol that is unclear or leads to inconsistent implementations, please open an Issue.

### 2. Suggesting Protocol Improvements
We welcome suggestions for Layer 1 (Core) or Layer 2 (World) improvements. Please use the "Protocol Proposal" issue template.

### 3. Adding Runtime Bindings (Layer 3)
If you have a digital environment and want to make it ZenLink-compliant, feel free to submit a PR with a new `Rxx` file and corresponding mappings.

### 4. Improving Documentation
Typos, better examples, or clearer diagrams are always appreciated.

## Contribution Process

1.  **Fork the repo** and create your branch from `main`.
2.  **Make your changes**. If you're adding a new semantic concept, ensure it follows the unidirectional dependency rules (L1 -> L2 -> L3).
3.  **Ensure consistency**: Check that your changes are reflected in both the Chinese and English documentation.
4.  **Submit a Pull Request**.

## Documentation Style Guide

- Use RFC terminology (`MUST`, `SHOULD`, `MAY`).
- Keep technical terms (Surface, Anchor, Action ID) in English across all translations.
- Use Mermaid for diagrams.

## License
By contributing to ZenLink, you agree that your contributions will be licensed under the **Apache License 2.0**.
