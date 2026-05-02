# ComfyUI LLM Development Guide

Welcome to the ComfyUI LLM Guide repository. This workspace contains a strict, token-dense set of protocols designed specifically for AI Agents to follow when assisting with ComfyUI workflow execution, custom node development, and backend architecture.

## 🚀 Antigravity Tuning & System Architecture

This workspace has been explicitly tuned for **Agentic RAG** and the Antigravity router.

- **YAML Frontmatter:** Every module in the `rules/` directory is equipped with a strict `name:` and `description:` YAML block at the top.
- **Automatic Indexing:** The router parses these `description:` blocks to understand precisely _when_ to load a specific rule.
- **Context Efficiency:** This architecture prevents the agent from dumping 12,000 words of documentation into its context window, allowing it to pull only the specific 500-1000 tokens required for the immediate task.

## 🧠 Agent Routing Instructions

**To AI Agents reading this:** The Antigravity system may auto-load rules based on their YAML frontmatter. However, if you are exploring the repository manually, DO NOT load all files in the `rules/` directory at once. Use the table of contents below to determine exactly which protocol is relevant to the user's current request, and `view_file` on that specific module.

### Directory: `/rules`

#### Foundational Execution & Routing

- `01_preflight_environment.md` — Hardware alignment, VRAM safeguards, and venv setup.
- `02_discovery_protocol.md` — The search-first mandate and trigger word extraction.
- `03_task_routing_examples.md` — The routing table and exact CLI syntax for T2I/I2I/Video.

#### Assets, Inputs, & Sharing

- `04_asset_auth_logic.md` — URI priorities, Civitai/HF authentication, and Format Translation.
- `05_inputs_handling.md` — Handling image URLs, PNG embedded workflows, and WebFetch scraping.
- `07_workflow_sharing.md` — Converting UI workflows to API JSON and sharing via `uvx`.

#### Automation & Scaling

- `06_scaling_automation.md` — Daemon processing and Python embedded client logic (CSV loops).

#### Troubleshooting & Vendor Specs

- `08_troubleshooting_logs.md` — OOM escalation paths, reading logs, and the Developer Escape hatch.
- `09_vendor_prompting.md` — The authoritative index of official vendor prompting URLs (Flux, Wan, LTX, etc.).

#### Pro-Level Development & Architecture

- `00_coding_style.md` — Global coding style, variable naming, linting mandates, and MRE creation.
- `10_workflow_architecture.md` — Graph primitive decoupling, logic grouping, and modular loaders.
- `11_api_and_node_dev.md` — Headless websocket integration, interrupt strategies, and backend custom node class rules.
- `12_frontend_litegraph_dev.md` — Frontend node development, LiteGraph widget handling, and Vue integration.

## 🙏 Acknowledgments
- Special thanks to **doctorpangloss** from the ComfyUI Discord channel for technical insights and foundational knowledge.
- Built upon and inspired by the [llms.txt protocol](https://github.com/hiddenswitch/pip-and-uv-installable-ComfyUI/blob/master/llms.txt) by Hiddenswitch.
