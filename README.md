<div align="center">

[![Tips](https://img.shields.io/badge/%E2%98%95_Tips-Support_the_work-ff5e5b?style=flat)](#-support-the-work)

# AEON-7

**NVFP4 quantizations · Abliterated LLMs · DGX Spark deployments · Apple Silicon MLX · AI media production**

[![GitHub followers](https://img.shields.io/github/followers/AEON-7?style=flat&color=blue&logo=github&label=Followers)](https://github.com/AEON-7?tab=followers)
[![GitHub stars](https://img.shields.io/github/stars/AEON-7?style=flat&color=yellow&logo=github&label=Total%20Stars)](https://github.com/AEON-7)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-AEON--7-yellow)](https://huggingface.co/AEON-7)
![Focus](https://img.shields.io/badge/focus-NVFP4%20%7C%20DFlash%20%7C%20DGX%20Spark-orange)
![Stack](https://img.shields.io/badge/stack-vLLM%20%7C%20ComfyUI%20%7C%20MLX%20%7C%20PyTorch-green)

</div>

---

I build deployment-ready open releases for next-gen hardware — NVFP4-quantized abliterated LLMs (Gemma 4, Qwen 3.6, Nemotron 3) on **NVIDIA DGX Spark** (GB10 / Blackwell / sm_121a), DFlash + EAGLE speculative decoding, **Apple Silicon MLX** builds for M-series Macs, a real-time voice-AI stack, and a complete agent-driven AI media production toolchain.

Everything below is **public, MIT/Apache-licensed, and reproducible** — Docker stacks, pre-built vLLM images, deployment guides, and benchmark numbers included. Model weights live on [🤗 Hugging Face](https://huggingface.co/AEON-7).

---

## 📑 Contents

| Section | What you'll find there |
|---|---|
| [🎬 AEON Media Production](#-aeon-media-production) | Agent-driven media generation — music, radio drama, music videos, cinematic film, and the ComfyUI base stack that powers them |
| [🎤 Voice and Video AI Stack](#-voice-and-video-ai-stack) | Real-time speech and vision on one DGX Spark — OpenAI-compatible TTS + ASR servers, Matrix VoIP bridge with camera-frame vision for video calls, AI persona builder. **~2.1 s end-to-end voice turns** |
| [💎 Gemma 4 Models](#-gemma-4-models) | Abliterated Gemma 4 NVFP4 quantizations, EAGLE drafters, and a 3.5×-faster DFlash serving container |
| [🍎 Apple Silicon MLX](#-apple-silicon-mlx) | Gemma-4-12B AEON Abliterated on M-series Macs — MLX quants + one-paste OpenAI-compatible multimodal server |
| [🐉 Qwen 3.6 Models](#-qwen-36-models) | The flagship line — lossless-abliterated Qwen 3.6 dense + MoE at NVFP4, production DFlash path and the DDTree research track |
| [🌌 Nemotron Models](#-nemotron-models) | Abliterated multimodal Nemotron 3 reasoning for Blackwell-class hardware |
| [🔧 Inference and Optimization Tools](#-inference-and-optimization-tools) | The engine room — AEON vLLM Ultimate unified image, DFlash, TurboQuant KV compression, modelopt tooling |
| [📦 Pre-built Docker Images](#-pre-built-docker-images) | Every public `ghcr.io/aeon-7` container mapped to its repo — `docker pull` and go |
| [🧪 Apps and Utilities](#-apps-and-utilities) | AI network management, digital gardens, and small sharp tools |
| [📊 Stats](#-stats) · [☕ Support](#-support-the-work) · [🤝 Contact](#-get-in-touch) | Numbers, tips, and how to reach me |

---

## 🎬 AEON Media Production

> Open-source AI-driven media production toolchain. Five focused repositories — each generating one kind of media (music, radio drama, music video, cinematic video, or the base ComfyUI stack), all designed for AI agents through skill MD files and CLI scripts. **No node-graph wrangling.**

| Repo | What it does | ★ |
|---|---|---|
| **[comfyui-aeon-spark](https://github.com/AEON-7/comfyui-aeon-spark)** | Bleeding-edge ComfyUI for DGX Spark (CUDA 13 + SageAttention v3 + NVFP4 + 14 custom-node packs + Flux 2 Dev / LTX 2.3 22B / ACE-Step v1.5 XL Turbo pre-bundled). Foundation for every other repo in this section. | ![](https://img.shields.io/github/stars/AEON-7/comfyui-aeon-spark?style=flat&label=) |
| **[aeon-music-maker](https://github.com/AEON-7/aeon-music-maker)** | ACE Step 1.5 XL music generation with dynamics-preserving mastering chain (HPF → EQ → tape sat → LUFS gain-match → true-peak ceiling). FLAC-lossless output, auto-detected mastering presets, CLI-driven. | ![](https://img.shields.io/github/stars/AEON-7/aeon-music-maker?style=flat&label=) |
| **[aeon-radio-drama](https://github.com/AEON-7/aeon-radio-drama)** | Full-pipeline radio drama / audiobook production — dialogue (Qwen3-TTS) + music (ACE Step) + SFX (MMAudio / Stable Audio Open / ACE) + sidechain mix in one command. Three-Lock voice persistence. Bundles standalone `music_maker.py` + `sfx_maker.py` for one-shot music or SFX generation. | ![](https://img.shields.io/github/stars/AEON-7/aeon-radio-drama?style=flat&label=) |
| **[aeon-music-video](https://github.com/AEON-7/aeon-music-video)** | Audio-reactive music video builder. librosa-driven beat / onset / RMS / spectral-centroid detection drives ffmpeg filter chains for synced visual effects. CPU-only — no GPU, no ComfyUI, no model downloads required. | ![](https://img.shields.io/github/stars/AEON-7/aeon-music-video?style=flat&label=) |
| **[aeon-movie-maker](https://github.com/AEON-7/aeon-movie-maker)** | Fast cinematic video via LTX 2.3 22B. Single clips, full screenplays with character continuity (last-frame carry-forward + per-character seed offsets), and sidechain-mixed final cuts. CLI-tunable LoRA strengths + saturation troubleshooting guide. | ![](https://img.shields.io/github/stars/AEON-7/aeon-movie-maker?style=flat&label=) |

### What every AEON Media Production repo ships with

| File | What it is |
|---|---|
| `README.md` | Quick start, configuration table, local-vs-remote ComfyUI execution modes, env-var reference, model-installation paths |
| `AGENTS.md` | Step-0 execution-mode detection guide for AI agents, invocation contract, recovery patterns |
| `SKILL.md` | Full prompt-engineering recipes, troubleshooting decision trees, the canonical agent skill definition |
| `ATTRIBUTION.md` | Upstream credits — every model, library, and custom node properly attributed |
| `.env.example` | Verbose, self-documenting — every variable has inline instructions on where to get values (HF tokens, Civitai tokens, ComfyUI URL patterns) |
| `setup.sh` | First-time install — validates ComfyUI reachability, installs Python deps, inventories model files, prints download commands for missing pieces |
| `sync.sh` | Incremental update — diff preview, auto-stash local edits, ff-only pull, refresh deps, re-run model check. Supports `--dry-run` / `--yes` / `--no-models` |
| `.gitignore` | Standard — never commits `output/`, `models/`, `.env`, `__pycache__`, etc. |
| `LICENSE` | MIT |

### Lifecycle (every repo, same pattern)

```
git clone https://github.com/AEON-7/<repo>     →   ./setup.sh        →   start using
                                                       │
                                                       ▼
                                              copy .env.example → .env
                                              edit COMFYUI_URL etc.
                                                       │
                                                       ▼
                                          python scripts/<tool>.py ...
                                                       │
                            (later, when upstream updates) ▼
                                                ./sync.sh
                                              (preview → confirm → pull → refresh)
```

### Local vs remote ComfyUI

Every tool that uses ComfyUI supports two execution modes, documented per-repo:

- **Mode A — Local**: CLI runs on the same machine as ComfyUI. Just `python scripts/<tool>.py ...`.
- **Mode B — Remote**: ComfyUI on a GPU box (DGX Spark, headless server). Either invoke the CLI over SSH (`ssh user@gpu-host 'cd repo && python ...'`) or hit the remote ComfyUI HTTP API directly via SSH tunnel or `--listen 0.0.0.0`.

`aeon-movie-maker` has additional constraints documented (I2V + screenplay carry-forward needs filesystem-level access — pure HTTP-only remote works for T2V single clips only).

---

## 🎤 Voice and Video AI Stack

> Real-time speech and vision AI for DGX Spark. Three composable sidecars turn any Spark into a voice agent host: pair two OpenAI-compatible audio endpoints (TTS + ASR) with the Matrix WebRTC bridge to dial your AI directly from any Matrix client — or **video-call it** and let a vision LLM see through your camera — then compose all three into fully-embodied AI **personas** with [create-agentic-personas](https://github.com/AEON-7/create-agentic-personas). **End-to-end voice turn: ~2.1 s on Spark.**

| Repo | What it does | ★ |
|---|---|---|
| **[qwen3-tts-server](https://github.com/AEON-7/qwen3-tts-server)** | OpenAI-compatible `/v1/audio/speech` server backed by Qwen3-TTS-12Hz-1.7B-VoiceDesign. CUDA + bf16 + flash-attn 2 (sm_120 wheel). **RTF 1.30× hot path** (1.48 s synthesis for ~2 s of speech). Pre-built ghcr image, deploy scripts covering 5 model variants (VoiceDesign / CustomVoice / Base @ 1.7B & 0.6B). | ![](https://img.shields.io/github/stars/AEON-7/qwen3-tts-server?style=flat&label=) |
| **[qwen3-asr-server](https://github.com/AEON-7/qwen3-asr-server)** | OpenAI-compatible `/v1/audio/transcriptions` server — Qwen3-ASR-0.6B served by vLLM. 30 spoken languages + 22 zh dialects. **RTF 16× hot path** (120 ms transcription for 2 s of audio). Pre-built ghcr image, deploy scripts for 0.6B / 1.7B variants. | ![](https://img.shields.io/github/stars/AEON-7/qwen3-asr-server?style=flat&label=) |
| **[matrix-voip-agent](https://github.com/AEON-7/matrix-voip-agent)** | Headless Matrix WebRTC voice **and video** agent — auto-answers VoIP calls and bridges audio to any AI agent via PipeWire. Optional video add-on: samples the caller's VP8 camera frames into an in-memory ring (never disk) and gives any vision-capable LLM a per-call `look` tool — video-call your AI and ask "what do you see?" (`VIDEO_ENABLED=true` opt-in). The recommended bridge for AI-on-Matrix-VoIP: combine with any Matrix homeserver (Synapse / Conduit) and the two sidecars above to dial your AI directly from any Matrix client. | ![](https://img.shields.io/github/stars/AEON-7/matrix-voip-agent?style=flat&label=) |
| **[create-agentic-personas](https://github.com/AEON-7/create-agentic-personas)** | Build fully-embodied AI **personas** on OpenClaw + Matrix — each with a chat identity, a knowledge corpus (RAG), a cloned-or-designed Qwen3-TTS voice, and a live WebRTC call line. Composes the three sidecars above into a one-command-per-persona roster builder: secret-free templates, a `new-persona.sh` scaffold, and a `create-agentic-persona` agent skill so an agent can spin up new personas itself. | ![](https://img.shields.io/github/stars/AEON-7/create-agentic-personas?style=flat&label=) |

### Recommended pairing — full voice-AI stack on a single Spark

The three voice sidecars + the [Qwen3.6-27B AEON Ultimate MTP-XS vLLM main](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash) on one Docker bridge = a complete sub-3-second voice agent. Latency budget (measured, hot path on DGX Spark):

| stage | wall |
|---|---|
| inbound RTP packet → matrix-voip-agent | ~5 ms |
| ASR (1.92 s clip → text) | 120 ms |
| LLM (Qwen3.6-27B chat completion, ~10 toks) | ~480 ms |
| TTS (text → 1.92 s WAV) | ~1.48 s |
| outbound RTP → Matrix client | ~5 ms |
| **End-to-end voice turn** | **~2.1 s** |

Each repo ships an autonomous bring-up runbook (`AGENTS.md` / `agents.md`) alongside its `README.md`; the TTS/ASR sidecars additionally ship `docs/MODELS.md` (variant catalog), `docs/ARCHITECTURE.md` (full topology), and `docs/INTEGRATIONS.md` (Matrix + OpenAI SDK + OpenWebUI + Home Assistant + raw HTTP), and matrix-voip-agent ships `docs/FULLY-OFFLINE-VOICE.md` (single-Spark voice stack walkthrough).

---

## 💎 Gemma 4 Models

> Abliterated Gemma 4 deployments at NVFP4 precision (4-bit weights) for NVIDIA DGX Spark / Blackwell GPUs — quantized weights, EAGLE speculative-decoding drafters, and a validated DFlash serving container that more than triples single-stream throughput.

| Repo | Model | Architecture | Description | ★ |
|---|---|---|---|---|
| **[Gemma-4-31B-Uncensored-NVFP4-DFlash](https://github.com/AEON-7/Gemma-4-31B-Uncensored-NVFP4-DFlash)** | Gemma 4 31B Deckard Heretic | Serving container + DFlash | Validated vLLM container pairing the 31B DECKARD NVFP4 weights with the official [z-lab DFlash drafter](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash). **3.5× single-stream (11 → 39 tok/s) and up to 427 tok/s aggregate @ c=32** on DGX Spark — with reasoning, tool calling, vision/video input, and structured output fully intact. | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-31B-Uncensored-NVFP4-DFlash?style=flat&label=) |
| **[Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4)** | Gemma 4 31B DECKARD HERETIC | Dense, thinking | NVFP4-quantized abliterated 31B dense reasoning model. AWQ_FULL + SVDQuant variants. [🤗 weights](https://huggingface.co/AEON-7/Gemma-4-31B-it-DECKARD-HERETIC-Uncensored-NVFP4) | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4?style=flat&label=) |
| **[Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4)** | EAGLE drafter for 31B DECKARD | Speculative decoding | EAGLE E4B speculative-decoding drafter for the 31B DECKARD HERETIC. [🤗 weights](https://huggingface.co/AEON-7/Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4) | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-E4B-DECKARD-HERETIC-Uncensored-NVFP4?style=flat&label=) |
| **[Gemma-4-26B-A4B-it-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-26B-A4B-it-Uncensored-NVFP4)** | Gemma 4 26B A4B-it | MoE | NVFP4-quantized 26B MoE. **50 tok/s single, 1430 tok/s aggregate** on DGX Spark. [🤗 weights](https://huggingface.co/AEON-7/Gemma-4-26B-A4B-it-Uncensored-NVFP4) | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-26B-A4B-it-Uncensored-NVFP4?style=flat&label=) |
| **[Gemma-4-E4B-it-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-E4B-it-Uncensored-NVFP4)** | EAGLE drafter for 26B MoE | Speculative decoding | EAGLE E4B speculative-decoding drafter for the Gemma 4 26B MoE. NVFP4 AWQ. [🤗 weights](https://huggingface.co/AEON-7/Gemma-4-E4B-it-Uncensored-NVFP4) | ![](https://img.shields.io/github/stars/AEON-7/Gemma-4-E4B-it-Uncensored-NVFP4?style=flat&label=) |
| **[supergemma4-26b-abliterated-multimodal-nvfp4](https://github.com/AEON-7/supergemma4-26b-abliterated-multimodal-nvfp4)** | SuperGemma4 26B Multimodal | Multimodal · 🗄️ archived | NVFP4 AWQ full quantization of SuperGemma4-26B-Abliterated-Multimodal — pre-built vLLM container + patches included. Archived; kept public for reference and reproducibility. [🤗 weights](https://huggingface.co/AEON-7/supergemma4-26b-abliterated-multimodal-nvfp4) | ![](https://img.shields.io/github/stars/AEON-7/supergemma4-26b-abliterated-multimodal-nvfp4?style=flat&label=) |

---

## 🍎 Apple Silicon MLX

> The AEON catalog comes to the Mac. Metal-accelerated MLX builds of abliterated Gemma 4 — fully multimodal (text + image + audio), OpenAI-compatible, running host-native on any M-series machine. No CUDA required, no Docker GPU passthrough games.

| Repo | What it does | ★ |
|---|---|---|
| **[gemma4-aeon-abliterated-mlx-toolkit](https://github.com/AEON-7/gemma4-aeon-abliterated-mlx-toolkit)** | Apple-Silicon toolkit + OpenAI-compatible server for the Gemma-4-12B AEON Abliterated MLX quant grid: near-lossless **MLX-8bit (13.4 GB)** flagship and compact **MLXFP4 (9.3 GB)** for 16 GB Macs. One-paste `uv` quickstart boots a multimodal `mlx_vlm.server` on a fresh Mac — verified image description **and** speech transcription through the API. Optional MTP speculative decoding (~1.1–1.2× faster, output-identical). Benchmarked on M4 Pro 48 GB. | ![](https://img.shields.io/github/stars/AEON-7/gemma4-aeon-abliterated-mlx-toolkit?style=flat&label=) |

**Grab the weights:** [🤗 MLX-8bit](https://huggingface.co/AEON-7/Gemma-4-12B-it-AEON-Abliterated-MLX-8bit) · [🤗 MLXFP4](https://huggingface.co/AEON-7/Gemma-4-12B-it-AEON-Abliterated-MLXFP4) · [🤗 K4-BF16 source](https://huggingface.co/AEON-7/Gemma-4-12B-it-AEON-Abliterated-K4-BF16)

---

## 🐉 Qwen 3.6 Models

> The flagship line. Lossless abliteration of Qwen 3.6 with hardware NVFP4 quantization — dense 27B and 35B MoE — combined with DFlash speculative decoding for serious single-stream throughput on DGX Spark, plus an open research track pushing speculative decoding for hybrid-attention models forward.

| Repo | Model | Architecture | Description | ★ |
|---|---|---|---|---|
| **[Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash)** | Qwen 3.6 27B AEON Ultimate Uncensored | Dense | **The most-starred release in the catalog.** Lossless abliteration with NVFP4 hardware quantization — **BF16 (51 GB) + NVFP4 (26 GB)** deployment guide, docker-compose, and QuickStart. The production serving path for Qwen 3.6 on Spark. [🤗 weights](https://huggingface.co/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-Multimodal-NVFP4-MTP-XS) | ![](https://img.shields.io/github/stars/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash?style=flat&label=) |
| **[Qwen3.6-NVFP4-DFlash](https://github.com/AEON-7/Qwen3.6-NVFP4-DFlash)** | Qwen 3.6 35B-A3B-heretic | MoE | NVFP4 + DFlash speculative decoding on DGX Spark (GB10 / sm_121a). Source-built vLLM image + 7 patches + comprehensive deployment guide. [🤗 weights](https://huggingface.co/AEON-7/Qwen3.6-35B-A3B-heretic-NVFP4) | ![](https://img.shields.io/github/stars/AEON-7/Qwen3.6-NVFP4-DFlash?style=flat&label=) |
| **[Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree)** | Qwen 3.6 27B AEON Ultimate Uncensored | 🔬 Experimental research track | DDTree-on-vLLM for hybrid-attention Qwen 3.6 — tree verification, branch-state replay, Gated DeltaNet state handling, fused branch attention. Intentionally candid lab notes: what's been tried, what works, what still breaks, and where the next breakthrough likely lives. Use the DFlash repo above for production. | ![](https://img.shields.io/github/stars/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree?style=flat&label=) |

---

## 🌌 Nemotron Models

> NVIDIA Nemotron deployments for Blackwell-class hardware.

| Repo | Model | Architecture | Description | ★ |
|---|---|---|---|---|
| **[Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored](https://github.com/AEON-7/Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored)** | Nemotron 3 Nano Omni | 12-D abliterated multimodal | BF16 + NVFP4 multimodal reasoning model for DGX Spark / Blackwell. Source-built vLLM v0.20.0 image + 4 patches + benchmark + deployment guide. [🤗 weights](https://huggingface.co/AEON-7/Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored-BF16) | ![](https://img.shields.io/github/stars/AEON-7/Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored?style=flat&label=) |

---

## 🔧 Inference and Optimization Tools

> The engine room: the unified serving image that runs the whole catalog, plus the speculative-decoding, KV-cache-compression, and quantization building blocks underneath it.

| Repo | What it does | ★ |
|---|---|---|
| **[vllm-ultimate-dgx-spark](https://github.com/AEON-7/vllm-ultimate-dgx-spark)** | ⭐ **AEON vLLM Ultimate — the current flagship serving image** (`ghcr.io/aeon-7/aeon-vllm-ultimate`). vLLM 0.22.1 + Triton **NVFP4 KV cache** (PR #44389 cherry-pick — up to 3× KV capacity) + **TurboQuant K8V4** 4-bit KV compression + native DFlash / EAGLE3 via `--speculative-config` + 4 idempotent sm_121a runtime patches. One image serves the entire AEON model catalog on DGX Spark and RTX 50-series Blackwell. | ![](https://img.shields.io/github/stars/AEON-7/vllm-ultimate-dgx-spark?style=flat&label=) |
| **[vllm-dflash](https://github.com/AEON-7/vllm-dflash)** | The original DFlash vLLM image for DGX Spark — Plug & Play Block-Diffusion Speculative Decoding with NVFP4, sm_121a kernels, and Qwen-targeted optimizations. Start with AEON vLLM Ultimate (above) for new deployments. | ![](https://img.shields.io/github/stars/AEON-7/vllm-dflash?style=flat&label=) |
| **[turboquant](https://github.com/AEON-7/turboquant)** | Near-optimal KV-cache quantization for LLM inference (3-bit keys, 2-bit values) with Triton kernels + vLLM integration. This fork carries the CUDA-graph-safe QJL `_POWERS` fix that lets TurboQuant boot under CUDA graph capture — bundled into AEON vLLM Ultimate as `--kv-cache-dtype tq_k8v4`. | ![](https://img.shields.io/github/stars/AEON-7/turboquant?style=flat&label=) |
| **[Model-Optimizer](https://github.com/AEON-7/Model-Optimizer)** | Tracking fork of NVIDIA's unified model-optimization library — quantization, pruning, distillation, speculative decoding — for TensorRT-LLM / TensorRT / vLLM deployment. The quantization workhorse behind every NVFP4 release on this page. | ![](https://img.shields.io/github/stars/AEON-7/Model-Optimizer?style=flat&label=) |
| **[modelopt-fast-moe](https://github.com/AEON-7/modelopt-fast-moe)** | MoE-targeted quantization + AWQ calibration tooling. NVFP4 routing, expert-aware modelopt. | ![](https://img.shields.io/github/stars/AEON-7/modelopt-fast-moe?style=flat&label=) |

---

## 📦 Pre-built Docker Images

> Every public container on `ghcr.io/aeon-7` — built, validated, and mapped to the repo that documents it. All images: `docker pull ghcr.io/aeon-7/<image>`.

| Image | What it serves | Docs / source |
|---|---|---|
| [`aeon-vllm-ultimate`](https://github.com/users/AEON-7/packages/container/package/aeon-vllm-ultimate) | ⭐ **The unified flagship** — vLLM 0.22.1 + NVFP4 KV + TurboQuant + DFlash; serves the entire AEON catalog | [vllm-ultimate-dgx-spark](https://github.com/AEON-7/vllm-ultimate-dgx-spark) |
| [`vllm-aeon-ultimate-dflash`](https://github.com/users/AEON-7/packages/container/package/vllm-aeon-ultimate-dflash) | Qwen 3.6 27B AEON Ultimate — production DFlash serving | [Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash) |
| [`vllm-aeon-ultimate`](https://github.com/users/AEON-7/packages/container/package/vllm-aeon-ultimate) | Qwen 3.6 27B AEON Ultimate — base serving image | [Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DFlash) |
| [`vllm-aeon-ultimate-ddtree`](https://github.com/users/AEON-7/packages/container/package/vllm-aeon-ultimate-ddtree) | 🔬 DDTree experimental research image (vLLM build) | [Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree) |
| [`qwen3.6-27b-aeon-ultimate-uncensored-ddtree`](https://github.com/users/AEON-7/packages/container/package/qwen3.6-27b-aeon-ultimate-uncensored-ddtree) | 🔬 DDTree experimental research image (full container) | [Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree](https://github.com/AEON-7/Qwen3.6-27B-AEON-Ultimate-Uncensored-DDTree) |
| [`vllm-spark-omni-q36`](https://github.com/users/AEON-7/packages/container/package/vllm-spark-omni-q36) | Qwen 3.6 35B-A3B-heretic NVFP4 + DFlash (source-built vLLM + 7 patches) | [Qwen3.6-NVFP4-DFlash](https://github.com/AEON-7/Qwen3.6-NVFP4-DFlash) |
| [`gemma-4-31b-uncensored-nvfp4-dflash`](https://github.com/users/AEON-7/packages/container/package/gemma-4-31b-uncensored-nvfp4-dflash) | Gemma 4 31B Deckard Heretic + z-lab DFlash (3.5× single-stream) | [Gemma-4-31B-Uncensored-NVFP4-DFlash](https://github.com/AEON-7/Gemma-4-31B-Uncensored-NVFP4-DFlash) |
| [`vllm-spark-gemma4-nvfp4`](https://github.com/users/AEON-7/packages/container/package/vllm-spark-gemma4-nvfp4) | Gemma 4 31B DECKARD NVFP4 serving | [Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4) |
| [`vllm-spark-gemma4-nvfp4-awq`](https://github.com/users/AEON-7/packages/container/package/vllm-spark-gemma4-nvfp4-awq) | Gemma 4 31B DECKARD NVFP4 serving — AWQ_FULL variant | [Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-31B-DECKARD-HERETIC-Uncensored-NVFP4) |
| [`aeon-gemma-4-26b-a4b-dflash`](https://github.com/users/AEON-7/packages/container/package/aeon-gemma-4-26b-a4b-dflash) | Gemma 4 26B A4B MoE + DFlash | [Gemma-4-26B-A4B-it-Uncensored-NVFP4](https://github.com/AEON-7/Gemma-4-26B-A4B-it-Uncensored-NVFP4) |
| [`vllm-nemotron-omni-aeon-ultimate`](https://github.com/users/AEON-7/packages/container/package/vllm-nemotron-omni-aeon-ultimate) | Nemotron 3 Nano Omni — source-built vLLM v0.20.0 + 4 patches | [Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored](https://github.com/AEON-7/Nemotron-3-Nano-Omni-AEON-Ultimate-Uncensored) |
| [`vllm-dflash`](https://github.com/users/AEON-7/packages/container/package/vllm-dflash) | The original DFlash vLLM image | [vllm-dflash](https://github.com/AEON-7/vllm-dflash) |
| [`comfyui-aeon-spark`](https://github.com/users/AEON-7/packages/container/package/comfyui-aeon-spark) | Full media-production ComfyUI stack for DGX Spark | [comfyui-aeon-spark](https://github.com/AEON-7/comfyui-aeon-spark) |
| [`qwen3-tts-server`](https://github.com/users/AEON-7/packages/container/package/qwen3-tts-server) | OpenAI-compatible TTS sidecar (Qwen3-TTS) | [qwen3-tts-server](https://github.com/AEON-7/qwen3-tts-server) |
| [`qwen3-asr-server`](https://github.com/users/AEON-7/packages/container/package/qwen3-asr-server) | OpenAI-compatible ASR sidecar (Qwen3-ASR) | [qwen3-asr-server](https://github.com/AEON-7/qwen3-asr-server) |

---

## 🧪 Apps and Utilities

> Side projects, tools, and infrastructure that aren't model deployments but might be useful.

| Repo | What it does | ★ |
|---|---|---|
| **[unifi-ai-network-management](https://github.com/AEON-7/unifi-ai-network-management)** | Agent-ready UniFi / Ubiquiti network management skill and tooling: safe API key setup, backup/restore helpers, OpenClaw + Hermes install paths, and operational playbooks for diagnostics, security events, clients, APs, switches, VLANs, and Wi-Fi automation. | ![](https://img.shields.io/github/stars/AEON-7/unifi-ai-network-management?style=flat&label=) |
| **[cosmic-mind](https://github.com/AEON-7/cosmic-mind)** | Security-and-resiliency-focused deployment of the Quartz web app. A place to build your second mind and share it. | ![](https://img.shields.io/github/stars/AEON-7/cosmic-mind?style=flat&label=) |
| **[regex-builder](https://github.com/AEON-7/regex-builder)** | Simple and elegant RegEx builder. | ![](https://img.shields.io/github/stars/AEON-7/regex-builder?style=flat&label=) |
| **[quartz](https://github.com/AEON-7/quartz)** | Fast batteries-included static-site generator that transforms Markdown into fully functional websites. Fork — the upstream base for cosmic-mind. | ![](https://img.shields.io/github/stars/AEON-7/quartz?style=flat&label=) |

---

## 📊 Stats

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=AEON-7&show_icons=true&theme=dark&hide_border=true&include_all_commits=true&count_private=true)
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=AEON-7&layout=compact&theme=dark&hide_border=true&langs_count=8)

</div>

---

## ☕ Support the work

If any of these releases have been useful to you, tips are deeply appreciated — they go directly toward more compute, more models, and more open releases. **Scan a QR with your wallet, or click any address below to copy.**

<table align="center">
  <tr>
    <td align="center" width="50%">
      <strong>₿ Bitcoin (BTC)</strong><br/>
      <img src="assets/qr/btc.png" alt="BTC QR" width="200"/><br/>
      <sub><code>bc1q09xmzn00q4z3c5raene0f3pzn9d9pvawfm0py4</code></sub>
    </td>
    <td align="center" width="50%">
      <strong>Ξ Ethereum (ETH)</strong><br/>
      <img src="assets/qr/eth.png" alt="ETH QR" width="200"/><br/>
      <sub><code>0x1512667F6D61454ad531d2E45C0a5d1fd82D0500</code></sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <strong>◎ Solana (SOL)</strong><br/>
      <img src="assets/qr/sol.png" alt="SOL QR" width="200"/><br/>
      <sub><code>DgQsjHdAnT5PNLQTNpJdpLS3tYGpVcsHQCkpoiAKsw8t</code></sub>
    </td>
    <td align="center" width="50%">
      <strong>ⓜ Monero (XMR)</strong><br/>
      <img src="assets/qr/xmr.png" alt="XMR QR" width="200"/><br/>
      <sub><code>836XrSKw4R76vNi3QPJ5Fa9ugcyvE2cWmKSPv3AhpTNNKvqP8v5ba9JRL4Vh7UnFNjDz3E2GXZDVVenu3rkZaNdUFhjAvgd</code></sub>
    </td>
  </tr>
</table>

> **Ethereum L2s (Base, Arbitrum, Optimism, Polygon, etc.) and EVM-compatible tokens** can be sent to the same Ethereum address.

---

## 🤝 Get in touch

- 🌐 Open an issue on any repo for questions, bug reports, or feature requests
- 🤗 Model weights, quant grids, and drafters live on [Hugging Face → AEON-7](https://huggingface.co/AEON-7)
- 📜 Most releases include a deployment guide + benchmark numbers — start there

<div align="center">

_Built for the open source community on NVIDIA DGX Spark, RTX 5090, and Blackwell-class GPUs — and now Apple Silicon._

</div>
