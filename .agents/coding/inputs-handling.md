---
name: 05_inputs_handling
description: Load this when the user provides an image URL, a social media link, or a PNG with an embedded workflow.
---

# PROTOCOL 5: INPUTS HANDLING

## SUPPORTED MEDIA SOURCES
Every `--image` / `--video` / `--audio` flag and workflow URI accepts these formats. The downloader handles caching transparently.

| Source | Format | Notes |
|---|---|---|
| **Direct HTTPS** | `https://example.com/foo.jpg` | Wikipedia, raw GitHub, Imgur direct, CDNs. |
| **Civitai Gallery** | `https://image.civitai.com/...` | Right-click "Copy image address" in browser. |
| **Hugging Face** | `hf://owner/repo/path` | Uses `hf_hub_download` + `HF_TOKEN`. |
| **S3 Object** | `s3://bucket/key` | Uses local AWS credentials. |
| **Local File** | `/abs/path` or `./rel/path` | Prefer absolute paths for portability. |

## SOCIAL MEDIA EXTRACTION (WebFetch)
- **IF** given a social media link (Pinterest, Reddit, Twitter/X):
- **DO NOT** pass the page URL directly to `--image`.
- **MUST** use WebFetch to extract the `<meta property="og:image">` tag from the page HTML, then pass *that* URL to `--image`.

## PNG EMBEDDED WORKFLOW EXTRACTION
- **IF** given a PNG file created by ComfyUI, A1111, Forge, or Fooocus:
- **EXECUTE:** `comfyui run-workflow ./screenshot.png --all`.
- The loader automatically extracts the embedded JSON or `parameters` text chunk and executes it.

## CIVITAI POST LINKS
- **IF** given a Civitai post link (not a direct image):
- **EXECUTE:** `--image https://civitai.com/api/v1/images?postId=<post-id> | jq -r '.items[0].url'`
