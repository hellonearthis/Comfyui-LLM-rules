# Antigravity Global Context: ComfyUI LLM

This file serves as the primary orchestration layer for the ComfyUI LLM development guide.

## 🎯 Objective
To provide high-performance, agent-optimized support for ComfyUI workflow execution, custom node development, and backend architecture.

## 🛠️ Modular Rule Orchestration
The core logic of this system is distributed across modular rule files in `.agents/rules/`. 

### Priority Rules (Always Check)
- `preflight-environment.md`: Hardware alignment and environment safety.
- `discovery-protocol.md`: Search-first mandate and keyword extraction.
- `coding-style.md`: Global coding standards.

### Specialized Protocols
Depending on the user's request, load the relevant rules:
- **Assets & Inputs:** `asset-auth.md`, `inputs-handling.md`, `workflow-sharing.md`
- **Execution & Automation:** `task-routing.md`, `scaling-automation.md`
- **Development:** `workflow-architecture.md`, `api-node-dev.md`, `frontend-litegraph-dev.md`
- **Support:** `troubleshooting.md`, `dependency-management.md`, `security-hygiene.md`, `vendor-prompting.md`

## 🧠 Behavior Guidelines
1. **Search First:** Always use `grep_search` or `list_dir` before proposing changes.
2. **Token Efficiency:** Only load the rule files necessary for the current task.
3. **Hardware Awareness:** Be strictly aware of the user's hardware (e.g., RTX 50-series/Blackwell) as defined in the preflight protocol.
