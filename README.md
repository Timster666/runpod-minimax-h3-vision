# MiniMax H3 Vision

Ready-to-use ComfyUI with **[MiniMax H3 Vision](https://github.com/Timster666/comfyui-minimax-h3-vision)**, a simple studio for MiniMax H3 videos and MOSS-Image pictures with a small editor, plus JupyterLab. Everything downloads by itself on the first start. Nothing to install.

MiniMax H3 Vision has three tabs:

- **Video:** prompt-to-video with MiniMax H3, with `@image` references, LoRAs and a moving live preview.
- **Image:** pictures with MOSS-Image, which is good at words in pictures.
- **Edit:** put your videos together on a timeline and export one MP4.

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

**All recommended LoRAs:** the **MMH3 Realism V2** LoRA and the **MiniMax H3 Turbo** LoRA.

**Also included:** the MiniMax H3 text encoder, video and audio VAEs, the MOSS-Image text encoder and VAE, and the moving live preview (taeh3).

**Plus:** ComfyUI + ComfyUI-Manager, JupyterLab (no password) and PyTorch for CUDA 13.0.

## Start here

1. Pick a GPU with **48 GB+ VRAM** (L40S, A6000, A100, H100, RTX PRO 6000) and **64 GB+ system RAM**.
2. Set the **CUDA filter to 13.0+** and the **Volume Disk to 200 GB**.
3. Deploy. The first start downloads about 160 GB of models (15–25 min). Watch the **Logs** for `Starting ComfyUI on port 8188`.
4. Click **Connect → ComfyUI**. **MiniMax H3 Vision** is in the left sidebar.

Later starts are much faster, because the models are already there. Each start also updates MiniMax H3 Vision to its newest version.

## Save space or money

Every model has an on/off switch. Click **Edit Template** when you deploy and set the ones you don't need to `false` in the **Environment Variables**:

| Switch | Model | Saves |
|---|---|---|
| `ENABLE_MINIMAX_H3` | MiniMax H3 + Turbo | 42 GB |
| `ENABLE_SINGULARITY` | Singularity v2 | 21 GB |
| `ENABLE_10EROS` | 10Eros Max beta 7 | 23 GB |
| `ENABLE_MOSS_TURBO` | MOSS-Image 8-step turbo | 5.4 GB |
| `ENABLE_MOSS_IMAGE` | MOSS-Image (the whole Image tab) | about 18 GB with the turbo |

With the first three off, a **100 GB** volume is enough.

## Other settings
| Variable | Default | What it does |
|---|---|---|
| `UPDATE_VISION` | `true` | `false` = keep the MiniMax H3 Vision version on the volume |
| `UPDATE_COMFYUI` | `false` | `true` = update ComfyUI on start |
| `JUPYTER_PASSWORD` | — | Set to require a Jupyter login |
| `CIVITAI_TOKEN` | — | Only if Civitai asks for a login for the Realism LoRA |

## Where things are saved
Everything is in `/workspace/ComfyUI`: `models`, `custom_nodes`, `output` and more. Your videos, images, edits and exports are in `output/minimax_flow`. Custom nodes you install stay between restarts.

## Ports
`8188` ComfyUI · `8888` JupyterLab · `22` SSH

## Licenses
MiniMax H3 and the models built on it use the **MiniMax H3 Community License**: check it before commercial use. MOSS-Image has its own license, and so do the LoRAs. MiniMax H3 Vision is GPL-3.0.
