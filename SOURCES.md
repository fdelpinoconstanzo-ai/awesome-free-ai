# Sources & verification log

Every claim in this list was checked against a primary source. This file records which, and how confident we are. If a fact here is wrong, [open an issue](CONTRIBUTING.md) with a link.

**Last verification pass: 28 September 2026.**

The rule we follow: a license claim is only stated if we read the license file or the model card. A rate limit is only stated as "published" if the provider publishes it. Everything else is labelled as community-reported.

---

## Licenses — read from the source file

| Project | Claim | Source read | Verdict |
|---|---|---|---|
| **Wan2.2** | Apache-2.0, no rights claimed over output | [`LICENSE.txt`](https://github.com/Wan-Video/Wan2.2/blob/main/LICENSE.txt) | ✅ **Confirmed.** Repo README states *"We claim no rights over your the generated contents."* |
| **Qwen-Image** | Apache-2.0 | [`LICENSE`](https://github.com/QwenLM/Qwen-Image/blob/main/LICENSE) | ✅ **Confirmed.** Standard Apache 2.0 text, no addendum. |
| **HunyuanVideo-1.5** | Tencent Hunyuan Community, territory-limited | [`LICENSE`](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5/blob/main/LICENSE) | ✅ **Confirmed.** Excludes EU, UK, South Korea. Requires a Notice file with redistribution. Encourages "Powered by Tencent Hunyuan" labelling. Prohibits trademark use. |
| **HunyuanImage-3.0** | Same family | [`LICENSE`](https://github.com/Tencent-Hunyuan/HunyuanImage-3.0/blob/main/LICENSE) | ✅ **Confirmed.** Same terms. |
| **FLUX.2-dev** | FLUX Non-Commercial License **v2.1** | [`LICENSE.md`](https://huggingface.co/black-forest-labs/FLUX.2-dev/blob/main/LICENSE.md) | ✅ **Confirmed non-commercial.** Grants use "for your non-commercial and non-production use". Revenue-generating activity is explicitly excluded. |
| **LTX-2** | LTX-2 Open Weights License 0.X | [`LICENSE`](https://huggingface.co/Lightricks/LTX-2/blob/main/LICENSE) | ✅ **Confirmed restricted.** Dated 5 Jan 2026. "Entities" must obtain a **paid** commercial license. Note this is a 19B model. |
| **F5-TTS** | Code MIT, **weights CC-BY-NC-4.0** | [`cstr/f5-tts-GGUF` README](https://huggingface.co/cstr/f5-tts-GGUF/blob/main/README.md) | ✅ **Confirmed.** The converter self-corrected from a wrong `mit` declaration to `cc-by-nc-4.0` to match upstream. |
| **GFPGAN** | Apache-2.0 | [repo](https://github.com/TencentARC/GFPGAN) | ✅ **Confirmed.** README states Apache License 2.0. |
| **CodeFormer** | NTU S-Lab License 1.0 | [repo](https://github.com/sczhou/CodeFormer) | ✅ **Confirmed.** Not Apache. Check before commercial use. |
| **InsightFace** | Code MIT, **models non-commercial** | [insightface.ai](https://www.insightface.ai/) | ✅ **Confirmed split.** Vendor states the open InSwapper-128 is the open-source standard and offers **separate commercial licensing**. Applies to every downstream tool. |

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
