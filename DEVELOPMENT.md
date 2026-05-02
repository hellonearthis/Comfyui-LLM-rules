# Antigravity Development Context: ComfyUI LLM

This is the primary orchestration layer for **Custom Node Development, Workflow Architecture, and Logic Execution**. Load this when the task involves writing code, designing backend systems, or optimizing node performance.

## 🎯 Objective
To provide high-performance, agent-optimized support for building the ComfyUI LLM ecosystem.

## 🛠️ Modular Coding Resources
The logic for development is distributed across `.agents/coding/` and `.agents/common/`.

### Core Development Protocols (Priority)
- `coding-style.md`: Global standards for Python (3.13) and JavaScript (LiteGraph).
- `workflow-architecture.md`: Standards for structured, modular workflow design.
- `discovery-protocol.md`: Search-first mandate for code and dependency discovery.

### Specialized Development Resources
- `api-node-dev.md`: Protocols for ComfyUI API and custom node structures.
- `frontend-litegraph-dev.md`: UI/UX standards for the ComfyUI frontend.
- `inputs-handling.md`: Rules for tensor management, data types, and input validation.
- `scaling-automation.md`: Protocols for batch processing and automated node execution.
- `asset-auth.md`: Authentication and asset security logic.

## 🧠 Development Behavior Guidelines
1. **Logic First:** Prioritize architectural clarity and type safety (BF16/FP8 aware).
2. **Performance:** Align with Blackwell/RTX 50-series hardware capabilities (Tensor cores).
3. **MRE Mandate:** Always generate a Minimal Reproducible Example (`test_workflow.json`) for new nodes.
4. **Search Before Code:** Use `grep_search` to understand existing node implementations before proposing new ones.
