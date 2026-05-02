---
name: 04_asset_auth_logic
description: Load this when handling URIs (hf://, civitai://), authentication, or foreign format translations.
---

# PROTOCOL 4: ASSET & AUTH LOGIC

## URI PRIORITY
- **Hugging Face:** Use `hf://<OWNER>/<REPO>/<PATH>`.
- **Civitai:** Use `civitai://<ID>`.
- **ORDER:** `hf://` > `civitai://`.
- **QUANTIZATION:** IF VRAM-constrained, **PRIORITIZE** GGUF or EXL2 formats over standard `.safetensors`.

## VAE & MERGING LOGIC
- **VAE DISTINCTION:** Always verify IF workflow uses "baked-in" or standalone VAE. **USE** standalone (e.g., `ae.safetensors`) for Flux to prevent artifacts.
- **MERGING:** **USE** `ModelMerge` nodes instead of external scripts to keep provenance inside the workflow JSON.

## AUTHENTICATION
- **Civitai:** Verify `CIVITAI_API_TOKEN` for `civitai://` URIs.
- **Hugging Face:** Execute `huggingface-cli login` for gated repos (e.g., Flux-Dev). **MANDATORY:** Must also manually "Agree to terms" on the repo page.

## FOREIGN FORMAT TRANSLATION
- **AUTO:** A1111/Forge `.txt` parameter dumps -> ComfyUI graph.
- **AUTO:** Fooocus JSON presets -> ComfyUI graph.
- **FAIL:** SwarmUI/InvokeAI/Krita-AI shapes -> `UnsupportedWorkflowFormatError`.

## RESOLUTION MECHANICS (UNDER THE HOOD)
1. **HF:** `hf_hub_download` local check.
2. **DISK:** Native indexer query (`Spotlight`/`ADODB`/`locate`).
3. **CLASS:** Map to `folder_paths` by parent dir name.
4. **REG:** `add_model_folder_path` (No moves/links).
5. **DL:** Fetch remaining unresolved assets.

## DRY-RUN AUDIT
- **EXECUTE:** `comfyui models from-workflow <TEMPLATE> --dry-run`.
- **IDENTIFY:** Large downloads before triggering.
