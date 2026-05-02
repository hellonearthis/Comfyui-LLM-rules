# ComfyUI LLM Development Guide

Welcome to the ComfyUI LLM Guide repository. This workspace contains a strict, token-dense set of protocols designed specifically for AI Agents to follow when assisting with ComfyUI workflow execution, custom node development, and backend architecture.

## 🚀 Antigravity Tuning & System Architecture

This workspace has been explicitly tuned for **Agentic RAG** and the Antigravity router.

- **YAML Frontmatter:** Every module in the `.agents/rules/` directory is equipped with a strict `name:` and `description:` YAML block at the top.
- **Automatic Indexing:** The router parses these `description:` blocks to understand precisely _when_ to load a specific rule.
- **Context Efficiency:** This architecture prevents the agent from dumping 12,000 words of documentation into its context window, allowing it to pull only the specific 500-1000 tokens required for the immediate task.

## 🧠 Agent Routing Instructions

**To AI Agents reading this:** The Antigravity system may auto-load rules based on their YAML frontmatter. However, if you are exploring the repository manually, DO NOT load all files in the `.agents/rules/` directory at once. Use the table of contents below to determine exactly which protocol is relevant to the user's current request, and `view_file` on that specific module.

### Directory: `/.agents/rules`

#### Foundational Execution & Routing

- `preflight-environment.md` — Hardware alignment, VRAM safeguards, and venv setup.
- `discovery-protocol.md` — The search-first mandate and trigger word extraction.
- `task-routing.md` — The routing table and exact CLI syntax for T2I/I2I/Video.

#### Assets, Inputs, & Sharing

- `asset-auth.md` — URI priorities, Civitai/HF authentication, and Format Translation.
- `inputs-handling.md` — Handling image URLs, PNG embedded workflows, and WebFetch scraping.
- `workflow-sharing.md` — Converting UI workflows to API JSON and sharing via `uvx`.

#### Automation & Scaling

- `scaling-automation.md` — Daemon processing and Python embedded client logic (CSV loops).

#### Troubleshooting & Vendor Specs

- `troubleshooting.md` — OOM escalation paths, reading logs, and the Developer Escape hatch.
- `vendor-prompting.md` — The authoritative index of official vendor prompting URLs (Flux, Wan, LTX, etc.).

#### Pro-Level Development & Architecture

- `coding-style.md` — Global coding style, variable naming, linting mandates, and MRE creation.
- `workflow-architecture.md` — Graph primitive decoupling, logic grouping, and modular loaders.
- `api-node-dev.md` — Headless websocket integration, interrupt strategies, and backend custom node class rules.
- `frontend-litegraph-dev.md` — Frontend node development, LiteGraph widget handling, and Vue integration.

## 🛠️ Installation & Setup (Antigravity)

To integrate these rules into your Antigravity environment:

1. **Workspace Registration:** Open this folder (`Comfyui LLM`) in your local IDE where the Antigravity extension is active.
2. **Indexing:** Antigravity will automatically index the `.agents/rules/` directory based on the YAML frontmatter in each file.
3. **Settings:**
   - **Context Level:** Ensure "Agentic RAG" or "Rule Indexing" is enabled in your Antigravity settings.
   - **Triggering:** The agent will selectively load rules based on your request. You can also explicitly invoke a rule by mentioning its name (e.g., "Follow the preflight environment protocol").
   - **VRAM Safeguards:** The `preflight-environment.md` rule is critical for Blackwell (RTX 50-series) hardware; ensure your hardware profile in Antigravity matches your actual specs.

## 🤖 Compatibility with Other AI Tools

While this repository is optimized for Antigravity via `GEMINI.md`, the modular rules in `.agents/rules/` are compatible with several other AI coding assistants.

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
