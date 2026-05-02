---
name: security_hygiene
description: Load this when installing new custom nodes, sharing workflows, or organizing complex graph architectures.
---

# PROTOCOL: SECURITY & WORKFLOW HYGIENE

## 1. CUSTOM NODE AUDIT (SECURITY FIRST)
- **THREAT:** Custom nodes can execute arbitrary code (`os.system`, `subprocess`, `requests`).
- **PROTOCOL:**
    - **SCAN:** Before recommending a node, check its `__init__.py` or main logic for suspicious calls.
    - **SANDBOX:** If unsure, recommend running in a separate `.venv` or container first.
    - **OFFLINE:** Prefer nodes that support offline mode (no auto-downloading binaries during runtime).

## 2. API KEY & DATA PRIVACY
- **HYGIENE:** 
    - **NEVER** hardcode API keys (OpenAI, Anthropic, Civitai) in a Note node.
    - **USE** `.env` files or system environment variables.
    - **SCRUB:** Before sharing a `.json` workflow, scrub the `user_data` and any text-based keys from nodes.

## 3. WORKFLOW HYGIENE (SPAGHETTI PREVENTION)
- **GROUPS:** Mandatory for workflows with >10 nodes. Use distinct colors for different functional blocks (e.g., Red for Inputs, Blue for LoRA, Green for Upscale).
- **NOTES:** Every complex logical decision (e.g., a specific sampler choice or denoise value) **MUST** have a Note node explaining the "Why".
- **PRIMITIVES:** Convert frequently changed values (Seed, CFG, Denoise) to Primitives for a cleaner "Control Panel" at the top of the workflow.

## 4. DATA PERSISTENCE & VERSIONING
- **JSON > PNG:** Recommend saving primary workflows as `.json` files in a Git-tracked folder. Do not rely solely on PNG metadata for versioning.
- **USER FOLDER:** Periodically backup the `ComfyUI/user` directory. This contains:
    - Custom UI layouts.
    - Node favorites.
    - Theme configurations.

## 5. REPRODUCIBILITY PROTOCOL
- **ENVIRONMENT FREEZE:** When sharing a workflow for a specific model (like Flux), include a `requirements.txt` or a `pip freeze` snapshot of the tested Locked Set.
- **SHA HASHES:** When possible, specify the model SHA256 hashes in the documentation to ensure the user is using the correct quantized version.
