---
name: 10_workflow_architecture
description: Load this when designing workflow graphs, decoupling primitives, or mapping requirements.
---

# PROTOCOL 10: WORKFLOW ARCHITECTURE

## DECOUPLING PRIMITIVES
- **MANDATE:** Use Primitive Nodes (integers, strings, floats) at the start of the graph.
- **RATIONALE:** Enables "API-friendly" graphs. Allows external scripts to override values via `--set` without hunting for specific node IDs.

## LOGIC BLOCKS (GROUPING/REROUTES)
- **MANDATE:** Use Groups to define Logic Blocks (e.g., "Sampler Block", "Upscale Block"). Use Reroutes to direct flow cleanly.
- **DOCUMENTATION:** **USE** `MarkdownNote` nodes within the graph to document rationale for specific settings (rendered in `run-workflow --help`).
- **RATIONALE:** Exposes data flow and identifies potential VRAM bottlenecks structurally.

## MODULAR LOADERS (CHECKPOINT VS. UNET)
- **MANDATE:** For modern architectures (Flux), separate loaders for Text Encoder, VAE, and Diffusion Model (UNet).
- **AVOID:** Single "Checkpoints" loaders.
- **RATIONALE:** Enables modular swaps without reloading the entire heavy model.

## DEPENDENCY MANAGEMENT
- **ANCHORING:** Use `extra_model_paths.yaml` to explicitly map model directories for consistent dev environments across machines. Avoid relying solely on auto-discovery.
- **REQUIREMENTS:** **EXECUTE** `comfyui workflows requirements <workflow.json>` to generate clean package lists and prevent dependency hell.
- **PROFILING:** **EXECUTE** `comfyui env check` regularly during node development to verify backend x dtype support (fp16 vs fp8).
