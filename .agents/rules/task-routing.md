---
name: 03_task_routing_examples
description: Load this when generating CLI commands for Text-to-Image, Image-to-Image, or Video tasks.
---

# PROTOCOL 3: TASK ROUTING & EXAMPLES

## ROUTING TABLE
| TASK | RECOMMENDED WORKFLOW | KEY FLAGS |
|---|---|---|
| **T2I** | `image_flux2_text_to_image` | `--all --seed <N>` |
| **I2I / Edit** | `image_flux2_klein_9b_kv_image_edit` | `--image <URL> --prompt "<CHANGE> + <KEEP>"` |
| **T2V** | `video_ltx2_3_t2v` | `--all --width 768 --height 512` |
| **I2V** | `video_ltx2_3_i2v` | `--all --image <URL>` |

## CLI INVOCATION SYNTAX (RESTORED CONTEXT)

### T2I with LoRA (Flux2)
```bash
comfyui run-workflow image_flux2_text_to_image --all --novram \
    --seed 42 \
    --prompt "A ceramic teapot in the style of a studio ghibli key frame: ghiblistyle, soft watercolor." \
    --add-lora civitai://v/755852:0.8
```

### I2I / Edit with Reference (Klein 9B KV)
```bash
comfyui run-workflow image_flux2_klein_9b_kv_image_edit --all --novram \
    --seed 42 \
    --image "https://upload.wikimedia.org/wikipedia/en/d/d7/Harry_Potter_character_poster.jpg" \
    --prompt "Restyle this portrait as a Studio Ghibli animated film key frame: ghiblistyle. Keep the round glasses, the lightning-bolt scar, and the Gryffindor robe colors recognizable." \
    --add-lora civitai://v/755852:0.8
```

### Image-to-Video (LTX 2.3)
```bash
comfyui run-workflow video_ltx2_3_i2v --all --guess-settings \
    --image https://example.com/dancer.jpg \
    --prompt "Camera pans slowly right while the dancer continues the same motion. 3 seconds." \
    --seed 42
```
