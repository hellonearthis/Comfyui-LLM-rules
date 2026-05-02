---
name: installation_troubleshooting
description: Load this when debugging environment setup, dependency conflicts, missing models, or version mismatches (Torch/CUDA/xFormers).
---

# PROTOCOL: INSTALLATION & SETUP TROUBLESHOOTING

## 1. VERSION HELL (TORCH/CUDA/XFORMERS)
- **SYMPTOM:** `"Torch not compiled with CUDA enabled"` or `"xformers wasn't built with CUDA support"`.
- **FIX:**
    - **VERIFY:** `comfyui env check` (Check for `CUDA available: True`).
    - **REINSTALL:** `uv pip install --force-reinstall torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124` (Adjust `cuXXX` to match driver).
    - **PINNING:** **IF** installing xformers, **USE** `--no-deps` to prevent it from downgrading Torch.

## 2. CUSTOM NODE DEPENDENCY CLASHES
- **SYMPTOM:** `ImportError`, `cannot import name 'cached_download'`, or nodes turning RED in UI.
- **FIX:**
    - **ISOLATE:** Check the node's `requirements.txt`.
    - **UPGRADE:** `uv pip install --upgrade transformers huggingface_hub`.
    - **CONFLICT SCAN:** `uv pip check` to find broken dependency trees.

## 3. MISSING MODELS & PATH CHAOS
- **SYMPTOM:** "Missing model" error even if model exists on disk.
- **FIX:**
    - **AUDIT:** Check `extra_model_paths.yaml`. Ensure it points to the absolute path of the model base folder.
    - **PLACEMENT:** 
        - Checkpoints -> `models/checkpoints`
        - VAE -> `models/vae`
        - LoRA -> `models/loras`
        - ControlNet -> `models/controlnet`
    - **SYMLINKS:** **IF** using symlinks on Windows, **VERIFY** with `dir /AL` that they aren't broken.

## 4. ENVIRONMENT CONFUSION (PORTABLE VS DESKTOP)
- **PORTABLE:** Uses embedded Python. **DO NOT** use system `pip`. **USE** `.\python_embeded\python.exe -m pip`.
- **DESKTOP:** Stores config in `%APPDATA%/ComfyUI`. Check there for `user_settings.json`.
- **VENV:** **ALWAYS** activate via `source .venv/bin/activate` before any CLI operations.

## 5. VRAM & RESOURCE SAFEGUARDS
- **OOM (Out of Memory):**
    - **IF** GPU < 12GB: **MUST USE** `--lowvram`.
    - **IF** GPU < 8GB: **MUST USE** `--novram`.
    - **FLUX/WAN:** Use GGUF or NF4 quantized versions to fit in VRAM.
- **STORAGE:** **IF** C: drive is full, **MOVE** models to a separate drive and update `extra_model_paths.yaml`.

## 6. STABILITY & UPDATES
- **STABLE APPROACH:** 
    - **BACKUP:** `cp -r ComfyUI ComfyUI_Backup` before updating.
    - **FREEZE:** If it works, **DO NOT** update unless a specific feature requires it.
    - **ROLLBACK:** `git checkout [commit_hash]` if a core update breaks custom nodes.
