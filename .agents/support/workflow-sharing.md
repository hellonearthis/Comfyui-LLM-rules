---
name: 07_workflow_sharing
description: Load this when converting UI workflows to API JSON or sharing workflows via uvx.
---

# PROTOCOL 7: WORKFLOW SHARING

## THE `uvx` SHAREABLE FORMAT
The best shareable unit of work is a single `uvx` one-liner. Recipients do not need a venv, git clone, or prior pip install.

**MANDATORY FORMAT:**
```bash
uvx --from 'comfyui @ git+https://github.com/hiddenswitch/pip-and-uv-installable-ComfyUI.git' \
    --torch-backend=auto \
    comfyui workflows run <URI_OR_TEMPLATE> -a -g \
    --prompt '<PROMPT>' \
    [--add-lora <URI>:<WT>]
```
- `-a`: Auto-fetches missing models (`--all`).
- `-g`: Auto-detects VRAM/attention backend (`--guess-settings`).

## PREPARING A SHARE COMMAND
1. **DRY-RUN:** Execute `comfyui models from-workflow <TEMPLATE> --dry-run`.
2. **VERIFY:** Ensure paths in `stderr` use canonical URLs (`hf://` or `civitai://`).
3. **MANDATE:** **NO LOCAL PATHS**. Avoid absolute local paths (e.g., `C:\Users\...`); **MUST** use relative paths or resolvable URIs.
4. **REQUIREMENTS:** **EXECUTE** `comfyui workflows requirements <wf.json>` to generate `requirements.txt` for custom node dependencies.

## UI-EXPORTED WORKFLOWS (WITH SUBGRAPHS)
- **IF** the workflow was exported from the UI and contains subgraphs:
- **MUST EXECUTE:** `comfyui workflows convert my_wf.json -o my_wf_api.json`.
- Host the resulting API JSON (gist, repo, HTTP static host) and share the raw URL as the `<URI_OR_TEMPLATE>`.
