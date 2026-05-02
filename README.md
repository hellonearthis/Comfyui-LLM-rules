# ComfyUI LLM Development Guide

---

## ⚡ Quick Start: Use this with your AI Assistant
To get the best results, tell your AI agent which mode you need by copying one of these commands:

**For Development (Coding, Nodes, UI):**
> "Reference `DEVELOPMENT.md` and follow the coding protocols for this task."

**For Support (Troubleshooting, Hardware, Environment):**
> "Reference `SUPPORT.md` and perform a pre-flight hardware check."

---

Welcome to the ComfyUI LLM Guide repository. This workspace contains a strict, token-dense set of protocols designed specifically for AI Agents to follow when assisting with ComfyUI workflow execution, custom node development, and backend architecture.

## 🚀 Antigravity Tuning & System Architecture

This workspace has been explicitly tuned for **Agentic RAG** and the Antigravity router.

- **Dual-Mode Orchestration:** Choose between **Development** and **Support** modes to align the AI's behavior with your current task.
- **Modular Directory Structure:** Rules are organized into `.agents/coding/`, `.agents/support/`, and `.agents/common/` to ensure high-precision context loading.
- **Context Efficiency:** This architecture prevents the agent from dumping excessive documentation into its context window, pulling only the specific tokens required.

## 🧠 Mode Selection (How to Choose)

Before starting a task, you should tell the AI which mode to operate in by referencing the corresponding orchestration file:

### 🛠️ Development Mode
**Target:** Coding, Node Architecture, Frontend Development, Logic Execution.
- **How to activate:** Say "Load Development Mode" or "Reference DEVELOPMENT.md".
- **Focus:** Building new features, writing Python/JS, optimizing performance.

### 🛡️ Support Mode
**Target:** Troubleshooting, Environment Setup, Hardware Compatibility, Maintenance.
- **How to activate:** Say "Load Support Mode" or "Reference SUPPORT.md".
- **Focus:** Fixing crashes, managing dependencies, configuring GPUs (RTX 50-series).

---

## 📂 Rule Architecture

### Directory: `/.agents/coding`
Rules for building and architecting ComfyUI nodes and logic.
- `api-node-dev.md`, `coding-style.md`, `frontend-litegraph-dev.md`, `inputs-handling.md`, `workflow-architecture.md`, `scaling-automation.md`, `asset-auth.md`.

### Directory: `/.agents/support`
Rules for environment safety, hardware alignment, and troubleshooting.
- `preflight-environment.md`, `troubleshooting.md`, `dependency-management.md`, `security-hygiene.md`, `vendor-prompting.md`, `workflow-sharing.md`.

### Directory: `/.agents/common`
Shared infrastructure and discovery protocols.
- `discovery-protocol.md`, `task-routing.md`.

## 🛠️ Installation & Setup (Antigravity)

To integrate these rules into your Antigravity environment:

1. **Workspace Registration:** Open this folder (`Comfyui LLM`) in your local IDE where the Antigravity extension is active.
2. **Indexing:** Antigravity will automatically index the `.agents/` directory.
3. **Settings:**
   - **Context Level:** Ensure "Agentic RAG" or "Rule Indexing" is enabled in your Antigravity settings.
   - **Triggering:** The agent will selectively load rules based on your request. You can also explicitly invoke a rule by mentioning its name (e.g., "Follow the preflight environment protocol").
   - **VRAM Safeguards:** The `preflight-environment.md` rule is critical for Blackwell (RTX 50-series) hardware; ensure your hardware profile in Antigravity matches your actual specs.

## 🤖 Compatibility with Other AI Tools

While this repository is optimized for Antigravity via `GEMINI.md`, the modular rules in `.agents/` are compatible with several other AI coding assistants.

### Supported Tool Mappings
If you use multiple AI tools, you can point them to these rules by creating or symlinking the following files at the root:

| Tool | Rule File | Notes |
| :--- | :--- | :--- |
| **Antigravity** | `GEMINI.md` | Highest priority; orchestration layer. |
| **Claude Code** | `CLAUDE.md` | Can be symlinked to `GEMINI.md`. |
| **Cursor** | `.cursorrules` | Use this for project-wide Cursor rules. |
| **Cross-Tool** | `AGENTS.md` | Shared rules across all "agentic" tools. |

### Quick Setup for Multi-Tool Support
To use these rules with both Antigravity and Claude Code simultaneously, you can run:
```powershell
# PowerShell (Windows)
New-Item -ItemType SymbolLink -Path "CLAUDE.md" -Target "GEMINI.md"
```

## 🙏 Acknowledgments
- Special thanks to **doctorpangloss** from the ComfyUI Discord channel for technical insights and foundational knowledge.
- Built upon and inspired by the [llms.txt protocol](https://github.com/hiddenswitch/pip-and-uv-installable-ComfyUI/blob/master/llms.txt) by Hiddenswitch.
