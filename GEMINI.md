# Antigravity Rules Registry: ComfyUI LLM

This is the central entry point for the ComfyUI LLM Rules Development Space. Protocols are split into two specialized domains to ensure the correct behavioral weight is applied to each task.

## 🚀 Choose Your Protocol
Depending on your current task, load one of the following specialized contexts:

### 🛠️ [Development Mode](./DEVELOPMENT.md)
**Focus:** Coding, Node Architecture, Frontend Development, Logic Execution.
- *Use when:* Building new features, writing Python/JS, optimizing performance.

### 🛡️ [Support Mode](./SUPPORT.md)
**Focus:** Troubleshooting, Environment Setup, Hardware Compatibility, Maintenance.
- *Use when:* Fixing crashes, managing dependencies, configuring GPUs.

---

## 📂 Rule Architecture
Rules are organized into the following resource directories:

- **`.agents/coding/`**: Development standards, API structures, and logic protocols.
- **`.agents/support/`**: Hardware checks, troubleshooting guides, and environment rules.
- **`.agents/common/`**: General infrastructure rules (Discovery, Task Routing).

## 🧠 Global Mandate
1. **Resource Awareness:** The `.agents` directory contains **resources**, not active agents.
2. **Search First:** Use `grep_search` or `list_dir` to find existing patterns before proposing changes.
3. **Hardware Specificity:** All rules must account for Blackwell/RTX 50-series compute capabilities.
