---
name: 06_scaling_automation
description: Load this when writing Python embedded client scripts, batch jobs, or daemon logic.
---

# PROTOCOL 6: SCALING & AUTOMATION

## MASS PROCESSING (DAEMON)
For tens-to-thousands of jobs, use the daemon to keep models resident in VRAM.
1. **START DAEMON:** `comfyui start`.
2. **SUBMIT:** `comfyui workflows submit <WF> --prompt "<PROMPT>" --seed <SEED>`.
3. **POLL / CANCEL:** `comfyui jobs` / `comfyui jobs cancel <JOB_ID>`.
4. **STOP:** `comfyui stop`.

## PYTHON INTEGRATION (EMBEDDED CLIENT)
For CSV-driven bulk jobs or complex graph mutations, use an ad-hoc Python script. This avoids spawning `run-workflow` per row.

```python
import asyncio, csv
from pathlib import Path
from comfy.cli_args_types import Configuration
from comfy.entrypoints.workflow import run_workflows

async def main():
    rows = list(csv.DictReader(Path("prompts.csv").open()))
    for i, row in enumerate(rows):
        config = Configuration(
            prompt=row["prompt"],
            seed=int(row.get("seed", 42 + i)),
            novram=True,
            output_directory=f"out/row_{i:04d}",
            workflows=["image_flux2_klein_text_to_image"],
        )
        await run_workflows(config.workflows, configuration=config)

asyncio.run(main())
```

## TIGHT-LOOP SUBMISSION TEMPLATE
```python
import asyncio, httpx
from comfy.component_model.prompt_utils import add_loras, enable_compile
from comfy.component_model.asyncio_files import load_workflow_json

async def submit(client, wf_name, prompt, loras):
    wf = add_loras(load_workflow_json(wf_name), loras)
    wf = enable_compile(wf)
    r = await client.post("http://localhost:8188/prompt", json={"prompt": wf})
    return r.json()["prompt_id"]
```
