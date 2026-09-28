# Awesome Free AI for Creators

**Everything here was verified against the project's own license file or the vendor's own docs. Not a single number in this list came from memory.**

Most "free AI" roundups are wrong in the same three ways: the license is misreported, the hardware number is for a different model, or the free tier was never permanent. This list is built to be wrong in none of them.

**Español** · [Sources & verification log](SOURCES.md) · [Contributing](CONTRIBUTING.md)

---

## Ask these three questions before anything else

A tool being free is not the same question as a tool being *usable*. Before you commit an hour or a client deadline, check:

| Question | Why it kills projects |
|---|---|
| **Can I use the output commercially?** | Most popular image and video models are **non-commercial**. This is the single most expensive mistake in open generative AI. |
| **Will it still exist in six months?** | Open weights don't get revoked. Hosted free tiers do, on a schedule. |
| **What does "free" actually cost me?** | Some free tiers train on your prompts. You are paying in data. |

The **code license and the weights license are frequently different.** `F5-TTS` is MIT code and CC-BY-NC weights. `InsightFace` is MIT code and non-commercial models. This split is the norm, not the exception — check both.

---

# 1. Creative tools

Because if you don't make things, none of this matters.

## 🎬 Video generation (open weights)

| Model | License | Commercial | Reality check |
|---|---|---|---|
| **[Wan2.2](https://github.com/Wan-Video/Wan2.2)** (Alibaba) | **Apache-2.0** | ✅ **Yes, clean** | The safe default. Repo states: *"We claim no rights over your generated contents."* 17.1k stars. |
| **[Qwen-Image](https://github.com/QwenLM/Qwen-Image)** (Alibaba) | **Apache-2.0** | ✅ Yes | Image model, but cleanly licensed — rare in this family. |
| **[HunyuanVideo-1.5](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5)** (Tencent) | Tencent Hunyuan Community | ⚠️ **With conditions** | Territory-limited: **the license does not apply in the EU, UK, or South Korea.** Must ship a Notice file. Encouraged (not required) to label output "Powered by Tencent Hunyuan". Trademark use is prohibited. |
| **[FLUX.2-dev](https://github.com/black-forest-labs/flux2)** (Black Forest Labs) | FLUX Non-Commercial **v2.1** | ❌ **No** | *"non-commercial and non-production use."* The most popular open image model **cannot legally be used for client work.** |
| **[LTX-2](https://huggingface.co/Lightricks/LTX-2)** (Lightricks) | LTX-2 Open Weights License 0.X | ❌ **Entities must buy** | Not open source. Any "Entity" needs a separate **paid** commercial license from Lightricks. |

### The Wan2.2 trap: the 14B models are not for you

The official README states that `T2V-A14B`, `I2V-A14B`, `S2V-14B` and `Animate-14B` require **at least 80GB VRAM** for single-GPU inference.

The one that actually runs on consumer hardware is **`TI2V-5B`**:

- Backbone on disk: **3.43 GB** (Q4 GGUF) / 5.4 GB (Q8) / 10 GB (fp16)
- Peak VRAM at 720p, 121 frames: **~8 GB**
- Officially documented on a 24GB RTX 4090: 5-second 720p clip in **under 9 minutes**
- ComfyUI's own tutorial claims it fits in **8GB** with native offloading

> **Apple Silicon note:** `TI2V-5B` runs on M2/M4 at 16GB and above. But the 14B `I2V` fp8-scaled checkpoint **crashes on macOS out of the box** — fp8 dtypes are incompatible with Metal. It needs community patches, e.g. [BRoliix/comfyui-wan22-apple-silicon](https://github.com/BRoliix/comfyui-wan22-apple-silicon) (tested on M3 Pro, 18GB).

> **Also worth knowing:** Wan 2.2 is the last *fully open* Wan flagship. Later 2.5–3.0 releases are API products. If a tutorial points at "Wan 2.5", you are being asked to pay.

**Frame interpolation** — smooth generated clips cheaply: [RIFE](https://github.com/nihui/rife-ncnn-vulkan) (real-time, ~1.1k stars) or [FILM](https://github.com/google-research/frame-interpolation). This is the cheapest quality win in video generation: interpolate instead of rendering more frames.

## 🖼️ Image generation

| Project | What it is |
|---|---|
| **[ComfyUI](https://github.com/comfyanonymous/ComfyUI)** | The node-based pipeline UI everything else plugs into. If you learn one tool, learn this. |
| **[FLUX.2](https://github.com/black-forest-labs/flux2)** | Best quality open model — but read the non-commercial license above first. |
| **[Qwen-Image](https://github.com/QwenLM/Qwen-Image)** | Apache-2.0, and good at text rendering in images. |
| **[Sana / Sana 1.5](https://github.com/NVlabs/Sana)** (NVIDIA) | Efficient high-resolution family. |
| **[HunyuanImage-3.0](https://github.com/Tencent-Hunyuan/HunyuanImage-3.0)** | Tencent community license — same territory limits as the video model. |
| **[Draw Things](https://docs.drawthings.ai/) / [DiffusionBee](https://github.com/divamgupta/diffusionbee-stable-diffusion-ui)** | Native Mac apps. No Python, no node graphs. DiffusionBee is the open one (13.6k stars). |

Other UIs: [AUTOMATIC1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) (the reference install), [Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge) (faster fork), [InvokeAI](https://github.com/invoke-ai/InvokeAI), [SwarmUI](https://github.com/mcmonkeyprojects/SwarmUI).

> ⚠️ **Forge and Fooocus drift out of date.** Both track upstream Stable Diffusion, which Stability has slowed considerably. Check the last commit before building a pipeline on either.

## 🎭 Face swap and identity

This is a four-stage pipeline. Knowing the stages explains every weird result.

| Stage | What happens | Standard tool |
|---|---|---|
| 1. Detect | Find the face, locate landmarks | **InsightFace `buffalo_l`** (de facto standard) |
| 2. Encode | Compress the face into an identity vector | **ArcFace** embeddings |
| 3. Generate | Rebuild the face with source identity | **InSwapper** (GAN, fast) or diffusion (slower, better) |
| 4. Blend + restore | Colour match, feather, recover skin texture | **CodeFormer** / **GFPGAN** |

> **Stage 4 is what makes 2026 swaps look good.** Skipping the restoration pass is the most common reason a swap looks like a sticker.

| Project | License | Note |
|---|---|---|
| **[FaceFusion](https://github.com/facefusion/facefusion)** | Code permissive; inherits model terms | 29.5k stars, actively maintained. Best entry point. Runs fully local. |
| **[InsightFace](https://github.com/deepinsight/insightface)** | Code **MIT**, models **non-commercial** | The detection/embedding backbone under most tools. ⚠️ The models are the restriction, not the code. |
| **[DeepFaceLive](https://github.com/iperov/DeepFaceLive)** | Permissive | Real-time webcam face swap for streaming. |
| **[DeepFaceLab](https://github.com/iperov/DeepFaceLab)** | Permissive | The high-quality path. Hours of training, best fidelity. Steep curve. |

> **ReActor removed.** The original repository for this popular Stable Diffusion face-swap node is no longer reachable and the surviving copies are low-star forks with no verifiable provenance. We would rather leave a gap than link something we cannot vouch for.

**Practical rule:** GANs (InSwapper) for real-time and volume; diffusion swappers for quality-critical stills.

> ⚠️ **The licensing inheritance problem:** FaceFusion and older Roop-based tools all rely on InsightFace's `inswapper` models. Those models are non-commercial. A permissive tool that ships non-commercial weights is **not** commercially free. If a client is paying, verify before you ship.

## 🎙️ Voice, speech and audio

| Project | License | Note |
|---|---|---|
| **[F5-TTS](https://github.com/SWivid/F5-TTS)** | Code **MIT**, weights **CC-BY-NC-4.0** | ⚠️ Non-commercial weights. Clones a voice from 5–15s of reference audio *plus its transcript*. ~1.5GB. Runs on CPU or 4GB VRAM. |
| **[X-Voice](https://github.com/sunnyxrxrx/X-Voice)** | Check model card | Zero-shot cross-lingual cloning across **30 languages** from one speaker. Released 2026-04. |
| **[Whisper](https://github.com/openai/whisper)** | MIT | Transcription. The default for getting a reference transcript for F5-TTS. |
| **[RVC](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)** | Check | Voice conversion — change one voice into another's timbre. |

> ⚠️ **A documented license bug worth knowing about:** the [cstr/f5-tts-GGUF](https://huggingface.co/cstr/f5-tts-GGUF) conversion initially declared `mit`, then corrected it to `cc-by-nc-4.0` to match upstream. If you found a TTS GGUF claiming MIT, it is probably wrong.

**F5-TTS quality settings** (from community testing): `speed = 0.78` for a natural broadcast voice, `nfe_step = 32` for best quality. One wrong word in the reference transcript degrades output noticeably.

## 🔧 Face restoration and upscaling

| Project | License | Note |
|---|---|---|
| **[GFPGAN](https://github.com/TencentARC/GFPGAN)** | **Apache-2.0** | ✅ Clean commercial license. Blind face restoration. Use v1.4 weights. |
| **[CodeFormer](https://github.com/sczhou/CodeFormer)** | **NTU S-Lab License 1.0** | ⚠️ Not Apache. Higher fidelity at low `w`, but read the license. |
| **[Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)** | BSD | General upscaling. Pairs with both above for the background. |

**Tune CodeFormer's fidelity weight `w`** (0→1): lower = better looking but may alter identity; higher = preserves identity more faithfully but softer. Most face swaps look "off" because `w` was left too high.

---

# 2. Run AI locally (text)

| Runtime | License | Best for |
|---|---|---|
| **[Ollama](https://github.com/ollama/ollama)** | MIT | The default. Easiest setup by a wide margin. |
| **[llama.cpp](https://github.com/ggml-org/llama.cpp)** | MIT | The engine underneath. Fastest, most portable. |
| **[LM Studio](https://lmstudio.ai/)** | Proprietary, free | Polished GUI, good for people who don't want a terminal. |
| **[KoboldCpp](https://github.com/LostRuins/koboldcpp)** | AGPL | Many quantization formats, very flexible. |
| **[MLX](https://github.com/ml-explore/mlx)** | MIT | Apple's own array framework. Apple Silicon only. |

### The memory math nobody explains

Approximate weight size is straightforward: **~2 bytes per parameter at full precision**, **~0.5 bytes per parameter at Q4_K_M**. So a 9B model at Q4_K_M is roughly 4.5–5.5 GB.

The part that surprises people is the **KV cache**, which grows linearly with context. Worked example for **Qwen3.5-9B**, a model with a hybrid 3:1 architecture — 3 Gated DeltaNet (linear attention) layers per 1 gated full-attention layer:

- Only **8 of 32** layers keep a growing KV cache. The other 24 keep a **fixed 48 MB** recurrent state.
- So its advertised **262K context is genuinely affordable** — unusual for a 9B.

| Context | KV cache (q8_0) | + model |
|---|---|---|
| 32K | 0.5 GB | 5.7 GB |
| 131K | 2.0 GB | 7.2 GB |
| **262K** | **4.0 GB** | **9.2 GB** |

If a model claims huge context and cheap memory, check whether it uses hybrid attention before dismissing it.

### Quantization, briefly

| Format | Bits/param | Use when |
|---|---|---|
| Q4_K_M | ~4.9 | The sensible default. Small, barely noticeable quality loss. |
| Q5_K_M | ~5.7 | Worth it if you have headroom. |
| Q6_K | ~6.6 | Diminishing returns. |
| Q8_0 | ~8.5 | Effectively lossless reference. |
| FP16 | 16 | Only if you're training or serving. |

**Qwen3.5-9B** deserves a note: Apache-2.0, 262K native context, multimodal (vision encoder), and small enough for a laptop. MMLU-Pro 82.5, MMMU-Pro 70.1 per the vendor's own table. It is the current answer to "what is the best model that fits on my machine".

---

# 3. Free API tiers — with the debunk

## 🔴 The Cerebras myth, checked at the source

Circulating claim: *"Cerebras gives 1,000,000 tokens every day, forever, no credit card."*

**Cerebras's own documentation** ([inference-docs.cerebras.ai/support/rate-limits](https://inference-docs.cerebras.ai/support/rate-limits)) states, verbatim:

> **Is there a permanently free tier?**
> No. The Free Trial is time- and credit-bounded: **$5 in credits that expire 30 days after they're granted.**

There is no permanent free tier. The $5 expires in 30 days. This is the clearest example on the internet of a free-tier claim being repeated until it becomes false.

## Verified tiers

| Provider | Free tier | Card? | Commercial? | Confidence |
|---|---|---|---|---|
| **[Google AI Studio](https://ai.google.dev/pricing)** | Flash / Flash-Lite only. **Pro models went paid on 1 Apr 2026.** | No | ✅ Yes | Provider-published. ⚠️ **Live RPM/RPD are shown in your console, not in docs.** |
| **[Groq](https://console.groq.com/docs/rate-limits)** | Commonly ~30 RPM. Daily caps vary by model. | No | ✅ Yes | ⚠️ **Community-reported.** Groq does not publish per-model daily caps. |
| **[Cerebras](https://inference-docs.cerebras.ai/support/rate-limits)** | **$5, expires in 30 days. Not permanent.** | No | Trial only | **Provider-published.** |
| **[OpenRouter](https://openrouter.ai/docs)** | 25+ free models, no credits purchased | No | ✅ Yes | Provider-published. |
| **[Mistral](https://docs.mistral.ai/)** | Experiment tier, rate-limited | No | ⚠️ Check | **Exact limits not published.** |

### The three free-tier traps

**1. The hidden data price.** Google's own terms state that free-tier prompts and completions **may be used to improve Google's products**. Paid usage typically is not. On a free tier you are buying volume with privacy. Never put client material, unreleased footage notes, or anything under NDA into it.

**2. Quota belongs to the account, not the key.** Creating five API keys does not create five allowances. Rate limits are per organization.

**3. A big token pool behind a tiny RPM is not a big allowance.** A million tokens per day is worthless if you can only issue five requests per minute. Check **both** numbers before designing around a provider.

### Stop guessing your remaining quota

Most APIs return the real numbers in response headers — remaining requests, remaining tokens, and reset time. Read them instead of guessing or hardcoding. Then implement backoff and routing: when one provider returns 429, fail over to the next. Every free plan eventually saturates, usually at the worst possible moment.

**Do not build a product on a single free provider.** Spread load, keep a local model as fallback, and never promise capacity you don't control.

---

# 4. Stacks

**$0 creative stack** — ComfyUI + Wan2.2 `TI2V-5B` (Apache-2.0, ~8GB) + FaceFusion + F5-TTS for scratch work, plus one paid fallback for client deliverables so you aren't stuck at a 429.

**$0 text stack** — Ollama + Qwen3.5-9B (Apache-2.0, 262K) for anything private. Google AI Studio free tier for everything else. Read the response headers.

**The real floor** — hosted free tiers are gifts that can be cancelled. A model on your own hardware has no rate limit, no training clause, no sunset notice, and no geo lock. You lose frontier quality and raw speed. You gain the only tier nobody can revoke.

---

## Contributing

Found something wrong, or a license that changed?

**[Open an issue](CONTRIBUTING.md)** — corrections with a source link are the most valuable contribution here. A license that silently changed is the failure mode this whole list exists to prevent.

## License

Content [CC BY 4.0](LICENSE). Trademarks and model weights remain the property of their respective owners — this list links to them, it does not redistribute them.
