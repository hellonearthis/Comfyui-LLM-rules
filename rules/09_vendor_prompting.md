---
name: 09_vendor_prompting
description: Load this when generating prompts for specific model families (Flux, Wan, Hunyuan) to fetch their schemas.
---

# PROTOCOL 9: VENDOR PROMPTING (FETCH ON DEMAND)

**MANDATE:** When rewriting user prompts for specific model families, **MUST** use WebFetch to read the vendor's official guide *before* generating. Do not cache these locally; re-fetch to ensure adherence to current vendor schemas, negative prompt handling, and token limits.

## OFFICIAL VENDOR URLs
- **Flux.1 / Flux.1 Kontext (Black Forest Labs):**
  - Summary: `https://docs.bfl.ml/guides/prompting_summary`
  - Fundamentals (T2I): `https://docs.bfl.ml/guides/prompting_guide_t2i_fundamentals`
  - Kontext (I2I/Edit): `https://docs.bfl.ml/guides/prompting_guide_kontext_i2i` (Note: 512-token limit)

- **Flux.2 (Black Forest Labs):**
  - Flux.2 [pro]/[dev]: `https://docs.bfl.ml/guides/prompting_guide_flux2`
  - Flux.2 Klein 9B: `https://docs.bfl.ml/guides/prompting_guide_flux2_klein` (Note: Scene-first prose)

- **Wan 2.x (Alibaba):**
  - T2V/I2V Formula: `https://www.alibabacloud.com/help/en/model-studio/text-to-video-prompt`

- **Qwen-Image / Qwen-Image-Edit (Alibaba):**
  - Editor Guide: `https://www.alibabacloud.com/help/en/model-studio/qwen-image-edit-guide`

- **Z-Image Turbo (Tongyi-MAI):**
  - Card: `https://huggingface.co/Tongyi-MAI/Z-Image-Turbo` (Note: No negative prompts; 512-token limit)

- **Hunyuan Image 3.0 / Video 1.5 (Tencent):**
  - Image: `https://github.com/Tencent-Hunyuan/HunyuanImage-3.0/blob/main/Hunyuan-Image3.md`
  - Video: `https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5/blob/main/assets/HunyuanVideo_1_5_Prompt_Handbook_EN.md`

- **LTX-Video / LTXV 2 (Lightricks):**
  - LTX-Video: `https://github.com/Lightricks/LTX-Video/blob/main/README.md`
  - LTX-2: `https://github.com/Lightricks/LTX-2/blob/main/README.md` (Note: <200 words, chronological)

- **ChronoEdit (NVIDIA):**
  - Prompt Guidance: `https://github.com/nv-tlabs/ChronoEdit/blob/main/docs/PROMPT_GUIDANCE.md`

- **OmniGen2 (VectorSpaceLab):**
  - In-Context Template: `https://github.com/VectorSpaceLab/OmniGen2`

- **Chroma (lodestones):**
  - Guide: `https://huggingface.co/lodestones/Chroma1-HD` (Note: Tag-with-periods syntax)

- **Anima (circlestone-labs):**
  - Anime T2I: `https://huggingface.co/circlestone-labs/Anima` (Note: Danbooru tags, order: quality -> char count -> char -> series)

- **NewBie-Image (NewBie-AI):**
  - Schema: `https://huggingface.co/NewBie-AI/NewBie-image-Exp0.1` (Note: XML prompt schema `<character_1>...`)

- **Stable Diffusion 3.5 (Stability AI):**
  - Prompt Guide: `https://stability.ai/learning-hub/stable-diffusion-3-5-prompt-guide`

- **HuMo (Phantom-video):**
  - Audio-Conditioned Video: `https://github.com/Phantom-video/HuMo`

- **ACE-Step 1.5 (ACE Studios):**
  - Music Generation: `https://github.com/ace-step/ACE-Step-1.5/blob/main/docs/en/Tutorial.md` (Note: Structural tags like `[Verse]`)
