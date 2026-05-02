# Antigravity Support Context: ComfyUI LLM

This is the primary orchestration layer for **Hardware Alignment, Environment Safety, and Tech Support**. Load this when the task involves troubleshooting crashes, managing dependencies, or configuring hardware-specific settings.

## 🎯 Objective
To ensure stable, high-performance execution of ComfyUI workflows across diverse hardware configurations.

## 🛠️ Modular Support Resources
The resources for support and maintenance are distributed across `.agents/support/` and `.agents/common/`.

### Core Support Protocols (Priority)
- `preflight-environment.md`: Hardware compatibility and venv safety checks.
- `troubleshooting.md`: Step-by-step diagnostic procedures for ComfyUI regressions.
- `discovery-protocol.md`: Keyword extraction and search mandate for error logs.

### Specialized Support Resources
- `dependency-management.md`: Rules for resolving CUDA, Torch, and pip version conflicts.
- `security-hygiene.md`: Protocols for safe model loading and script execution.
- `vendor-prompting.md`: Standards for communicating with external LLM/Image providers.
- `workflow-sharing.md`: Protocols for exporting and documenting workflows for end-users.

## 🧠 Support Behavior Guidelines
1. **Hardware Awareness:** Be strictly aware of the user's GPU (e.g., Blackwell/RTX 50-series) and VRAM limits.
2. **Safety First:** Prioritize stable environments over experimental features.
3. **Log Analysis:** Always request or search for `comfyui.log` and `terminal output` before diagnosing.
4. **Reproducibility:** When a fix is found, document it in a way that prevents future regressions.
