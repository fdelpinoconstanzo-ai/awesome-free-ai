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

The **code license and the weights license are frequently different.** This split is the norm, not the exception — check both.

### The usability filter applied to this list

Being free is not the same as being usable. A tool is only on this list if it clears **all four** of these:

1. **You can actually run it** — on a consumer GPU or a laptop. Not a 80GB datacenter requirement.
2. **You can use the output commercially** — no NC clause, no "entities must buy".
3. **It is not region-blocked** — a license that excludes the EU, UK or South Korea is not a free tool.
4. **The license is confirmed on the weights**, not just the code.

**Removed because they failed the filter** — listed so you can recognise them when a tutorial recommends them:

| Removed | Why |
|---|---|
| `FLUX.2-dev` | Non-commercial license. Cannot ship client work. |
| `LTX-2` | Any "Entity" must buy a separate paid license. |
| `Wan2.2` 14B (`T2V/I2V/S2V/Animate`) | Requires **80GB VRAM**; the fp8 `I2V` checkpoint also crashes on Metal. |
| `HunyuanVideo-1.5`, `HunyuanImage-3.0` | Tencent license **does not apply in the EU, UK or South Korea.** |
| `InsightFace` / `inswapper` | Code MIT, but the **models are non-commercial** — and it is a backbone, not a tool. |
| `F5-TTS` | MIT code, **CC-BY-NC weights.** Superseded here by Chatterbox (MIT). |
| `Cerebras free tier` | There is no permanent free tier. A "$5 free credit" that expires in 30 days is not free. |
| `CogVideoX` | Repo LICENSE says Apache-2.0, but the **weights on Hugging Face say `other`.** When they disagree, the weights win. |

---

# 1. Creative tools

Because if you don't make things, none of this matters.

## 🎬 Video generation (open weights)

Only one model in this category passes the filter, and it is enough.

| Model | License | Commercial | Reality check |
|---|---|---|---|
| **[Wan2.2 `TI2V-5B`](https://github.com/Wan-Video/Wan2.2)** (Alibaba) | **Apache-2.0** | ✅ **Yes, clean** | The safe default, and the reason nothing else is listed. Repo states: *"We claim no rights over your generated contents."* 17.1k stars. |
| **[RIFE](https://github.com/nihui/rife-ncnn-vulkan)** | MIT | ✅ Yes | Frame interpolation. The cheapest quality win in video generation — interpolate to 2x instead of rendering more frames. |
| **[FILM](https://github.com/google-research/frame-interpolation)** | Apache-2.0 | ✅ Yes | Google's frame interpolation, for when RIFE smears fine detail. |

> ⚠️ **Everything else in open video is a trap.** The 14B Wan models need **80GB VRAM**; `LTX-2` requires entities to pay Lightricks; `HunyuanVideo-1.5` is void in the EU, UK and South Korea. `TI2V-5B` is the one that runs.

### Why `TI2V-5B` and not the 14B

The official README states `T2V-A14B`, `I2V-A14B`, `S2V-14B` and `Animate-14B` require **at least 80GB VRAM** for single-GPU inference. That is a rented A100, not a computer.

The one that runs on consumer hardware:

- Backbone on disk: **3.43 GB** (Q4 GGUF) / 5.4 GB (Q8) / 10 GB (fp16)
- Peak VRAM at 720p, 121 frames: **~8 GB**
- Officially documented on a 24GB RTX 4090: 5-second 720p clip in **under 9 minutes**
- ComfyUI's own tutorial claims it fits in **8GB** with native offloading

> **Apple Silicon note:** `TI2V-5B` runs on M2/M4 at 16GB and above. But the 14B `I2V` fp8-scaled checkpoint **crashes on macOS out of the box** — fp8 dtypes are incompatible with Metal. It needs community patches, e.g. [BRoliix/comfyui-wan22-apple-silicon](https://github.com/BRoliix/comfyui-wan22-apple-silicon) (tested on M3 Pro, 18GB).

> **Also worth knowing:** Wan 2.2 is the last *fully open* Wan flagship. Later 2.5–3.0 releases are API products. If a tutorial points at "Wan 2.5", you are being asked to pay.

## 🖼️ Image generation

| Project | License | Reality check |
|---|---|---|
| **[Qwen-Image](https://huggingface.co/Qwen/Qwen-Image)** (Alibaba) | **Apache-2.0**, **not gated** | ✅ **The best starting point.** No account approval, no click-through, and it is unusually good at rendering text inside images. |
| **[FLUX.1-schnell](https://huggingface.co/black-forest-labs/FLUX.1-schnell)** (Black Forest Labs) | **Apache-2.0** | ✅ The commercially clean FLUX. ⚠️ **Gated on Hugging Face** — you need a free HF account and to accept the terms once. That is mild friction, not a blocker. 4 steps to an image. |
| **[Sana](https://github.com/NVlabs/Sana)** (NVIDIA) | **Apache-2.0** | ✅ Efficient high-resolution family. |
| **[SD 3.5 Medium](https://huggingface.co/stabilityai/stable-diffusion-3.5-medium)** | Stability Community | ⚠️ Usable commercially below **$1M annual revenue**, gated. Fine for most people, not for an agency. |
| **[DiffusionBee](https://github.com/divamgupta/diffusionbee-stable-diffusion-ui)** | Open | ✅ Native Mac app. No Python, no node graphs. 13.6k stars. |
| **[Draw Things](https://docs.drawthings.ai/)** | Free, closed | Native Mac app with a genuinely good Metal backend. |

Other UIs, all MIT and all working: [ComfyUI](https://github.com/comfyanonymous/ComfyUI) (the node-based pipeline everything else plugs into — if you learn one tool, learn this), [AUTOMATIC1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) (the reference install), [Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge) (faster fork), [InvokeAI](https://github.com/invoke-ai/InvokeAI), [SwarmUI](https://github.com/mcmonkeyprojects/SwarmUI).

> ⚠️ **Forge and Fooocus drift out of date.** Both track upstream Stable Diffusion, which Stability has slowed considerably. Check the last commit before building a pipeline on either.

## 🎭 Face swap and identity

> 🚫 **This entire category fails the commercial filter, and we are not going to pretend otherwise.** Every open face-swap tool — FaceFusion, DeepFaceLab, ReActor, Roop — is built on **InsightFace `inswapper`**, whose models are **non-commercial**. The code being MIT changes nothing. The tools are genuinely good and they are fine for personal and research work; they are **not** free for client work.
>
> If a swap has to be commercially licensed, the vendor path is [InsightFace's own commercial licensing](https://www.insightface.ai/), not a workaround.

This is a four-stage pipeline. Knowing the stages explains every weird result.

| Stage | What happens | Standard tool |
|---|---|---|
| 1. Detect | Find the face, locate landmarks | **InsightFace `buffalo_l`** (de facto standard) |
| 2. Encode | Compress the face into an identity vector | **ArcFace** embeddings |
| 3. Generate | Rebuild the face with source identity | **InSwapper** (GAN, fast) or diffusion (slower, better) |
| 4. Blend + restore | Colour match, feather, recover skin texture | **GFPGAN** |

> **Stage 4 is what makes 2026 swaps look good.** Skipping the restoration pass is the most common reason a swap looks like a sticker.

| Project | License | Note |
|---|---|---|
| **[FaceFusion](https://github.com/facefusion/facefusion)** | Code permissive; **inherits non-commercial model terms** | 29.5k stars, actively maintained, best entry point. Runs fully local. 🚫 Non-commercial via `inswapper`. |
| **[DeepFaceLive](https://github.com/iperov/DeepFaceLive)** | Permissive code, non-commercial models | Real-time webcam face swap for streaming. Same restriction. |
| **[DeepFaceLab](https://github.com/iperov/DeepFaceLab)** | Permissive code, non-commercial models | The high-quality path. Hours of training, best fidelity. Steep curve. Same restriction. |

> **ReActor removed.** The original repository for this popular Stable Diffusion face-swap node is no longer reachable and the surviving copies are low-star forks with no verifiable provenance. We would rather leave a gap than link something we cannot vouch for.

**Practical rule:** GANs (InSwapper) for real-time and volume; diffusion swappers for quality-critical stills.

> ⚠️ **The licensing inheritance problem, stated once and clearly:** a permissive tool that ships non-commercial weights is **not** commercially free. This is the single most common way people accidentally break a client contract with "free" AI software.

## 🎙️ Voice, speech and audio

| Project | License | Note |
|---|---|---|
| **[Chatterbox](https://github.com/resemble-ai/chatterbox)** (Resemble AI) | **MIT** | ✅ **The voice model to use.** Zero-shot voice cloning from a short reference clip, with CFG and exaggeration controls. `Chatterbox-Turbo` is **350M** and explicitly built for low VRAM; `Chatterbox-Multilingual V3` is 500M and covers **23+ languages**. Ships an `example_for_mac.py`. |
| **[Qwen3-Omni](https://github.com/QwenLM/Qwen3-Omni)** (Alibaba) | **Apache-2.0** | ✅ End-to-end omni-modal: text, image, audio and video in; **real-time streaming speech out**. 119 text languages, 19 speech input, 10 speech output. |
| **[Whisper](https://github.com/openai/whisper)** | **MIT** | Transcription. Gives you the reference transcript that voice cloning needs. |
| **[RVC](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)** | Check the model card | Voice **conversion** — change one voice into another's timbre, rather than cloning from scratch. |

> ⚠️ **`F5-TTS` is gone from this list** for one reason: MIT code but **CC-BY-NC weights**. It was the most-recommended open TTS for two years and it cannot legally be used for paid work. `Chatterbox` is MIT end to end and is the replacement.

> ⚠️ **A documented license bug worth knowing about:** the [cstr/f5-tts-GGUF](https://huggingface.co/cstr/f5-tts-GGUF) conversion initially declared `mit`, then corrected it to `cc-by-nc-4.0` to match upstream. If you find a TTS GGUF claiming MIT, it is probably wrong. This is exactly why the weights license is checked and not the repo license.

**Chatterbox practical notes:** clone only from audio you own or have permission to use. Multilingual V3 improves accent and speaker-similarity preservation across languages, which matters more than raw audio quality if your source voice is accented.

## 🗣️ Lip sync and talking heads

Cheapest dialogue in AI video. Replace the mouth, keep the performance.

| Project | License | Verdict |
|---|---|---|
| **[LatentSync](https://github.com/bytedance/LatentSync)** (ByteDance) | **Apache-2.0** | ✅ **The one to use.** End-to-end latent diffusion, no intermediate motion representation. 6k stars. Inference, checkpoints **and training code** all open. Version 1.6 trains at 512×512 specifically to fix the blur older versions had. Strong identity preservation. |
| **[MuseTalk](https://github.com/TMElyralab/MuseTalk)** (Tencent Music) | **MIT code, weights free for any purpose** | ✅ Rare — the README states the trained models are *"available for any purpose, even commercially."* Real-time at **30fps+ on a Tesla V100**. 6.5k stars. Weights only modify a 256×256 face region. |
| **[SadTalker](https://github.com/OpenTalker/SadTalker)** | Check model card | Adds head motion, not just lips. 14.1k stars. ⚠️ Output resolution is capped by its 3DMM rendering stage — it cannot deliver 4K. |

> ⚠️ **MuseTalk's own caveat:** its bundled **test data** was collected from the internet and is *"available for non-commercial research purposes only."* That applies to the test data, **not** the model. Do not ship the test set in a commercial project.

**Tuning LatentSync:** `inference_steps` 20–50 (higher = better, slower), `guidance_scale` 1.0–3.0 (higher = tighter sync, can look artificial past 2.5).

> **The generation-order trap:** MuseV (or any image-to-video model) generates the face → **interpolate** the frame rate → *then* run lip sync. Lip-syncing before interpolation makes the mouth stutter.

## 🎵 Audio separation and restoration

| Project | License | Verdict |
|---|---|---|
| **[demucs-rs](https://github.com/nikhilunni/demucs-rs)** | **Apache-2.0** | ✅ **The one to use.** Rust reimplementation of HTDemucs v4 with **Metal acceleration on macOS**, plus a VST3/CLAP plugin so you can drop it into a DAW and pull stems live. Created 2026, actively built. |
| **[AudioCraft](https://github.com/facebookresearch/audiocraft)** (Meta) | **MIT** | ✅ Music and sound generation — MusicGen and friends. |
| **[Demucs](https://github.com/adefossez/demucs)** (Meta) | **MIT** | ⚠️ The original and still the reference implementation, but **the author left Meta** and states he is no longer actively working on it. It still ships releases (4.1.0, Jul 2026), so it works — it just may not get fixed. Use `demucs-rs`. |

**What separation is actually for in post:** pulling clean dialogue out of a noisy location recording, or clearing music out under a voiceover. For music production itself it is equally at home.

> ⚠️ **The maintainer trap, stated plainly:** the most-starred, most-linked music separation tool is **effectively unmaintained by its author**. Check the last release date before you build a pipeline on it — this field churns faster than image generation.

## 🔧 Face restoration and upscaling

| Project | License | Note |
|---|---|---|
| **[Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)** | **BSD-3** | ✅ General upscaling. Pairs with the face restorer for the background. |
| **[GFPGAN](https://github.com/TencentARC/GFPGAN)** (Tencent) | **Apache-2.0** | ✅ Clean commercial license. Blind face restoration. Use v1.4 weights. |

> ⚠️ **`CodeFormer` removed.** Its license is **S-Lab License 1.0**, which grants use *"for non-commercial purpose"* — despite the repo's permissive-looking appearance. It was the standard recommendation for years and it cannot legally be used for paid work. `GFPGAN` is the clean replacement.

**Tuning note:** if you use `GFPGAN` v1.4, the `upscale` setting is the main quality lever — start at 2 and only raise it if the output looks soft.

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

There is no permanent free tier. The $5 expires in 30 days. This is the clearest example on the internet of a free-tier claim being repeated until it becomes false. **That is why Cerebras is absent from the table below.**

## Verified tiers

| Provider | Free tier | Card? | Commercial? | Confidence |
|---|---|---|---|---|
| **[Google AI Studio](https://ai.google.dev/pricing)** | Flash / Flash-Lite only. **Pro models went paid on 1 Apr 2026.** | No | ✅ Yes | Provider-published. ⚠️ **Live RPM/RPD are shown in your console, not in docs.** |
| **[Groq](https://console.groq.com/docs/rate-limits)** | Commonly ~30 RPM. Daily caps vary by model. | No | ✅ Yes | ⚠️ **Community-reported.** Groq does not publish per-model daily caps. |
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

**$0 commercial creative stack** — ComfyUI + Wan2.2 `TI2V-5B` (Apache-2.0, ~8GB) + Qwen-Image (Apache-2.0) + MuseTalk (MIT) + Chatterbox (MIT) + GFPGAN (Apache-2.0), plus one paid fallback for client deliverables so you aren't stuck at a 429. Every component is commercially clean.

**$0 text stack** — Ollama + Qwen3.5-9B (Apache-2.0, 262K) for anything private. Google AI Studio free tier for everything else. Read the response headers.

**The real floor** — hosted free tiers are gifts that can be cancelled. A model on your own hardware has no rate limit, no training clause, no sunset notice, and no geo lock. You lose frontier quality and raw speed. You gain the only tier nobody can revoke.

---

## Contributing

Found something wrong, or a license that changed?

**[Open an issue](CONTRIBUTING.md)** — corrections with a source link are the most valuable contribution here. A license that silently changed is the failure mode this whole list exists to prevent.

## License

Content [CC BY 4.0](LICENSE). Trademarks and model weights remain the property of their respective owners — this list links to them, it does not redistribute them.
