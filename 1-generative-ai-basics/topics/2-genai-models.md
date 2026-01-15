# What are Generative AI Models?


### What Are Generative AI Models?

**Definition:** Generative AI models are a subset of machine learning algorithms designed to generate **new data instances** that resemble the training data.

In engineering terms, they learn the **probability distribution** of a dataset. If a "Discriminative Model" (like a spam filter) learns the boundary between classes (Spam vs. Not Spam), a "Generative Model" learns the geometry of the data itself, allowing it to sample from that distribution to create entirely new artifacts.

---

### 1. The Core Taxonomy: Architectures

Different "families" of models solve generation for different data types.

#### A. Autoregressive Transformers (The "Brain")

* **Dominant Domain:** Text, Code (LLMs).
* **Mechanism:** They process data sequentially. They predict the probability of the next token () based on all previous tokens () using **Self-Attention**.
* **Key Trait:** They are "stateless" functions that are fed their own output back as input to generate long sequences.
* **Examples:** GPT-4, Claude 3, Llama 3.

#### B. Diffusion Models (The "Artist")

* **Dominant Domain:** Images, Video, Audio.
* **Mechanism:** They are trained to reverse a noise process.
1. **Forward Process:** Slowly add Gaussian noise to an image until it is pure static.
2. **Reverse Process (Learning):** The model learns to predict the noise added at each step and subtract it.
3. **Generation:** Start with pure random noise and iteratively "denoise" it guided by a text prompt until a clear image emerges.


* **Key Trait:** Slower than GANs but highly stable and controllable.
* **Examples:** Stable Diffusion (SDXL), Midjourney, DALL-E 3, Sora (Video).

#### C. Generative Adversarial Networks (GANs) (The "Forger")

* **Dominant Domain:** High-res Image upscaling, Style Transfer, Deepfakes.
* **Mechanism:** A game-theoretic approach with two competing neural networks:
* **Generator:** Tries to create fake data.
* **Discriminator:** Tries to detect if data is real or fake.


* **Key Trait:** Extremely fast inference (single pass), but notoriously hard to train (unstable convergence).
* **Examples:** StyleGAN (generating realistic human faces), Super-Resolution (DLSS in gaming).

---

### 2. Modalities & The Model Landscape

*A breakdown of models by what they produce.*

| Modality | Input  Output | Underlying Tech | Key Models |
| --- | --- | --- | --- |
| **Text (LLM)** | Text  Text/Code | Transformer (Decoder-only) | **GPT-4o**, **Claude 3.5**, **Llama 3**, **Mistral** |
| **Image** | Text  Image | Latent Diffusion | **Stable Diffusion 3**, **Flux**, **Midjourney v6** |
| **Video** | Text/Image  Video | Spacetime Patches (Diffusion + Transformer) | **Sora**, **Runway Gen-3**, **Luma Dream Machine** |
| **Audio/Speech** | Text  Audio | Audio Transformer / VAE | **ElevenLabs** (TTS), **Suno** (Music), **Whisper** (ASR - distinct but related) |
| **Multimodal** | Image/Text  Text | Vision Transformer (ViT) + LLM | **GPT-4o**, **Gemini 1.5 Pro**, **LLaVA** (Open Source) |

---

### 3. The Engineering Lifecycle of a Model

*How a mathematical formula becomes a product.*

1. **Pre-Training (The Expensive Part):**
* The model consumes terabytes of data (e.g., the Common Crawl) to learn "world knowledge" and grammar.
* *Cost:* Millions of dollars in GPU compute.
* *Result:* A "Base Model" (e.g., `Llama-3-70b-Base`). It can predict text but follows instructions poorly.


2. **Post-Training / Alignment (The Usable Part):**
* **SFT (Supervised Fine-Tuning):** Showing the model Q&A pairs so it learns to act like an assistant.
* **RLHF (Reinforcement Learning from Human Feedback):** Humans rank model outputs to teach it safety, tone, and refusal of harmful queries.
* *Result:* An "Instruct" or "Chat" Model (e.g., `Llama-3-70b-Instruct`).


3. **Inference (The Runtime):**
* The model is deployed (quantized to Int8 or FP16) to process user prompts. This is where parameters like `Temperature` (randomness) and `Top-P` (nucleus sampling) are tuned.
