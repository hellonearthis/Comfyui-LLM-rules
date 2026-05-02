---
name: dependency_management
description: Load this to resolve dependency oscillation loops, ABI mismatches, or when managing the Torch/CUDA/xFormers/SageAttention compatibility matrix.
---

# PROTOCOL: ADVANCED DEPENDENCY MANAGEMENT

## 1. THE LOCKED SET RULE
- **DEFINITION:** The following packages form a **Locked Set** and must be managed as a single compatibility matrix:
    `torch`, `torchvision`, `torchaudio`, `xformers`, `sageattention`, `triton`.
- **ACTION:** Never modify one package in this set without verifying the impact on the others.
- **FORBIDDEN:** `pip install torch -U` (Blind upgrades are strictly prohibited).

## 2. BASELINE CAPTURE (MANDATORY)
Before any package modification, you **MUST** capture the current state:
- **EXECUTE:** `pip freeze > requirements-backup.txt`.
- **VERIFY:** 
    - `python --version`
    - `python -c "import torch; print(torch.__version__, torch.version.cuda)"`
    - `nvidia-smi`

## 3. DEPENDENCY OSCILLATION LOOP DETECTION
- **SYMPTOM:** Package A upgrades/downgrades Package B, which then triggers a re-fix of Package A.
- **PROTOCOL:**
    1. **STOP** all automated fixes.
    2. **BUILD** a compatibility matrix manually (check versions for current Torch + CUDA).
    3. **PIN** all versions explicitly using a requirements file.
    4. **EXECUTE:** `uv pip install --no-deps` for secondary packages (like xformers) to prevent them from touching the core Torch install.

## 4. COMPATIBILITY MATRIX DEFAULTS (STABLE BASELINE)
Unless explicitly required otherwise, prefer this "Safe Zone" configuration:
- **Python:** 3.10 or 3.11 (Avoid 3.12 for legacy custom node support).
- **Torch:** 2.6.0+cu124 (or matching the current stable wheel).
- **xFormers:** 0.0.29 (Matches Torch 2.6).
- **SageAttention:** Verify Torch ABI compatibility before install.

## 5. RECOVERY & ENVIRONMENT PROTECTION
- **BACKUP:** `cp -r .venv .venv_backup` before major stack changes.
- **CLEAN SLATE:** If the environment is "trashed" (oscillation loop confirmed), **DO NOT** attempt piecemeal fixes.
    1. **WIPE:** `rmdir /s /q .venv`.
    2. **REBUILD:** Re-install the Locked Set from explicit wheel URLs.

## 6. WHEEL-FIRST & COMPILER VERIFICATION
- **RULE:** **NEVER** recommend or attempt source builds (`pip install .`, `setup.py`, or compilation) unless:
    1. No prebuilt wheel exists.
    2. User explicitly requests a developer setup.
    3. **VERIFIED:** Compiler toolchain is present (`cl.exe` for MSVC, `nvcc --version` for CUDA).
- **ASSUMPTION (WINDOWS):** Assume **NO** Visual Studio, **NO** CMake, and **NO** CUDA Toolkit are installed until proven otherwise.
- **ACTION:** Prioritize prebuilt wheels from official indices or trusted repositories (e.g., `download.pytorch.org`).

## 7. GRACEFUL DEGRADATION (STABILITY > SPEED)
- **PHILOSOPHY:** Working slowly is infinitely better than being broken fast.
- **PROTOCOL:**
    - **IF** an accelerator (SageAttention, xFormers, Triton) fails to install/load:
        1. **ABANDON** the install attempt immediately.
        2. **DEGRADE:** Disable the feature and fall back to standard **PyTorch SDPA**.
        3. **VERIFY:** Ensure the server boots and generates without the accelerator.
- **PRIORITY HIERARCHY:** 1. Stability -> 2. Reproducibility -> 3. Recoverability -> 4. Performance.

## 8. STARTUP LOG AUDIT (ABI MISMATCH)
- **SCAN:** Check startup logs for `undefined symbol` or `DLL load failed`.
- **CAUSE:** ABI mismatch (usually SageAttention or xFormers compiled against a different Torch version).
- **FIX:** Re-install the specific package matching the *exact* installed Torch version string.
