---
name: coding-style
description: Global standards for variable naming, comment structures, linting, and testing in ComfyUI custom node development.
---

# PROTOCOL 00: CODING STYLE & DEVELOPMENT STANDARDS

## 1. VARIABLE NAMING
- **JavaScript/TypeScript:** Use `camelCase` for variables and functions. Use `PascalCase` for LiteGraph components, Vue components, and Classes.
- **Python:** Use `snake_case` for all variables and function names.
- **Hardware-Specific:** When referencing target hardware constraints (e.g., specific GPU features or VRAM limits), prefix variables with `hw_` (e.g., `hw_vram_limit`).
- **Booleans:** Must start with a verb (e.g., `is_active`, `has_metadata`, `should_render`).

## 2. COMMENTING RULES
- **Purpose over Process:** Do not comment *what* the code is doing (the code should be readable). Comment *why* it is doing it.
- **Docstrings:** Every exported function must have a brief Docstring (Python) or JSDoc (JS) block.
- **ComfyUI Specific:** For custom nodes, include a comment block at the top detailing the `INPUT_TYPES` requirements.
- **Todo Tags:** Use `// TODO:` or `# TODO:` for incomplete logic to track technical debt.

## 3. LINTING & VALIDATE MANDATE
- **MANDATORY:** Before finalizing any custom Python node, **MUST** run a linter (e.g., `ruff check .` or `flake8`) to ensure Python 3.13 compliance and catch syntax errors prior to runtime.
- **VALIDATION:** **EXECUTE** `comfyui run-workflow --all --dry-run` to validate dependencies and model requirements without sampling.

## 4. MINIMAL REPRODUCIBLE EXAMPLE (MRE) MANDATE
- **MANDATORY:** When delivering a new custom node or a complex scaling script, **MUST** generate a minimal `test_workflow.json` containing only primitive inputs and the new node.
- **ALIGNMENT:** Backend logic **MUST** align with `test-unit.yml` standards to ensure compatibility with ComfyUI's automated CI.
