# Sources & verification log

Every claim in this list was checked against a primary source. This file records which, and how confident we are. If a fact here is wrong, [open an issue](CONTRIBUTING.md) with a link.

**Last verification pass: 28 September 2026.**

The rule we follow: a license claim is only stated if we read the license file or the model card. A rate limit is only stated as "published" if the provider publishes it. Everything else is labelled as community-reported.

### Pass 2 — the usability filter

A second pass was run after the first list shipped, applying four hard criteria: **runnable on a consumer GPU**, **commercially usable**, **not region-blocked**, **license confirmed on the weights**. Eight entries failed and were removed:

| Removed | Verified reason | Source read |
|---|---|---|
| `CodeFormer` | **S-Lab License 1.0 grants use "for non-commercial purpose"** | [`LICENSE`](https://github.com/sczhou/CodeFormer/blob/master/LICENSE) — *"Redistribution and use for non-commercial purpose in source and binary forms"* |
| `CogVideoX` | Repo LICENSE says Apache-2.0, but **HF weights say `other`** | [HF API `THUDM/CogVideoX-5b`](https://huggingface.co/api/models/THUDM/CogVideoX-5b) → `license: other`. **Weights beat the repo.** |
| `FLUX.2-dev` | Non-commercial | [`LICENSE.md`](https://huggingface.co/black-forest-labs/FLUX.2-dev/blob/main/LICENSE.md) |
| `LTX-2` | Entities must buy | [`LICENSE`](https://huggingface.co/Lightricks/LTX-2/blob/main/LICENSE) |
| `HunyuanVideo-1.5`, `HunyuanImage-3.0` | Void in EU, UK, South Korea | [`LICENSE`](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5/blob/main/LICENSE) |
| `InsightFace` / `inswapper` | Models non-commercial | [insightface.ai](https://www.insightface.ai/) |
| `F5-TTS` | Weights CC-BY-NC-4.0 | [`cstr/f5-tts-GGUF` README](https://huggingface.co/cstr/f5-tts-GGUF/blob/main/README.md) |
| `Cerebras` | No permanent free tier; $5 expires in 30 days | [inference-docs.cerebras.ai/support/rate-limits](https://inference-docs.cerebras.ai/support/rate-limits) |

**Replacements added in the same pass**, each verified:

| Replacement | Claim | Source read | Verdict |
|---|---|---|---|
| **Chatterbox** (replaces F5-TTS) | **MIT** | [`LICENSE`](https://github.com/resemble-ai/chatterbox/blob/master/LICENSE) | ✅ **Confirmed MIT.** 350M `Chatterbox-Turbo` for low VRAM, 500M `Chatterbox-Multilingual V3` across 23+ languages, ships `example_for_mac.py`. |
| **FLUX.1-schnell** (replaces FLUX.2-dev) | **Apache-2.0**, ⚠️ gated | [HF API](https://huggingface.co/api/models/black-forest-labs/FLUX.1-schnell) | ✅ `license: apache-2.0`. ⚠️ `gated: auto` — free HF account + accept terms. ⚠️ The **GitHub repo 404s**; link points to the model page. |
| **Qwen-Image** | **Apache-2.0**, **not gated** | [HF API](https://huggingface.co/api/models/Qwen/Qwen-Image) | ✅ `license: apache-2.0`, `gated: false`. No click-through at all. |
| **Qwen3-Omni** | **Apache-2.0** | [`LICENSE`](https://github.com/QwenLM/Qwen3-Omni/blob/main/LICENSE) | ✅ **Confirmed.** 119 text languages, 19 speech input, 10 speech output, real-time streaming speech. |
| **Sana** | **Apache-2.0** | [`LICENSE`](https://github.com/NVlabs/Sana/blob/main/LICENSE) | ✅ **Confirmed.** |
| **SD 3.5 Medium** | Stability Community, revenue-limited | [HF API](https://huggingface.co/api/models/stabilityai/stable-diffusion-3.5-medium) | ⚠️ `license: other`, `gated: auto`. Commercial below **$1M annual revenue**. |

**Demoted, not removed:** `Demucs` (MIT, but the author left Meta and states he is no longer actively working on it — it still ships releases, so it works; `demucs-rs` is the recommendation) and the face-swap category as a whole (good tools, but every one of them inherits InsightFace's non-commercial weights — now labelled as failing the commercial filter rather than quietly listed).

---

## Licenses — read from the source file

| Project | Claim | Source read | Verdict |
|---|---|---|---|
| **Wan2.2** | Apache-2.0, no rights claimed over output | [`LICENSE.txt`](https://github.com/Wan-Video/Wan2.2/blob/main/LICENSE.txt) | ✅ **Confirmed.** Repo README states *"We claim no rights over your the generated contents."* |
| **Real-ESRGAN** | BSD-3-Clause | [`LICENSE`](https://github.com/xinntao/Real-ESRGAN/blob/master/LICENSE) | ✅ **Confirmed.** "BSD 3-Clause License, Copyright (c) 2021, Xintao Wang." |
| **GFPGAN** | Apache-2.0 | [repo](https://github.com/TencentARC/GFPGAN) | ✅ **Confirmed.** README states Apache License 2.0. |
| **LatentSync** | Apache-2.0 | [`LICENSE`](https://github.com/bytedance/LatentSync/blob/main/LICENSE) | ✅ **Confirmed.** Standard Apache 2.0, no addendum. Cleanest license in the lip-sync category. |
| **MuseTalk** | MIT code, **weights free for any purpose** | [`LICENSE`](https://github.com/TMElyralab/MuseTalk/blob/main/LICENSE) + README Disclaimer | ✅ **Confirmed.** LICENSE is MIT (Tencent Music Entertainment Group). README states models are *"available for any purpose, even commercially"*, and that dependent models (whisper, ft-mse-vae, dwpose, S3FD) carry their own terms. ⚠️ Bundled **test data** is non-commercial research only. |
| **Demucs** | MIT | [`LICENSE`](https://github.com/adefossez/demucs/blob/main/LICENSE) | ✅ **License confirmed clean** (Meta Platforms). ⚠️ **Maintenance is not:** the author states he left Meta and is no longer actively working on it. PyPI shows 4.1.0 released 11 Jul 2026. |
| **demucs-rs** | Apache-2.0 | [repo](https://github.com/nikhilunni/demucs-rs) | ✅ **Confirmed.** Independent Rust reimplementation of HTDemucs v4, Metal/Vulkan/WebGPU backends, VST3+CLAP. Created Feb 2026. |
| **AudioCraft** | MIT | [`LICENSE`](https://github.com/facebookresearch/audiocraft/blob/main/LICENSE) | ✅ **Confirmed.** MIT, Meta Platforms. |

### Removed — retained here so the removal is auditable

| Project | Claim | Source read | Verdict |
|---|---|---|---|
| **HunyuanVideo-1.5** | Tencent Hunyuan Community, territory-limited | [`LICENSE`](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5/blob/main/LICENSE) | 🚫 **Confirmed, then removed.** Excludes EU, UK, South Korea. Requires a Notice file. Prohibits trademark use. |
| **HunyuanImage-3.0** | Same family | [`LICENSE`](https://github.com/Tencent-Hunyuan/HunyuanImage-3.0/blob/main/LICENSE) | 🚫 **Same terms. Removed.** |
| **FLUX.2-dev** | FLUX Non-Commercial **v2.1** | [`LICENSE.md`](https://huggingface.co/black-forest-labs/FLUX.2-dev/blob/main/LICENSE.md) | 🚫 **Confirmed non-commercial. Removed.** |
| **LTX-2** | LTX-2 Open Weights License 0.X | [`LICENSE`](https://huggingface.co/Lightricks/LTX-2/blob/main/LICENSE) | 🚫 **Confirmed restricted. Removed.** Dated 5 Jan 2026. 19B model. |
| **F5-TTS** | Code MIT, **weights CC-BY-NC-4.0** | [`cstr/f5-tts-GGUF` README](https://huggingface.co/cstr/f5-tts-GGUF/blob/main/README.md) | 🚫 **Confirmed. Removed, replaced by Chatterbox.** |
| **CodeFormer** | **S-Lab License 1.0 — non-commercial** | [`LICENSE`](https://github.com/sczhou/CodeFormer/blob/master/LICENSE) | 🚫 **Confirmed non-commercial. Removed.** The LICENSE reads *"Redistribution and use for non-commercial purpose in source and binary forms."* The repo's permissive appearance is misleading. |
| **InsightFace** | Code MIT, **models non-commercial** | [insightface.ai](https://www.insightface.ai/) | 🚫 **Confirmed split. Removed**, and the whole face-swap category relabelled as non-commercial. |
| **Cerebras** | No permanent free tier | [inference-docs.cerebras.ai/support/rate-limits](https://inference-docs.cerebras.ai/support/rate-limits) | 🚫 **"No. The Free Trial is time- and credit-bounded: $5 in credits that expire 30 days after they're granted."** Removed from the tier table; kept as a debunk. |

## Hardware requirements

| Claim | Source | Verdict |
|---|---|---|
| Wan2.2 14B variants need **≥80GB VRAM** single-GPU | [Wan-Video/Wan2.2 README](https://github.com/Wan-Video/Wan2.2) | ✅ **First-party.** |
| Wan2.2 `TI2V-5B`: 24GB (RTX 4090), 5s 720p clip in <9 min | [Wan-AI first-party docs](https://github.com/Wan-Video/Wan2.2) | ✅ **First-party.** |
| `TI2V-5B` fits ~8GB with ComfyUI native offloading | [ComfyUI Wan 2.2 tutorial](https://docs.comfy.org/) | ✅ **Provider-documented.** |
| `TI2V-5B` Q4 GGUF = 3.43GB on disk, ~8GB peak | [localmodel.run](https://localmodel.run/model/wan-2-2-ti2v-5b) | ⚠️ **Third-party.** Consistent with first-party weights. |
| Wan2.2 I2V 14B fp8 **crashes on macOS/Metal** | [BRoliix/comfyui-wan22-apple-silicon](https://github.com/BRoliix/comfyui-wan22-apple-silicon) | ⚠️ **Community.** Reported as reproducible out-of-the-box; fixed by patches. |
| F5-TTS: ~1.5GB, runs on CPU or 4GB VRAM | [SWivid/F5-TTS](https://github.com/SWivid/F5-TTS) + community benchmarks | ⚠️ **Mixed.** Weights size is first-party; the RTF figures are community. |
| Qwen3.5-9B: 262K context, hybrid 3:1, 8 of 32 layers cache KV | [`config.json`](https://huggingface.co/Qwen/Qwen3.5-9B/blob/main/config.json) | ✅ **First-party.** `full_attention_interval: 4`, `num_hidden_layers: 32`, `num_key_value_heads: 4`, `head_dim: 256`. KV figures are our own arithmetic from those values. |

## Free API tiers

### The debunk

**Cerebras does not have a permanent free tier.** Their own rate-limits page, quoted verbatim:

> **Is there a permanently free tier?**
> No. The Free Trial is time- and credit-bounded: $5 in credits that expire 30 days after they're granted.

Source: [inference-docs.cerebras.ai/support/rate-limits](https://inference-docs.cerebras.ai/support/rate-limits) — **provider-published**.

The widespread claim of "1,000,000 free tokens per day, resets daily, no expiry" appears on many aggregator sites. We could not find it in any Cerebras primary source. **Treat it as unverified.**

### Published vs community-reported

| Provider | Status |
|---|---|
| **Google AI Studio** | Pro-series left the free tier on **1 Apr 2026** — provider-published. Free-tier data may be used to improve Google products — provider-published. Exact live RPM/RPD are **not published**; they appear only in your console. |
| **Cerebras** | **Provider-published** (see above). No permanent free tier. |
| **OpenRouter** | **Provider-published** free model limits. |
| **Groq** | ⚠️ **Community-reported only** (~30 RPM, varying daily caps). Groq does not publish per-model daily caps. Quotas are per-organization, not per-key. |
| **Mistral** | ⚠️ Exact limits **not published**. |

**We deliberately did not include rate-limit tables from aggregator sites.** They are frequently stale, mix units, and in the Cerebras case were simply wrong.

## Known gaps in this list

Being honest about what we have *not* verified:

- **Image generation license state is incomplete.** We confirmed FLUX.2, Qwen-Image and HunyuanImage. We have not audited every 2026 open image model. Check the model card before commercial use — this field changed fast.
- **Qwen3.5-9B benchmarks** are from the vendor's own table, not an independent leaderboard.
- **No audio restoration / denoise / source separation** (e.g. Demucs, UVR) has been audited yet.
- **Ab-literation and "uncensored" model builds** are deliberately excluded. Many are random personal uploads with no provenance, and a modified weight file can be fine-tuned on anything. If you want those, treat the weights as untrusted.
- **No regional availability matrix.** Some providers block sanctioned territories; VPN-faked locations can get accounts closed. Untested here.

## How to re-verify

```bash
# The licensing claims — the ones that matter most
curl -sL https://raw.githubusercontent.com/Wan-Video/Wan2.2/main/LICENSE.txt | head -5
curl -sL https://raw.githubusercontent.com/QwenLM/Qwen-Image/main/LICENSE   | head -5
curl -sL https://raw.githubusercontent.com/black-forest-labs/flux2/main/model_licenses/LICENSE-FLUX-NON-COMMERICAL | head -8

# The Cerebras debunk
curl -sL https://inference-docs.cerebras.ai/support/rate-limits | grep -i "permanently free"

# Qwen3.5-9B architecture, to recheck our KV arithmetic
curl -sL https://huggingface.co/Qwen/Qwen3.5-9B/raw/main/config.json \
  | grep -E "num_hidden_layers|num_key_value_heads|head_dim|full_attention_interval"
```

If any of these have changed, the list is wrong. Please tell us.
