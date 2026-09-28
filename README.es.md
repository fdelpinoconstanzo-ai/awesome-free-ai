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

**La licencia del código y la de los pesos son cosas distintas.** Este split es la norma, no la excepción — revisa las dos.

### El filtro de usabilidad aplicado a esta lista

Ser gratis no es lo mismo que ser usable. Una herramienta entra a esta lista solo si supera **las cuatro**:

1. **Puedes correrla de verdad** — en una GPU de consumo o en un notebook. No un requisito de datacenter de 80GB.
2. **Puedes usar el resultado comercialmente** — sin cláusula NC, sin "las entidades deben comprar".
3. **No está bloqueada por región** — una licencia que excluye la UE, Reino Unido o Corea del Sur no es una herramienta gratis.
4. **La licencia está confirmada en los pesos**, no solo en el código.

**Removidas porque no pasaron el filtro** — listadas para que las reconozcas cuando un tutorial te las recomiende:

| Removida | Por qué |
|---|---|
| `FLUX.2-dev` | Licencia no comercial. No se puede entregar trabajo de cliente. |
| `LTX-2` | Cualquier "Entity" debe comprar licencia aparte. |
| `Wan2.2` 14B (`T2V/I2V/S2V/Animate`) | Requiere **80GB de VRAM**; el checkpoint `I2V` fp8 además crashea en Metal. |
| `HunyuanVideo-1.5`, `HunyuanImage-3.0` | La licencia de Tencent **no aplica en la UE, Reino Unido ni Corea del Sur.** |
| `InsightFace` / `inswapper` | Código MIT, pero los **modelos son no comerciales** — y además es un backbone, no una herramienta. |
| `F5-TTS` | Código MIT, **pesos CC-BY-NC.** Reemplazada aquí por Chatterbox (MIT). |
| `Cerebras free tier` | No hay tier gratuito permanente. Un "$5 de crédito" que expira en 30 días no es gratis. |
| `CogVideoX` | El LICENSE del repo dice Apache-2.0, pero los **pesos en Hugging Face dicen `other`.** Cuando discrepan, ganan los pesos. |

---

# 1. Herramientas creativas

Porque si no haces cosas, nada de esto importa.

## 🎬 Video (pesos abiertos)

Solo un modelo pasa el filtro en esta categoría, y alcanza.

| Modelo | Licencia | Comercial | Realidad |
|---|---|---|---|
| **[Wan2.2 `TI2V-5B`](https://github.com/Wan-Video/Wan2.2)** (Alibaba) | **Apache-2.0** | ✅ **Sí, limpia** | El default seguro, y la razón de que no haya nada más en la lista. El repo dice: *"We claim no rights over your generated contents."* 17.1k estrellas. |
| **[RIFE](https://github.com/nihui/rife-ncnn-vulkan)** | MIT | ✅ Sí | Interpolación de frames. La mejora de calidad más barata en video: interpola a 2x en vez de renderizar más frames. |
| **[FILM](https://github.com/google-research/frame-interpolation)** | Apache-2.0 | ✅ Sí | La interpolación de Google, para cuando RIFE difumina el detalle fino. |

> ⚠️ **Todo lo demás en video abierto es una trampa.** Los 14B de Wan necesitan **80GB de VRAM**; `LTX-2` exige pagar a Lightricks; `HunyuanVideo-1.5` no vale en la UE, Reino Unido ni Corea del Sur. `TI2V-5B` es el que corre.

### Por qué `TI2V-5B` y no el 14B

El README oficial dice que `T2V-A14B`, `I2V-A14B`, `S2V-14B` y `Animate-14B` requieren **al menos 80GB de VRAM** para inferencia en una sola GPU. Eso es una A100 rentada, no un computador.

El que corre en hardware de consumo:

- Backbone en disco: **3.43 GB** (Q4 GGUF) / 5.4 GB (Q8) / 10 GB (fp16)
- VRAM pico a 720p, 121 frames: **~8 GB**
- Documentado oficialmente en RTX 4090 de 24GB: clip de 5 segundos en 720p en **menos de 9 minutos**
- El propio tutorial de ComfyUI dice que cabe en **8GB** con offloading nativo

> **Nota Apple Silicon:** `TI2V-5B` corre en M2/M4 desde 16GB. Pero el checkpoint `I2V` 14B fp8-scaled **crashea en macOS tal cual** — los dtypes fp8 son incompatibles con Metal. Necesita parches de la comunidad, p. ej. [BRoliix/comfyui-wan22-apple-silicon](https://github.com/BRoliix/comfyui-wan22-apple-silicon) (probado en M3 Pro, 18GB).

> **Ojo además:** Wan 2.2 es el último Wan *totalmente abierto*. Las versiones 2.5–3.0 son productos de API. Si un tutorial te manda a "Wan 2.5", te está pidiendo que pagues.

## 🖼️ Imagen

| Proyecto | Licencia | Realidad |
|---|---|---|
| **[Qwen-Image](https://huggingface.co/Qwen/Qwen-Image)** (Alibaba) | **Apache-2.0**, **sin gate** | ✅ **El mejor punto de partida.** Sin aprobación de cuenta, sin click-through, y es inusualmente bueno renderizando texto dentro de imágenes. |
| **[FLUX.1-schnell](https://huggingface.co/black-forest-labs/FLUX.1-schnell)** (Black Forest Labs) | **Apache-2.0** | ✅ El FLUX comercialmente limpio. ⚠️ **Gated en Hugging Face** — necesitas una cuenta HF gratis y aceptar los términos una vez. Es fricción leve, no un bloqueo. 4 pasos hasta una imagen. |
| **[Sana](https://github.com/NVlabs/Sana)** (NVIDIA) | **Apache-2.0** | ✅ Familia eficiente de alta resolución. |
| **[SD 3.5 Medium](https://huggingface.co/stabilityai/stable-diffusion-3.5-medium)** | Stability Community | ⚠️ Usable comercialmente bajo **$1M de ingresos anuales**, gated. Bien para casi todos, no para una agencia. |
| **[DiffusionBee](https://github.com/divamgupta/diffusionbee-stable-diffusion-ui)** | Abierta | ✅ App nativa de Mac. Sin Python, sin grafos de nodos. 13.6k estrellas. |
| **[Draw Things](https://docs.drawthings.ai/)** | Gratis, cerrada | App nativa de Mac con un backend Metal realmente bueno. |

Otras UIs, todas MIT y todas funcionando: [ComfyUI](https://github.com/comfyanonymous/ComfyUI) (la UI de pipelines en nodos a la que todo se enchufa — si aprendes una herramienta, que sea esta), [AUTOMATIC1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) (la instalación de referencia), [Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge) (fork más rápido), [InvokeAI](https://github.com/invoke-ai/InvokeAI), [SwarmUI](https://github.com/mcmonkeyprojects/SwarmUI).

> ⚠️ **Forge y Fooocus se quedan atrás.** Los dos siguen a Stable Diffusion upstream, que Stability ha ralentizado mucho. Revisa el último commit antes de construir un pipeline sobre cualquiera.

## 🎭 Face swap e identidad

> 🚫 **Toda esta categoría falla el filtro comercial, y no vamos a fingir lo contrario.** Cada herramienta abierta de face swap — FaceFusion, DeepFaceLab, ReActor, Roop — está construida sobre **InsightFace `inswapper`**, cuyos modelos son **no comerciales**. Que el código sea MIT no cambia nada. Las herramientas son buenas de verdad y sirven perfecto para uso personal y de investigación; **no** son gratis para trabajo de cliente.
>
> Si un swap debe tener licencia comercial, el camino es [la licencia comercial de InsightFace](https://www.insightface.ai/), no un rodeo.

Este es un pipeline de cuatro etapas. Conocerlas explica todo resultado raro.

| Etapa | Qué pasa | Herramienta estándar |
|---|---|---|
| 1. Detectar | Encuentra la cara, ubica landmarks | **InsightFace `buffalo_l`** (el estándar de facto) |
| 2. Codificar | Comprime la cara en un vector de identidad | **Embeddings ArcFace** |
| 3. Generar | Reconstruye la cara con la identidad fuente | **InSwapper** (GAN, rápido) o difusión (lento, mejor) |
| 4. Mezclar + restaurar | Igualar color, difuminar bordes, recuperar textura | **GFPGAN** |

> **La etapa 4 es lo que hace que los swaps de 2026 se vean bien.** Saltarse el pase de restauración es la razón más común de que un swap parezca una pegatina.

| Proyecto | Licencia | Nota |
|---|---|---|
| **[FaceFusion](https://github.com/facefusion/facefusion)** | Código permisivo; **hereda términos no comerciales de los modelos** | 29.5k estrellas, mantenido activamente, la mejor puerta de entrada. Corre 100% local. 🚫 No comercial vía `inswapper`. |
| **[DeepFaceLive](https://github.com/iperov/DeepFaceLive)** | Código permisivo, modelos no comerciales | Face swap en tiempo real desde webcam, para streaming. Misma restricción. |
| **[DeepFaceLab](https://github.com/iperov/DeepFaceLab)** | Código permisivo, modelos no comerciales | La vía de máxima calidad. Horas de entrenamiento, mejor fidelidad. Curva empinada. Misma restricción. |

> **ReActor eliminado.** El repo original de este popular nodo de face swap para Stable Diffusion ya no es accesible y las copias que sobreviven son forks de pocas estrellas sin procedencia verificable. Preferimos dejar un hueco antes que linkear algo que no podemos respaldar.

**Regla práctica:** GANs (InSwapper) para tiempo real y volumen; swappers de difusión para stills donde la calidad es crítica.

> ⚠️ **El problema de herencia de licencias, dicho una vez y claro:** una herramienta permisiva que incluye pesos no comerciales **no** es gratis comercialmente. Esta es la forma más común de romper sin darte cuenta un contrato con cliente usando IA "gratis".

## 🎙️ Voz, habla y audio

| Proyecto | Licencia | Nota |
|---|---|---|
| **[Chatterbox](https://github.com/resemble-ai/chatterbox)** (Resemble AI) | **MIT** | ✅ **El modelo de voz que hay que usar.** Clonaje zero-shot desde un clip de referencia corto, con controles de CFG y exageración. `Chatterbox-Turbo` es de **350M** y está pensado explícitamente para poco VRAM; `Chatterbox-Multilingual V3` es 500M y cubre **23+ idiomas**. Incluye un `example_for_mac.py`. |
| **[Qwen3-Omni](https://github.com/QwenLM/Qwen3-Omni)** (Alibaba) | **Apache-2.0** | ✅ Omni-modal end-to-end: texto, imagen, audio y video de entrada; **salida de voz en streaming en tiempo real**. 119 idiomas de texto, 19 de entrada de voz, 10 de salida. |
| **[Whisper](https://github.com/openai/whisper)** | **MIT** | Transcripción. Te da la transcripción de referencia que el clonaje necesita. |
| **[RVC](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)** | Revisa el model card | Voice **conversion** — cambia el timbre de una voz por el de otra, en vez de clonar desde cero. |

> ⚠️ **`F5-TTS` salió de esta lista** por una sola razón: código MIT pero **pesos CC-BY-NC**. Fue el TTS abierto más recomendado por dos años y no se puede usar legalmente para trabajo pagado. `Chatterbox` es MIT de punta a punta y es el reemplazo.

> ⚠️ **Un bug de licencia documentado que conviene conocer:** la conversión [cstr/f5-tts-GGUF](https://huggingface.co/cstr/f5-tts-GGUF) declaraba `mit` y después se corrigió a `cc-by-nc-4.0` para coincidir con upstream. Si encontraste un GGUF de TTS que dice MIT, probablemente está mal. Por eso se revisa la licencia de los pesos y no la del repo.

**Notas prácticas de Chatterbox:** clona solo desde audio que te pertenezca o que tengas permiso de usar. El V3 Multilingual mejora la preservación de acento y similitud de hablante entre idiomas, y eso importa más que la calidad de audio cruda si tu voz fuente tiene acento.

## 🗣️ Lip sync y talking heads

La forma más barata de tener diálogo en video con IA. Cambia la boca, conserva la actuación.

| Proyecto | Licencia | Veredicto |
|---|---|---|
| **[LatentSync](https://github.com/bytedance/LatentSync)** (ByteDance) | **Apache-2.0** | ✅ **El que hay que usar.** Difusión latente end-to-end, sin representación de movimiento intermedia. 6k estrellas. Inferencia, checkpoints **y código de entrenamiento** abiertos. La versión 1.6 entrena a 512×512 específicamente para arreglar el blur de las versiones anteriores. Preservación de identidad fuerte. |
| **[MuseTalk](https://github.com/TMElyralab/MuseTalk)** (Tencent Music) | **Código MIT, pesos libres para cualquier uso** | ✅ Raro — el README dice que los modelos entrenados están *"available for any purpose, even commercially."* Tiempo real a **30fps+ en una Tesla V100**. 6.5k estrellas. Los pesos solo modifican una región facial de 256×256. |
| **[SadTalker](https://github.com/OpenTalker/SadTalker)** | Revisa el model card | Agrega movimiento de cabeza, no solo labios. 14.1k estrellas. ⚠️ La resolución de salida la limita su etapa de render 3DMM — no puede entregar 4K. |

> ⚠️ **La advertencia de MuseTalk:** sus **datos de test** fueron recolectados de internet y están *"available for non-commercial research purposes only."* Eso aplica a los datos de test, **no** al modelo. No incluyas el set de test en un proyecto comercial.

**Ajustes de LatentSync:** `inference_steps` 20–50 (más = mejor, más lento), `guidance_scale` 1.0–3.0 (más = sync más justo, puede verse artificial pasado 2.5).

> **La trampa del orden de generación:** MuseV (o cualquier modelo image-to-video) genera la cara → **interpola** el framerate → *luego* corre el lip sync. Hacer lip sync antes de interpolar hace que la boca tartamudee.

## 🎵 Separación y restauración de audio

| Proyecto | Licencia | Veredicto |
|---|---|---|
| **[demucs-rs](https://github.com/nikhilunni/demucs-rs)** | **Apache-2.0** | ✅ **El que hay que usar.** Reimplementación en Rust de HTDemucs v4 con **aceleración Metal en macOS**, más un plugin VST3/CLAP para soltarlo en un DAW y escuchar los stems en vivo. Creado en 2026, en desarrollo activo. |
| **[AudioCraft](https://github.com/facebookresearch/audiocraft)** (Meta) | **MIT** | ✅ Generación de música y sonido — MusicGen y compañía. |
| **[Demucs](https://github.com/adefossez/demucs)** (Meta) | **MIT** | ⚠️ El original y sigue siendo la implementación de referencia, pero **el autor se fue de Meta** y dice que ya no trabaja activamente en esto. Sigue publicando releases (4.1.0, Jul 2026), así que funciona — nomás puede que no lo arreglen. Usa `demucs-rs`. |

**Para qué sirve realmente separar en post:** sacar diálogo limpio de una grabación de locación con ruido, o despejar música debajo de un voiceover. Para producción musical también funciona igual de bien.

> ⚠️ **La trampa del mantenimiento, dicha claro:** la herramienta de separación musical con más estrellas y más links está **efectivamente sin mantener por su autor**. Revisa la fecha del último release antes de construir un pipeline encima — este campo cambia más rápido que la imagen.

## 🔧 Restauración de caras y upscaling

| Proyecto | Licencia | Nota |
|---|---|---|
| **[Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)** | **BSD-3** | ✅ Upscaling general. Se combina con el restaurador de caras para el fondo. |
| **[GFPGAN](https://github.com/TencentARC/GFPGAN)** (Tencent) | **Apache-2.0** | ✅ Licencia comercial limpia. Restauración ciega de caras. Usa los pesos de v1.4. |

> ⚠️ **`CodeFormer` removida.** Su licencia es **S-Lab License 1.0**, que concede uso *"for non-commercial purpose"* — pese a que el repo parezca permisivo. Fue la recomendación estándar por años y no se puede usar legalmente para trabajo pagado. `GFPGAN` es el reemplazo limpio.

**Nota de ajuste:** si usas `GFPGAN` v1.4, el ajuste `upscale` es la palanca principal de calidad — empieza en 2 y súbelo solo si la salida se ve suave.

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

No hay tier gratuito permanente. Los $5 expiran a los 30 días. Este es el ejemplo más claro que hay en internet de un claim de tier gratis repetido hasta volverse falso. **Por eso Cerebras no aparece en la tabla de abajo.**

## Tiers verificados

| Proveedor | Tier gratis | ¿Tarjeta? | ¿Comercial? | Confianza |
|---|---|---|---|---|
| **[Google AI Studio](https://ai.google.dev/pricing)** | Solo Flash / Flash-Lite. **Los Pro pasaron a pago el 1 Abr 2026.** | No | ✅ Sí | Publicado por el proveedor. ⚠️ **Los RPM/RPD reales están en tu consola, no en los docs.** |
| **[Groq](https://console.groq.com/docs/rate-limits)** | Comúnmente ~30 RPM. Los topes diarios varían por modelo. | No | ✅ Sí | ⚠️ **Reportado por la comunidad.** Groq no publica topes diarios por modelo. |
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

**Stack creativo comercial $0** — ComfyUI + Wan2.2 `TI2V-5B` (Apache-2.0, ~8GB) + Qwen-Image (Apache-2.0) + MuseTalk (MIT) + Chatterbox (MIT) + GFPGAN (Apache-2.0), más un fallback pagado para entregables de cliente, para no quedarte atrapado en un 429. Cada componente es comercialmente limpio.

**Stack de texto $0** — Ollama + Qwen3.5-9B (Apache-2.0, 262K) para todo lo privado. Tier gratis de Google AI Studio para el resto. Lee los headers de respuesta.

**El piso real** — los tiers gratuitos alojados son regalos que se pueden cancelar. Un modelo en tu propio hardware no tiene rate limit, ni cláusula de entrenamiento, ni aviso de cierre, ni bloqueo geográfico. Pierdes calidad frontier y velocidad. Ganas el único nivel que nadie puede revocar.

---

## Cómo contribuir

¿Encontraste algo mal, o una licencia que cambió?

**[Abre un issue](CONTRIBUTING.md)** — las correcciones con un link a la fuente son la contribución más valiosa acá. Una licencia que cambió en silencio es exactamente el modo de falla que esta lista existe para evitar.

## Licencia

Contenido [CC BY 4.0](LICENSE). Las marcas y los pesos de los modelos siguen siendo de sus dueños respectivos — esta lista los enlaza, no los redistribuye.
