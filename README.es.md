# Awesome Free AI para Creadores

**Todo lo que está aquí fue verificado contra el archivo de licencia del propio proyecto o los docs oficiales del proveedor. Ni un solo número de esta lista salió de mi memoria.**

La mayoría de las listas de "IA gratis" fallan siempre de las mismas tres formas: la licencia está mal reportada, el número de hardware corresponde a otro modelo, o el tier gratis nunca fue permanente. Esta lista está hecha para no fallar en ninguna.

**English** · [Fuentes y log de verificación](SOURCES.md) · [Cómo contribuir](CONTRIBUTING.md)

---

## Hazte estas tres preguntas antes que nada

Que una herramienta sea gratis no es lo mismo que sea *usable*. Antes de perder una hora o una fecha de entrega, verifica:

| Pregunta | Por qué mata proyectos |
|---|---|
| **¿Puedo usar el resultado comercialmente?** | Los modelos de imagen y video más populares son **no comerciales**. Este es el error más caro de la IA generativa abierta. |
| **¿Seguirá existiendo en seis meses?** | Los pesos abiertos no se revocan. Los tiers gratuitos alojados sí, con calendario. |
| **¿Qué cuesta realmente "gratis"?** | Algunos tiers gratuitos entrenan con tus prompts. Estás pagando con datos. |

**La licencia del código y la de los pesos son cosas distintas.** `F5-TTS` es código MIT con pesos CC-BY-NC. `InsightFace` es código MIT con modelos no comerciales. Este split es la norma, no la excepción — revisa las dos.

---

# 1. Herramientas creativas

Porque si no haces cosas, nada de esto importa.

## 🎬 Video (pesos abiertos)

| Modelo | Licencia | Comercial | Realidad |
|---|---|---|---|
| **[Wan2.2](https://github.com/Wan-Video/Wan2.2)** (Alibaba) | **Apache-2.0** | ✅ **Sí, limpia** | El default seguro. El repo dice: *"We claim no rights over your generated contents."* 17.1k estrellas. |
| **[Qwen-Image](https://github.com/QwenLM/Qwen-Image)** (Alibaba) | **Apache-2.0** | ✅ Sí | Modelo de imagen, pero bien licenciado — raro en esta familia. |
| **[HunyuanVideo-1.5](https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5)** (Tencent) | Tencent Hunyuan Community | ⚠️ **Con condiciones** | Limitado por territorio: **la licencia no aplica en la UE, Reino Unido ni Corea del Sur.** Hay que incluir un archivo Notice. Se recomienda (no se exige) etiquetar la salida "Powered by Tencent Hunyuan". Prohibido usar la marca. |
| **[FLUX.2-dev](https://github.com/black-forest-labs/flux2)** (Black Forest Labs) | FLUX Non-Commercial **v2.1** | ❌ **No** | *"non-commercial and non-production use."* El modelo de imagen abierto más popular **no se puede usar legalmente para trabajo de cliente.** |
| **[LTX-2](https://huggingface.co/Lightricks/LTX-2)** (Lightricks) | LTX-2 Open Weights License 0.X | ❌ **Las entidades deben comprar** | No es open source. Cualquier "Entity" necesita licencia comercial **pagada** aparte de Lightricks. |

### La trampa de Wan2.2: los modelos 14B no son para ti

El README oficial dice que `T2V-A14B`, `I2V-A14B`, `S2V-14B` y `Animate-14B` requieren **al menos 80GB de VRAM** para inferencia en una sola GPU.

El que sí corre en hardware de consumo es **`TI2V-5B`**:

- Backbone en disco: **3.43 GB** (Q4 GGUF) / 5.4 GB (Q8) / 10 GB (fp16)
- VRAM pico a 720p, 121 frames: **~8 GB**
- Documentado oficialmente en RTX 4090 de 24GB: clip de 5 segundos en 720p en **menos de 9 minutos**
- El propio tutorial de ComfyUI dice que cabe en **8GB** con offloading nativo

> **Nota Apple Silicon:** `TI2V-5B` corre en M2/M4 desde 16GB. Pero el checkpoint `I2V` 14B fp8-scaled **crashea en macOS tal cual** — los dtypes fp8 son incompatibles con Metal. Necesita parches de la comunidad, p. ej. [BRoliix/comfyui-wan22-apple-silicon](https://github.com/BRoliix/comfyui-wan22-apple-silicon) (probado en M3 Pro, 18GB).

> **Ojo además:** Wan 2.2 es el último Wan *totalmente abierto*. Las versiones 2.5–3.0 son productos de API. Si un tutorial te manda a "Wan 2.5", te está pidiendo que pagues.

**Interpolación de frames** — suaviza clips generados de forma barata: [RIFE](https://github.com/nihui/rife-ncnn-vulkan) (tiempo real, ~1.1k estrellas) o [FILM](https://github.com/google-research/frame-interpolation). Es la mejora de calidad más barata en generación de video: interpola en vez de renderizar más frames.

## 🖼️ Imagen

| Proyecto | Qué es |
|---|---|
| **[ComfyUI](https://github.com/comfyanonymous/ComfyUI)** | La UI de pipelines en nodos a la que todo se enchufa. Si aprendes una herramienta, que sea esta. |
| **[FLUX.2](https://github.com/black-forest-labs/flux2)** | El mejor modelo abierto en calidad — pero lee primero la licencia no comercial. |
| **[Qwen-Image](https://github.com/QwenLM/Qwen-Image)** | Apache-2.0, y bueno renderizando texto en imágenes. |
| **[Sana / Sana 1.5](https://github.com/NVlabs/Sana)** (NVIDIA) | Familia eficiente de alta resolución. |
| **[HunyuanImage-3.0](https://github.com/Tencent-Hunyuan/HunyuanImage-3.0)** | Licencia community de Tencent — mismos límites territoriales que el modelo de video. |
| **[Draw Things](https://docs.drawthings.ai/) / [DiffusionBee](https://github.com/divamgupta/diffusionbee-stable-diffusion-ui)** | Apps nativas de Mac. Sin Python, sin grafos de nodos. DiffusionBee es la abierta (13.6k estrellas). |

Otras UIs: [AUTOMATIC1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) (la instalación de referencia), [Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge) (fork más rápido), [InvokeAI](https://github.com/invoke-ai/InvokeAI), [SwarmUI](https://github.com/mcmonkeyprojects/SwarmUI).

> ⚠️ **Forge y Fooocus se quedan atrás.** Los dos siguen a Stable Diffusion upstream, que Stability ha ralentizado mucho. Revisa el último commit antes de construir un pipeline sobre cualquiera.

## 🎭 Face swap e identidad

Este es un pipeline de cuatro etapas. Conocerlas explica todo resultado raro.

| Etapa | Qué pasa | Herramienta estándar |
|---|---|---|
| 1. Detectar | Encuentra la cara, ubica landmarks | **InsightFace `buffalo_l`** (el estándar de facto) |
| 2. Codificar | Comprime la cara en un vector de identidad | **Embeddings ArcFace** |
| 3. Generar | Reconstruye la cara con la identidad fuente | **InSwapper** (GAN, rápido) o difusión (lento, mejor) |
| 4. Mezclar + restaurar | Igualar color, difuminar bordes, recuperar textura | **CodeFormer** / **GFPGAN** |

> **La etapa 4 es lo que hace que los swaps de 2026 se vean bien.** Saltarse el pase de restauración es la razón más común de que un swap parezca una pegatina.

| Proyecto | Licencia | Nota |
|---|---|---|
| **[FaceFusion](https://github.com/facefusion/facefusion)** | Código permisivo; hereda términos de los modelos | 29.5k estrellas, mantenido activamente. La mejor puerta de entrada. Corre 100% local. |
| **[InsightFace](https://github.com/deepinsight/insightface)** | Código **MIT**, modelos **no comerciales** | El backbone de detección/embedding bajo casi todas las herramientas. ⚠️ La restricción están en los modelos, no en el código. |
| **[DeepFaceLive](https://github.com/iperov/DeepFaceLive)** | Permisiva | Face swap en tiempo real desde webcam, para streaming. |
| **[DeepFaceLab](https://github.com/iperov/DeepFaceLab)** | Permisiva | La vía de máxima calidad. Horas de entrenamiento, mejor fidelidad. Curva empinada. |

> **ReActor eliminado.** El repo original de este popular nodo de face swap para Stable Diffusion ya no es accesible y las copias que sobreviven son forks de pocas estrellas sin procedencia verificable. Preferimos dejar un hueco antes que linkear algo que no podemos respaldar.

**Regla práctica:** GANs (InSwapper) para tiempo real y volumen; swappers de difusión para stills donde la calidad es crítica.

> ⚠️ **El problema de herencia de licencias:** FaceFusion y las herramientas antiguas basadas en Roop dependen de los modelos `inswapper` de InsightFace. Esos modelos son no comerciales. Una herramienta permisiva que incluye pesos no comerciales **no** es gratis comercialmente. Si te está pagando un cliente, verifica antes de entregar.

## 🎙️ Voz, habla y audio

| Proyecto | Licencia | Nota |
|---|---|---|
| **[F5-TTS](https://github.com/SWivid/F5-TTS)** | Código **MIT**, pesos **CC-BY-NC-4.0** | ⚠️ Pesos no comerciales. Clona una voz desde 5–15s de audio de referencia *más su transcripción*. ~1.5GB. Corre en CPU o con 4GB de VRAM. |
| **[X-Voice](https://github.com/sunnyxrxrx/X-Voice)** | Revisa el model card | Clonaje cross-lingual zero-shot en **30 idiomas** desde un solo hablante. Liberado en abril 2026. |
| **[Whisper](https://github.com/openai/whisper)** | MIT | Transcripción. El default para obtener la transcripción de referencia del F5-TTS. |
| **[RVC](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)** | Revisa | Voice conversion — cambia el timbre de una voz por el de otra. |

> ⚠️ **Un bug de licencia documentado que conviene conocer:** la conversión [cstr/f5-tts-GGUF](https://huggingface.co/cstr/f5-tts-GGUF) declaraba `mit` y después se corrigió a `cc-by-nc-4.0` para coincidir con upstream. Si encontraste un GGUF de TTS que dice MIT, probablemente está mal.

**Ajustes de calidad de F5-TTS:** `speed = 0.78` para voz de locución natural, `nfe_step = 32` para mejor calidad. Una palabra mal en la transcripción de referencia degrada la salida de forma notable.

## 🔧 Restauración de caras y upscaling

| Proyecto | Licencia | Nota |
|---|---|---|
| **[GFPGAN](https://github.com/TencentARC/GFPGAN)** | **Apache-2.0** | ✅ Licencia comercial limpia. Restauración ciega de caras. Usa los pesos de v1.4. |
| **[CodeFormer](https://github.com/sczhou/CodeFormer)** | **NTU S-Lab License 1.0** | ⚠️ No es Apache. Mayor fidelidad con `w` bajo, pero lee la licencia. |
| **[Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)** | BSD | Upscaling general. Se combina con ambos para el fondo. |

**Ajusta el peso de fidelidad `w` de CodeFormer** (0→1): más bajo = se ve mejor pero puede alterar la identidad; más alto = preserva la identidad pero queda más suave. La mayoría de los face swaps "raros" tienen el `w` muy alto.

---

# 2. Correr IA localmente (texto)

| Runtime | Licencia | Mejor para |
|---|---|---|
| **[Ollama](https://github.com/ollama/ollama)** | MIT | El default. El setup más fácil por lejos. |
| **[llama.cpp](https://github.com/ggml-org/llama.cpp)** | MIT | El motor que está debajo. El más rápido y portable. |
| **[LM Studio](https://lmstudio.ai/)** | Propietaria, gratis | GUI pulida, buena para quien no quiera terminal. |
| **[KoboldCpp](https://github.com/LostRuins/koboldcpp)** | AGPL | Muchos formatos de cuantización, muy flexible. |
| **[MLX](https://github.com/ml-explore/mlx)** | MIT | El framework de arrays de Apple. Solo Apple Silicon. |

### La cuenta de memoria que nadie explica

El tamaño de los pesos es fácil: **~2 bytes por parámetro en precisión completa**, **~0.5 bytes por parámetro en Q4_K_M**. Así que un modelo 9B en Q4_K_M ronda 4.5–5.5 GB.

Lo que sorprende es el **KV cache**, que crece linealmente con el contexto. Ejemplo real con **Qwen3.5-9B**, un modelo con arquitectura híbrida 3:1 — 3 capas Gated DeltaNet (atención lineal) por cada 1 de atención completa:

- Solo **8 de 32** capas mantienen un KV cache creciente. Las otras 24 mantienen un estado recurrente **fijo de 48 MB**.
- Por eso su contexto anunciado de **262K es realmente asequible** — inusual en un 9B.

| Contexto | KV cache (q8_0) | + modelo |
|---|---|---|
| 32K | 0.5 GB | 5.7 GB |
| 131K | 2.0 GB | 7.2 GB |
| **262K** | **4.0 GB** | **9.2 GB** |

Si un modelo promete contexto enorme y memoria barata, revisa si usa atención híbrida antes de descartarlo.

### Cuantización, en breve

| Formato | Bits/par | Cuándo usarlo |
|---|---|---|
| Q4_K_M | ~4.9 | El default sensato. Pequeño, pérdida casi imperceptible. |
| Q5_K_M | ~5.7 | Vale la pena si tienes holgura. |
| Q6_K | ~6.6 | Rendimientos decrecientes. |
| Q8_0 | ~8.5 | Referencia prácticamente sin pérdida. |
| FP16 | 16 | Solo si entrenas o sirves en producción. |

**Qwen3.5-9B** merece nota: Apache-2.0, 262K de contexto nativo, multimodal (con encoder de visión), y lo bastante chico para una laptop. MMLU-Pro 82.5, MMMU-Pro 70.1 según la propia tabla del vendor. Es la respuesta actual a "¿cuál es el mejor modelo que me cabe en mi máquina?".

---

# 3. Tiers gratuitos de API — con el debunk

## 🔴 El mito de Cerebras, revisado en la fuente

Claim que circula: *"Cerebras da 1,000,000 de tokens todos los días, para siempre, sin tarjeta."*

**La propia documentación de Cerebras** ([inference-docs.cerebras.ai/support/rate-limits](https://inference-docs.cerebras.ai/support/rate-limits)) dice, textual:

> **Is there a permanently free tier?**
> No. The Free Trial is time- and credit-bounded: **$5 in credits that expire 30 days after they're granted.**

No hay tier gratuito permanente. Los $5 expiran a los 30 días. Este es el ejemplo más claro que hay en internet de un claim de tier gratis repetido hasta volverse falso.

## Tiers verificados

| Proveedor | Tier gratis | ¿Tarjeta? | ¿Comercial? | Confianza |
|---|---|---|---|---|
| **[Google AI Studio](https://ai.google.dev/pricing)** | Solo Flash / Flash-Lite. **Los Pro pasaron a pago el 1 Abr 2026.** | No | ✅ Sí | Publicado por el proveedor. ⚠️ **Los RPM/RPD reales están en tu consola, no en los docs.** |
| **[Groq](https://console.groq.com/docs/rate-limits)** | Comúnmente ~30 RPM. Los topes diarios varían por modelo. | No | ✅ Sí | ⚠️ **Reportado por la comunidad.** Groq no publica topes diarios por modelo. |
| **[Cerebras](https://inference-docs.cerebras.ai/support/rate-limits)** | **$5, expira a los 30 días. No es permanente.** | No | Solo trial | **Publicado por el proveedor.** |
| **[OpenRouter](https://openrouter.ai/docs)** | 25+ modelos gratis sin créditos comprados | No | ✅ Sí | Publicado por el proveedor. |
| **[Mistral](https://docs.mistral.ai/)** | Experiment tier, con rate limit | No | ⚠️ Revisa | **Límites exactos no publicados.** |

### Las tres trampas del tier gratis

**1. El precio oculto de los datos.** Los propios términos de Google dicen que los prompts y completions del tier gratuito **pueden usarse para mejorar los productos de Google**. El uso de pago normalmente no. En un tier gratis estás comprando volumen con privacidad. Nunca metas material de cliente, notas de material no publicado, ni nada bajo NDA.

**2. La cuota es de la cuenta, no de la key.** Crear cinco API keys no crea cinco asignaciones. Los rate limits son por organización.

**3. Un pool enorme de tokens detrás de un RPM diminuto no es una asignación grande.** Un millón de tokens diarios no sirve si solo puedes hacer cinco requests por minuto. Revisa **ambos** números antes de diseñar en torno a un proveedor.

### Deja de adivinar tu cuota restante

La mayoría de las APIs devuelven los números reales en los headers de respuesta — requests restantes, tokens restantes y tiempo de reset. Lelos en vez de adivinar o hardcodear. Después implementa backoff y routing: cuando un proveedor devuelva 429, cambia al siguiente. Todo plan gratis termina saturándose, normalmente en el peor momento posible.

**No construyas un producto sobre un solo proveedor gratis.** Reparte la carga, ten un modelo local como respaldo, y nunca prometas capacidad que no controlas.

---

# 4. Stacks

**Stack creativo $0** — ComfyUI + Wan2.2 `TI2V-5B` (Apache-2.0, ~8GB) + FaceFusion + F5-TTS para trabajo en borrador, más un fallback pagado para entregables de cliente, para no quedarte atrapado en un 429.

**Stack de texto $0** — Ollama + Qwen3.5-9B (Apache-2.0, 262K) para todo lo privado. Tier gratis de Google AI Studio para el resto. Lee los headers de respuesta.

**El piso real** — los tiers gratuitos alojados son regalos que se pueden cancelar. Un modelo en tu propio hardware no tiene rate limit, ni cláusula de entrenamiento, ni aviso de cierre, ni bloqueo geográfico. Pierdes calidad frontier y velocidad. Ganas el único nivel que nadie puede revocar.

---

## Cómo contribuir

¿Encontraste algo mal, o una licencia que cambió?

**[Abre un issue](CONTRIBUTING.md)** — las correcciones con un link a la fuente son la contribución más valiosa acá. Una licencia que cambió en silencio es exactamente el modo de falla que esta lista existe para evitar.

## Licencia

Contenido [CC BY 4.0](LICENSE). Las marcas y los pesos de los modelos siguen siendo de sus dueños respectivos — esta lista los enlaza, no los redistribuye.
