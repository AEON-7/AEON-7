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

## 🎙️ Voice — real-time speech AI for DGX Spark

> Three composable sidecars that turn any DGX Spark into a real-time voice agent host. Pair two OpenAI-compatible audio endpoints (TTS + ASR) with the Matrix WebRTC bridge to dial your AI directly from any Matrix client. **End-to-end voice turn: ~2.1 s on Spark.**

| Repo | What it does | ★ |
|---|---|---|
| **[qwen3-tts-server](https://github.com/AEON-7/qwen3-tts-server)** | OpenAI-compatible `/v1/audio/speech` server backed by Qwen3-TTS-12Hz-1.7B-VoiceDesign. CUDA + bf16 + flash-attn 2 (sm_120 wheel). **RTF 1.30× hot path** (1.48 s synthesis for ~2 s of speech). Pre-built ghcr image, deploy scripts covering 5 model variants (VoiceDesign / CustomVoice / Base @ 1.7B & 0.6B). | ![](https://img.shields.io/github/stars/AEON-7/qwen3-tts-server?style=flat&label=) |
| **[qwen3-asr-server](https://github.com/AEON-7/qwen3-asr-server)** | OpenAI-compatible `/v1/audio/transcriptions` server — Qwen3-ASR-0.6B served by vLLM. 30 spoken languages + 22 zh dialects. **RTF 16× hot path** (120 ms transcription for 2 s of audio). Pre-built ghcr image, deploy scripts for 0.6B / 1.7B variants. | ![](https://img.shields.io/github/stars/AEON-7/qwen3-asr-server?style=flat&label=) |
| **[matrix-voip-agent](https://github.com/AEON-7/matrix-voip-agent)** | Headless Matrix WebRTC voice agent — auto-answers VoIP calls and bridges audio to any AI agent via PipeWire. The recommended bridge for AI-on-Matrix-VoIP: combine with any Matrix homeserver (Synapse / Conduit) and the two sidecars above to dial your AI directly from any Matrix client. | ![](https://img.shields.io/github/stars/AEON-7/matrix-voip-agent?style=flat&label=) |

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

Each repo ships with a `README.md`, `agents.md` (autonomous bring-up runbook), `docs/MODELS.md` (variant catalog), `docs/ARCHITECTURE.md` (full topology), and `docs/INTEGRATIONS.md` (Matrix + OpenAI SDK + OpenWebUI + Home Assistant + raw HTTP).

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
- 📜 Most releases include a deployment guide + benchmark numbers — start there

<div align="center">

_Built for the open source community on NVIDIA DGX Spark, RTX 5090, and Blackwell-class GPUs._

</div>
