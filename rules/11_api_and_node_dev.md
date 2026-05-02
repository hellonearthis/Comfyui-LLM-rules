---
name: 11_api_and_node_dev
description: Load this when developing backend custom nodes (IS_CHANGED, VALIDATE_INPUTS) or implementing websockets.
---

# PROTOCOL 11: API & NODE DEVELOPMENT

## HEADLESS API INTEGRATION
- **WEBSOCKET LISTENER:** **MUST** listen to `/ws` for `executing`, `progress`, and `execution_cached` events. Do not rely solely on polling for final output.
- **INTERRUPT STRATEGY:** **MUST** implement a listener for `POST /interrupt`. Essential in production for killing runaway generations and preserving VRAM.
- **PROMPT MUTATION:** Use the API to send *only* mutated nodes or updated prompt strings rather than sending the full JSON graph for every small change.

## ADVANCED CUSTOM NODE DEVELOPMENT
When writing custom nodes, these class methods prevent engine breakage:

- **CACHING (`IS_CHANGED`):** **MUST** implement if node fetches external data (API, disk). Return a hash of the data to signal the engine to re-run or use cache.
- **DATA SINKS (`OUTPUT_NODE`):** **MUST SET** `OUTPUT_NODE = True` if the node performs an action without passing data to a successor (e.g., cloud upload, notification). Without this, the engine will skip the node.
- **GPU SAFETY (`VALIDATE_INPUTS`):** **MUST** implement to catch errors (mismatched dimensions, missing files) *before* VRAM allocation or model loading occurs.
- **UI DISCOVERABILITY:** Include `NODE_DISPLAY_NAME_MAPPINGS` and use clear `SEARCH_ALIASES` to ensure the UI's search functionality can find the node.

## DEVELOPER VALIDATION & CI
- **INTEGRITY CHECK:** **EXECUTE** `comfyui env check` to validate package versions, torch/CUDA alignment, and the backend × dtype support matrix.
- **EXECUTION TESTS:** Align logic with `test-unit.yml` and `test-ci.yml` patterns. 
- **STABILITY DASHBOARD:** Reference `ci.comfy.org` to verify cross-platform stability results on real GPU runners (Linux/Windows) before finalizing core modifications.
