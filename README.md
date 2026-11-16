# MiniMax H3 Vision

Ready-to-use ComfyUI with **[MiniMax H3 Vision](https://github.com/Timster666/comfyui-minimax-h3-vision)**, a simple studio for MiniMax H3 videos and MOSS-Image pictures with a small editor, plus JupyterLab. Everything downloads by itself on the first start. Nothing to install.

MiniMax H3 Vision has three tabs:

- **Video:** prompt-to-video with MiniMax H3, with `@image` references, LoRAs and a moving live preview.
- **Image:** pictures with MOSS-Image, which is good at words in pictures.
- **Edit:** put your videos together on a timeline and export one MP4.

The image also has [LanPaint](https://github.com/scraed/LanPaint), the inpainting sampler the Klein tab's face swap can use with **Only the head**.

## Included by default

**Video models, all in the Video tab's model menu:**

| Model | Size |
|---|---|
| **HyperFlow H3 Flash** (default, fastest) | 32 GB |
| **MiniMax H3** and **MiniMax H3 Turbo** | 42 GB |
| **Singularity v2** | 21 GB |
| **10Eros Max beta 7** | 23 GB |

**Image models, in the Image tab's model menu:**

| Model | Size |
|---|---|
| **MOSS-Image SFT (INT8)** | 5.4 GB |
| **MOSS-Image SFT Turbo 8-step (INT8)** | 5.4 GB |
| **MOSS-Image SFT (BF16)**, the full-size model | 10.2 GB |

**All recommended LoRAs:** the **MMH3 Realism V2** LoRA and the **MiniMax H3 Turbo** LoRA.

**LoRA folders:** `models/loras` has a folder per model, and each tab of MiniMax H3 Vision lists its own:
`MiniMax H3` (Video), `MOSS Image` (Image) and `Flux Klein` (coming). Put new LoRAs in the right one;
loose files still show everywhere, as Not sorted. The built-in LoRAs go into `MiniMax H3`, and copies
that earlier versions left loose in `loras` are moved there on start.

**Also included:** the MiniMax H3 text encoder, video and audio VAEs, the MOSS-Image text encoder and VAE, and the moving live preview (taeh3).

**Plus:** ComfyUI + ComfyUI-Manager, JupyterLab (no password) and PyTorch for CUDA 13.0.

## Start here

1. Pick a GPU with **48 GB+ VRAM** (L40S, A6000, A100, H100, RTX PRO 6000) and **64 GB+ system RAM**.
2. Set the **CUDA filter to 13.0+** and the **Volume Disk to 200 GB**.
3. Deploy. The first start downloads about 170 GB of models (15–25 min). Watch the **Logs** for `Starting ComfyUI on port 8188`.
4. Click **Connect → ComfyUI**. **MiniMax H3 Vision** is in the left sidebar.

Later starts are much faster, because the models are already there. Each start also updates MiniMax H3 Vision to its newest version.

## Save space or money

You can also leave models off and download them later from inside Vision: **gear menu → Models** lists every
model group with its size and a **Download** button, and downloads run in the background on the pod. Both use
the same list (Vision's `model_catalog.json`), so a switch and the Models page always fetch the same files.

Every model has an on/off switch. Click **Edit Template** when you deploy and set the ones you don't need to `false` in the **Environment Variables**:

| Switch | Model | Saves |
|---|---|---|
| `ENABLE_MINIMAX_H3` | MiniMax H3 + Turbo | 42 GB |
| `ENABLE_SINGULARITY` | Singularity v2 | 21 GB |
| `ENABLE_10EROS` | 10Eros Max beta 7 | 23 GB |
| `ENABLE_MOSS_TURBO` | MOSS-Image 8-step turbo | 5.4 GB |
| `ENABLE_MOSS_BF16` | MOSS-Image SFT full-size BF16 | 10.2 GB |
| `ENABLE_MOSS_EDIT` | MOSS-Image edit LoRA, for the Image tab's **Edit** (into `loras/MOSS Image`) | 297 MB |
| `ENABLE_MOSS_IMAGE` | MOSS-Image (the whole Image tab) | about 28 GB with the turbo and BF16 |
| `ENABLE_KLEIN_9B_BF16` | FLUX.2 [klein] 9B Distilled, full BF16 (about 18 GB), with its text encoder (8.1 GB) and VAE. **On**, needs `HF_TOKEN` | the model, encoder and VAE |
| `ENABLE_KLEIN_9B` | FLUX.2 [klein] 9B Distilled fp8 (about half the size, faster), to compare. **Off**, needs `HF_TOKEN` | the model |
| `ENABLE_KLEIN_9B_BASE` | FLUX.2 [klein] 9B Base fp8 (undistilled, slower). **Off**, needs `HF_TOKEN` | the model |
| `ENABLE_BFS_KLEIN` | BFS head-swap LoRAs for Klein 9B (Alissonerdx/BFS-Best-Face-Swap, rank 128 and rank 64) for the Klein tab's **Face swap**, into `loras/Flux Klein`. Only with a Klein model | the LoRAs |
| `ENABLE_PH3_IMAGE` | P-H3-Image for the **Pruna** tab: Pruna's LoRA (1.8 GB, into `loras/P-H3 Image`) on MiniMax H3's FL2VA model, with its INT8 text encoder (4.8 GB) and VAE (2.9 GB). Downloads FL2VA (19.5 GB) too when `ENABLE_MINIMAX_H3` is off | about 9.5 GB |
| `ENABLE_PH3_UPSAMPLER` | P-H3-Image's BF16 prompt upsampler, for the Pruna tab's **Enhance prompt** | 19.3 GB |

With the first three off, a **100 GB** volume is enough.

## Other settings
| Variable | Default | What it does |
|---|---|---|
| `UPDATE_VISION` | `true` | `false` = keep the MiniMax H3 Vision version on the volume |
| `UPDATE_COMFYUI` | `false` | `true` = update ComfyUI on start |
| `JUPYTER_PASSWORD` | — | Set to require a Jupyter login |
| `HF_TOKEN` | — | Needed for Klein: a Hugging Face read token from an account that accepted the FLUX Non-Commercial License on [FLUX.2-klein-9B](https://huggingface.co/black-forest-labs/FLUX.2-klein-9B) (and [FLUX.2-klein-9b-fp8](https://huggingface.co/black-forest-labs/FLUX.2-klein-9b-fp8) or [FLUX.2-klein-base-9b-fp8](https://huggingface.co/black-forest-labs/FLUX.2-klein-base-9b-fp8) if you switch those on). Without it, Klein is skipped with a warning in the log |
| `CIVITAI_TOKEN` | — | Only if Civitai asks for a login for the Realism LoRA |

## Where things are saved
Everything is in `/workspace/ComfyUI`: `models`, `custom_nodes`, `output` and more. Your videos, images, edits and exports are in `output/minimax_flow`. Custom nodes you install stay between restarts.

## Ports
`8188` ComfyUI · `8888` JupyterLab · `22` SSH

## Licenses
MiniMax H3 and the models built on it use the **MiniMax H3 Community License**: check it before commercial use. MOSS-Image has its own license, and so do the LoRAs. FLUX.2 [klein] 9B is under the FLUX Non-Commercial License. MiniMax H3 Vision is GPL-3.0.
