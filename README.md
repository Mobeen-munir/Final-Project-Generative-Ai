# Final-Project-Generative-Ai
ComicConsist: Adaptive identity/pose blending for character-consistent comic panel generation using Stable Diffusion, ControlNet, and IP-Adapter.
# ComicConsist

**Adaptive identity/pose blending for character-consistent comic panel generation.**

ComicConsist generates multi-panel comic strips from a character reference image
and a plain-text script. A lightweight gating MLP reads each panel's action text
and dynamically balances two competing objectives:

- **Identity consistency** (via IP-Adapter) — keep the character looking the same
- **Pose expressiveness** (via ControlNet + OpenPose) — allow dynamic poses in action panels

This adaptive blending outperforms a fixed-weight baseline on CLIP-I identity
consistency scores, especially on scripts that mix calm and action panels.

## Architecture

| Component | Role |
|---|---|
| Stable Diffusion 1.5 | Image generation backbone |
| ControlNet (OpenPose) | Pose conditioning |
| IP-Adapter | Identity/appearance conditioning |
| Gating MLP | Per-panel adaptive weight prediction |
| CLIP-I | Identity consistency evaluation metric |

## Setup

```bash
pip uninstall -y gradio gradio_client fastapi starlette pydantic numpy
pip install numpy==1.26.4
pip install gradio==4.44.1 gradio_client==1.3.0 fastapi==0.115.5 \
    starlette==0.41.3 "pydantic>=2.0,<2.10" \
    diffusers==0.30.0 transformers==4.44.2 accelerate==0.33.0 \
    controlnet-aux==0.0.9 sentence-transformers==3.0.1 safetensors
```

## Run

```bash
python comicconsist_app_fixed.py
```

Open the printed Gradio URL in a **new** browser tab.

## Usage

1. Upload a character reference photo
2. Enter your script (one panel description per line)
3. Select **Adaptive (ours)** mode
4. Click **Generate comic**

Output panels and the assembled strip are saved to `./comicconsist_outputs/`

## Results

Compare **Adaptive (ours)** vs **Fixed baseline** using the CLIP-I consistency
score shown after each run. Adaptive mode dynamically raises identity weight on
calm panels and pose weight on action panels.

## Authors

- Mobeen Munir
- Syed Raza Abbass
- Nabeeha Rafi
- Hurrain Mustafa

## Report 

[Project Comics.pdf](https://github.com/user-attachments/files/29252528/Project.Comics.pdf)
