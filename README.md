<div align="center">

# AEON-7

**NVFP4 quantizations · Abliterated LLMs · DGX Spark deployments · AI media production toolchain**

[![GitHub followers](https://img.shields.io/github/followers/AEON-7?style=flat&color=blue&logo=github&label=Followers)](https://github.com/AEON-7?tab=followers)
[![GitHub stars](https://img.shields.io/github/stars/AEON-7?style=flat&color=yellow&logo=github&label=Total%20Stars)](https://github.com/AEON-7)
![Focus](https://img.shields.io/badge/focus-NVFP4%20%7C%20DFlash%20%7C%20DGX%20Spark-orange)
![Stack](https://img.shields.io/badge/stack-vLLM%20%7C%20ComfyUI%20%7C%20PyTorch-green)

</div>

---

I build deployment-ready open releases for next-gen GPUs — NVFP4-quantized abliterated LLMs (Gemma 4, Qwen 3.6, Nemotron 3) running on **NVIDIA DGX Spark** (GB10 / Blackwell / sm_121a), DFlash speculative decoding, EAGLE drafters, and a complete agent-driven AI media production toolchain.

Everything below is **public, MIT/Apache-licensed, and reproducible** — Docker stacks, pre-built vLLM images, deployment guides, and benchmark numbers included.

---

## 🎬 AEON Media Production

> Open-source AI-driven media production toolchain. Five focused repositories — each generating one kind of media (music, radio drama, music video, cinematic video, or the base ComfyUI stack), all designed for AI agents through skill MD files and CLI scripts. **No node-graph wrangling.**

| Repo | What it does | ★ |
|---|---|---|
| **[comfyui-aeon-spark](https://github.com/AEON-7/comfyui-aeon-spark)** | Bleeding-edge ComfyUI for DGX Spark (CUDA 13 + SageAttention v3 + NVFP4 + 14 custom-node packs + Flux 2 Dev / LTX 2.3 22B / ACE-Step v1.5 XL Turbo pre-bundled). Foundation for every other repo in this section. | ![](https://img.shields.io/github/stars/AEON-7/comfyui-aeon-spark?style=flat&label=) |
| **[aeon-music-maker](https://github.com/AEON-7/aeon-music-maker)** | ACE Step 1.5 XL music generation with dynamics-preserving mastering chain (HPF → EQ → tape sat → LUFS gain-match → true-peak ceiling). FLAC-lossless output, auto-detected mastering presets, CLI-driven. | ![](https://img.shields.io/github/stars/AEON-7/aeon-music-maker?style=flat&label=) |
| **[aeon-radio-drama](https://github.com/AEON-7/aeon-radio-drama)** | Full-pipeline radio drama / audiobook production — dialogue (Qwen3-TTS) + music (ACE Step) + SFX (MMAudio / Stable Audio Open / ACE) + sidechain mix in one command. Three-Lock voice persistence. | ![](https://img.shields.io/github/stars/AEON-7/aeon-radio-drama?style=flat&label=) |
| **[aeon-music-video](https://github.com/AEON-7/aeon-music-video)** | Audio-reactive music video builder. librosa-driven beat / onset / RMS / spectral-centroid detection drives ffmpeg filter chains for synced visual effects. CPU-only — no GPU required. | ![](https://img.shields.io/github/stars/AEON-7/aeon-music-video?style=flat&label=) |
| **[aeon-movie-maker](https://github.com/AEON-7/aeon-movie-maker)** | Fast cinematic video via LTX 2.3 22B. Single clips, full screenplays with character continuity (last-frame carry-forward + per-character seed offsets), and sidechain-mixed final cuts. | ![](https://img.shields.io/github/stars/AEON-7/aeon-movie-maker?style=flat&label=) |

Each repo ships with `SKILL.md` + `AGENTS.md` for drop-in agent integration, `setup.sh` / `sync.sh` for installation, `.env.example` for config, and full attribution to upstream model creators.

---

## 💎 Gemma 4 Models — NVFP4 quantizations for DGX Spark

> Abliterated Gemma 4 deployments at NVFP4 precision (4-bit weights + 8-bit activations) for NVIDIA DGX Spark / Blackwell GPUs. Includes EAGLE speculative-decoding drafters for both base models.

| Repo | Model | Architecture | Description | ★ |
|---|---|---|---|---|
| **[Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4)** | Gemma 4 31B DECKARD HERETIC | Dense, thinking | NVFP4-quantized abliterated 31B dense reasoning model. AWQ_FULL + SVDQuant variants. | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4?style=flat&label=) |
| **[Gemma-4-26B-A4B-it-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-26B-A4B-it-Uncensored-NVFP4)** | Gemma 4 26B A4B-it | MoE | NVFP4-quantized 26B MoE. **50 tok/s single, 1430 tok/s aggregate** on DGX Spark. | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-26B-A4B-it-Uncensored-NVFP4?style=flat&label=) |
| **[supergemma4-26b-abliterated-multimodal-nvfp4](https://github.com/AEON-7/supergemma4-26b-abliterated-multimodal-nvfp4)** | SuperGemma 4 26B Abliterated Multimodal | MoE, multimodal | NVFP4 AWQ Full quantization for Blackwell GPUs. Pre-built vLLM container + patches included. | ![](https://img.shields.io/github/stars/AEON-7/supergemma4-26b-abliterated-multimodal-nvfp4?style=flat&label=) |
| **[Gemma-4-E4B-it-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-E4B-it-Uncensored-NVFP4)** | EAGLE drafter for 26B MoE | Speculative decoding | EAGLE E4B speculative-decoding drafter for the Gemma 4 26B MoE. NVFP4 AWQ. | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-E4B-it-Uncensored-NVFP4?style=flat&label=) |
| **[Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4)** | EAGLE drafter for 31B DECKARD | Speculative decoding | EAGLE E4B speculative-decoding drafter for the 31B DECKARD HERETIC. | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4?style=flat&label=) |

---

## 🐉 Qwen 3.5 Models

> Reserved for upcoming Qwen 3.5 abliterated NVFP4 deployments. _No releases yet — coming soon._

---

## 🐉 Qwen 3.6 Models — NVFP4 + DFlash on DGX Spark

> Lossless abliteration of Qwen 3.6 with hardware NVFP4 quantization, optionally combined with DFlash speculative decoding for higher single-stream throughput.

| Repo | Model | Architecture | Description | ★ |
|---|---|---|---|---|
| **[Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash)** | Qwen 3.6 27B AEON Ultimate Uncensored | Dense | Lossless abliteration with NVFP4 hardware quantization. **BF16 (51 GB) + NVFP4 (26 GB)** deployment guide, docker-compose, QuickStart. | ![](https://img.shields.io/github/stars/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash?style=flat&label=) |
| **[Qwen3.6-NVFP4-DFlash](https://github.com/AEON-7/Qwen3.6-NVFP4-DFlash)** | Qwen 3.6 35B-A3B-heretic | MoE | NVFP4 + DFlash speculative decoding on DGX Spark (GB10 / sm_121a). Source-built vLLM image + 7 patches + comprehensive deployment guide. | ![](https://img.shields.io/github/stars/AEON-7/Qwen3.6-NVFP4-DFlash?style=flat&label=) |

---

## 🌌 Nemotron Models

> NVIDIA Nemotron deployments for Blackwell-class hardware.

| Repo | Model | Architecture | Description | ★ |
|---|---|---|---|---|
| **[Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored](https://github.com/AEON-7/Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored)** | Nemotron 3 Nano Omni | 12-D abliterated multimodal | BF16 + NVFP4 multimodal reasoning model for DGX Spark / Blackwell. Source-built vLLM v0.20.0 image + 4 patches + benchmark + deployment guide. | ![](https://img.shields.io/github/stars/AEON-7/Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored?style=flat&label=) |

---

## 🛠️ Inference & Optimization Tools

> Lower-level building blocks: speculative decoding, KV-cache compression, quantization tooling, and vLLM image builds.

| Repo | What it does | ★ |
|---|---|---|
| **[vllm-dflash](https://github.com/AEON-7/vllm-dflash)** | DFlash vLLM for DGX Spark — Plug & Play Block-Diffusion Speculative Decoding. Pre-built Docker image with NVFP4, sm_121a kernels, and Qwen-targeted optimizations. | ![](https://img.shields.io/github/stars/AEON-7/vllm-dflash?style=flat&label=) |
| **[turboquant](https://github.com/AEON-7/turboquant)** | Near-optimal KV cache quantization for LLM inference (3-bit keys, 2-bit values) with Triton kernels + vLLM integration. | ![](https://img.shields.io/github/stars/AEON-7/turboquant?style=flat&label=) |
| **[Model-Optimizer](https://github.com/AEON-7/Model-Optimizer)** | Unified library of SOTA model-optimization techniques — quantization, pruning, distillation, speculative decoding — for TensorRT-LLM / TensorRT / vLLM deployment. | ![](https://img.shields.io/github/stars/AEON-7/Model-Optimizer?style=flat&label=) |
| **[modelopt-fast-moe](https://github.com/AEON-7/modelopt-fast-moe)** | MoE-targeted quantization + AWQ calibration tooling. NVFP4 routing, expert-aware modelopt. | ![](https://img.shields.io/github/stars/AEON-7/modelopt-fast-moe?style=flat&label=) |

---

## 🧪 Apps & Utilities

> Side projects, tools, and infrastructure that aren't model deployments but might be useful.

| Repo | What it does | ★ |
|---|---|---|
| **[matrix-voip-agent](https://github.com/AEON-7/matrix-voip-agent)** | Headless Matrix WebRTC voice agent — auto-answers VoIP calls and bridges audio to any AI agent via PipeWire. | ![](https://img.shields.io/github/stars/AEON-7/matrix-voip-agent?style=flat&label=) |
| **[cosmic-mind](https://github.com/AEON-7/cosmic-mind)** | Security-and-resiliency-focused deployment of the Quartz web app. A place to build your second mind and share it. | ![](https://img.shields.io/github/stars/AEON-7/cosmic-mind?style=flat&label=) |
| **[regex-builder](https://github.com/AEON-7/regex-builder)** | Simple and elegant RegEx builder. | ![](https://img.shields.io/github/stars/AEON-7/regex-builder?style=flat&label=) |
| **[quartz](https://github.com/AEON-7/quartz)** | Fast batteries-included static-site generator that transforms Markdown into fully functional websites. | ![](https://img.shields.io/github/stars/AEON-7/quartz?style=flat&label=) |

---

## 📊 Stats

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=AEON-7&show_icons=true&theme=dark&hide_border=true&include_all_commits=true&count_private=true)
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=AEON-7&layout=compact&theme=dark&hide_border=true&langs_count=8)

</div>

---

## ☕ Support the work

If any of these releases have been useful to you, tips are deeply appreciated — they go directly toward more compute, more models, and more open releases. Click any address below to copy.

| Currency |  | Address |
|---|---|---|
| **Bitcoin** (BTC) | ₿ | `bc1q09xmzn00q4z3c5raene0f3pzn9d9pvawfm0py4` |
| **Ethereum** (ETH) | Ξ | `0x1512667F6D61454ad531d2E45C0a5d1fd82D0500` |
| **Solana** (SOL) | ◎ | `DgQsjHdAnT5PNLQTNpJdpLS3tYGpVcsHQCkpoiAKsw8t` |
| **Monero** (XMR) | ⓜ | `836XrSKw4R76vNi3QPJ5Fa9ugcyvE2cWmKSPv3AhpTNNKvqP8v5ba9JRL4Vh7UnFNjDz3E2GXZDVVenu3rkZaNdUFhjAvgd` |

Tokens on EVM-compatible L2s (Base, Arbitrum, Optimism, Polygon, etc.) can be sent to the same Ethereum address.

---

## 🤝 Get in touch

- 🌐 Open an issue on any repo for questions, bug reports, or feature requests
- 📜 Most releases include a deployment guide + benchmark numbers — start there

<div align="center">

_Built for the open source community on NVIDIA DGX Spark, RTX 5090, and Blackwell-class GPUs._

</div>
