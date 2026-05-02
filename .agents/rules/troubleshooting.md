---
name: 08_troubleshooting_logs
description: Load this when diagnosing OOM errors, crashes, or when live server logs are needed.
---

# PROTOCOL 8: TROUBLESHOOTING & LOGS

## LOGGING & MONITORING PROTOCOL
- **CLI STREAM:** `comfyui logs -f` (Reads live server logs).
- **WS SUBSCRIPTION:** **USE** `PATCH /internal/logs/subscribe` for filtered, real-time feedback on errors.
- **PULSE CHECK:** Monitor `GET /queue` and `GET /history` to track job density and detect "hanging" workers.
- **REST API (LIVE):** `GET /internal/logs/raw` (JSON ring buffer).
- **DAEMON LOG:** Read `~/.comfyui/comfyui.log`.

## DIAGNOSTIC TOOLING
- **LOGIC TEST:** **EXECUTE** with `--novram` to verify if a crash is a logic error vs. VRAM allocation error.
- **CAPACITY:** **EXECUTE** `--all --dry-run` to verify disk space before 100GB+ downloads.
- **SCHEMA:** **EXECUTE** `comfyui nodes info <ClassName>` for authoritative input/output schema verification.

## OOM RESOLUTION (ESCALATION PATH)
**IF** CUDA OOM occurs:
1. **EXECUTE:** `--disable-smart-memory`. (Forces `unload_all_models()` between runs).
2. **EXECUTE:** `--novram`. (Streams weights per-module; mandatory for Klein/Flux on <24GB).
3. **SET:** `export COMFYUI_CUDA_ALLOC_CONF=expandable_segments:True` (Reduces fragmentation).

## CUSTOM NODES & PITFALLS
- **INSTALL:** Exclusively via pip facade:
  `uv pip install --extra-index-url https://nodes.appmana.com/simple/ <NODE_PACKAGE>`
- **SUBGRAPH IDS:** Use `comfyui workflows convert` + `jq 'keys'` to verify `"75:72"` style nested node IDs.
- **TRITON:** `fp8e4nv not supported` on Ampere (sm < 8.9) is expected. The runtime auto-disables the triton backend.

## DEVELOPER ESCAPE (CATASTROPHIC BUGS)
**IF** non-resolution bug detected (crash, NaN output, etc.):
1. **CLONE:** `git clone https://github.com/hiddenswitch/pip-and-uv-installable-ComfyUI.git`
2. **EDITABLE:** `uv pip install -e . --reinstall-package comfyui`
3. **TRACE:** Inject `print()` / `logger.warning()` in suspected node via `class_type` grep.
4. **MAINTAINER:** Join Discord (<https://discord.gg/sjscAyeTBs>). Ping `@doctorpangloss` with Summary, Repro, Env Info, and Hypothesis.
