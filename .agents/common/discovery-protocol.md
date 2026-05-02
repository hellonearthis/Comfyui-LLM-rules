---
name: 02_discovery_protocol
description: Load this when searching for models, extracting trigger words, or auditing workflow URLs.
---

# PROTOCOL 2: DISCOVERY PROTOCOL (SEARCH-FIRST)

## ZERO GUESSING MANDATE
- Execution **MUST** be preceded by `comfyui models search "<QUERY>"` for any requested style or character.

## TRIGGER WORD EXTRACTION
- **EXECUTE:** `comfyui models search "<QUERY>" --kind lora --base-model "<BASE>" --json | jq '.[0] | {uri, trigger_words}'`.
- **EXTRACT:** `trigger_words`.
- **MANDATORY:** Trigger words **MUST** be included in the `<PROMPT>` verbatim; ELSE LoRA fails.

## WORKFLOW AUDIT
- **IF** using external URLs: **MUST EXECUTE** `comfyui run-workflow <URL> --help`.
- **EXTRACT:** `MarkdownNote` requirements, explicit model instructions, and examples.
