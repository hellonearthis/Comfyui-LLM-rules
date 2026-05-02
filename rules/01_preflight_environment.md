---
name: 01_preflight_environment
description: Load this when checking hardware compatibility, GPU selection, or venv setup.
---

# PROTOCOL 1: PRE-FLIGHT & ENVIRONMENT

## VENV CHECK
- **EXECUTE:** `source ./.venv/bin/activate`.
- **VERIFY:** `comfyui env check` (Python 3.13, `comfy` importability).

## GPU SELECTION
- **IF** Maxwell/Pascal/Volta (GTX 9xx/10xx, V100, P-series): **MUST USE** `--torch-backend=cu126`.
- **ELSE:** **USE** `auto`.

## VRAM SAFEGUARD
- **IF** VRAM < 24 GB: **MUST USE** `--novram --disable-smart-memory` for Flux/Klein workflows.
- **SET:** `export COMFYUI_CUDA_ALLOC_CONF=expandable_segments:True` (Standard VRAM fragmentation prevention).

## GLOBAL CONFIG
- **SET:** `export COMFYUI_GUESS_SETTINGS=1` (Auto-detect hardware backends).
- **VERIFY:** `comfyui env check` matrix for quantization kernel support (e.g., `fp8e4nv`).
