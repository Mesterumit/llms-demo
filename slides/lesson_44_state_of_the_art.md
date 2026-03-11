---
marp: true
theme: default
paginate: true
style: |
  section {
    background-color: #1a1a2e;
    color: #e0e0e0;
  }
  section h1, section h2, section h3 {
    color: #e2b55a;
  }
  section a {
    color: #93c5fd;
  }
  section strong {
    color: #f0f0f0;
  }
  section table th {
    background-color: #2a2a4a;
    color: #e2b55a;
  }
  section table td {
    background-color: #1e1e36;
    color: #e0e0e0;
  }
  section code {
    background-color: #2a2a4a;
    color: #e0e0e0;
  }
  section pre {
    background-color: #12122a;
  }
  section::after {
    color: #888;
  }
---

# Lesson 44: State of the art in generative AI

**LLM landscape and foundations**

---

## Recap: how LLMs work

- **Decoder-only transformers**: Self-attention and feed forward layers
- **Tokenization:** Text is split into tokens (subwords), not characters or words
- **Autoregressive generation:** LLMs predict the next token given all previous tokens
- **Training:** Learned from massive text corpora via self-supervised learning
- **Scale:** Billions of parameters encode language patterns and knowledge

We covered transformers in depth earlier - here we focus on the **landscape** of available models

---

## Today's outline

**1. The landscape** - what's available
- Open vs closed weights, licensing
- Text and code generation models

**2. Evaluating models** - how to compare and choose
- Model sizes and parameters
- Context length
- Benchmarks

**3. Looking ahead** - where this is going
- Key trends
- Limitations

---

# The landscape

What models are available and who makes them

- Open vs closed weights
- Licensing considerations
- Text and code generation models

---

## Open vs closed weights

**Closed weights (API only):**
- Sources: OpenAI, Anthropic, Google, Moonshot AI
- Best performance, easy to use
- Can't self-host, can't fine-tune (some exceptions), ongoing costs

**Open weights (self-hostable):**
- Sources: Meta, Mistral AI, Alibaba, Zhipu AI, Hugging Face
- Full control, fine-tunable, privacy-friendly, free to use
- Require infrastructure, generally less capable

---

## Licensing considerations

- **Closed weights**: governed by Terms of Service, pay per token, check data policies
- **Open weights**: "open" does not always mean "open source" - always check the license
  - **Permissive** (Apache 2.0, MIT): Mistral, Falcon, DeepSeek, Phi
  - **Restricted**: Llama (free, but limited above 700M monthly active users)

**Key takeaway:** Always check the license before using a model commercially

---

## Text generation models: closed weights

| Model | Company | Strengths |
|-------|---------|-----------|
| [GPT](https://openai.com) | OpenAI | Strong reasoning |
| [Claude](https://anthropic.com) | Anthropic | Strong analysis |
| [Gemini](https://gemini.google.com) | Google | Search integration |
| [Kimi](https://kimi.moonshot.cn) | Moonshot AI | Long context, strong multilingual |
| [Grok](https://x.ai) | xAI | Strong reasoning, real-time knowledge |
| [Command](https://cohere.com) | Cohere | Enterprise search and RAG |

---

## Text generation models: open weights

| Model | Company | Strengths |
|-------|---------|-----------|
| [Llama](https://huggingface.co/meta-llama) | Meta | 8B to 70B parameters, strong open option |
| [Mistral](https://huggingface.co/mistralai) | Mistral AI | Efficient 7B model, good quality |
| [DeepSeek](https://huggingface.co/deepseek-ai) | DeepSeek | Strong reasoning, competitive with closed models |
| [Qwen](https://huggingface.co/Qwen) | Alibaba | Competitive multilingual models |
| [GLM](https://huggingface.co/THUDM) | Zhipu AI | Strong bilingual (English/Chinese) |
| [Trinity](https://huggingface.co/arcee-ai) | Arcee AI | Broad task coverage |
| [Phi](https://huggingface.co/microsoft) | Microsoft | Small, efficient, strong for size |
| [Falcon](https://huggingface.co/tiiuae) | TII (Abu Dhabi) | Permissive license, multilingual |

---

## Code generation models

Most general-purpose LLMs can generate code, but some companies offer code-specialized variants fine-tuned for programming tasks.

| Model | Company | Access | Strengths |
|-------|---------|--------|-----------|
| [Codex](https://openai.com) | OpenAI | Closed | Code-specialized, powers Copilot |
| [CodeLlama](https://huggingface.co/codellama) | Meta | Open | 7B-34B, code-specialized |
| [StarCoder](https://huggingface.co/bigcode) | Hugging Face | Open | 15B, permissive training data |
| [DeepSeek Coder](https://huggingface.co/deepseek-ai) | DeepSeek | Open | Strong open alternative |
| [Qwen Coder](https://huggingface.co/Qwen) | Alibaba | Open | Competitive code generation |

---

# Evaluating models

How to compare and choose models

- Model sizes and parameters
- Context length
- Benchmarks

---

## Model sizes and parameters

- **Parameters**: the learned weights that define the model's behavior
- More parameters -> more capable, but also more expensive to run

| Size class | Examples | Hardware |
|------------|----------|-----------------|
| Small (1-3B) | Phi-2, TinyLlama | CPU, laptop |
| Medium (7-13B) | Mistral 7B, Llama 8B | Single consumer GPU |
| Large (30-70B) | Llama 70B, CodeLlama 34B | Multiple GPUs / cloud |
| Frontier (100B+) | GPT, Claude | API only |

**Mixture of Experts (MoE):** some models (Mixtral, DeepSeek) have many total parameters but only activate a subset per token - large capacity, lower compute cost.

**Key takeaway:** Bigger is not always better - match model to task

---

## Context and context length

- **Context window**: number of tokens a model can process (input + output)

| Model | Context length |
|-------|---------------|
| GPT (2020) | 4K tokens |
| GPT (2023) | 128K tokens |
| Claude (2024) | 200K tokens |
| Gemini (2024) | 1M tokens |

- Longer context = larger documents, longer conversations
- Cost scales with context length (more tokens = more compute = more $$$)

---

## Benchmarks and evaluation

- Benchmarks provide a **standardized way to compare** models

| Benchmark | What it measures |
|-----------|-----------------|
| [MMLU](https://huggingface.co/datasets/cais/mmlu) | General knowledge across 57 subjects |
| [HumanEval](https://github.com/openai/human-eval) | Code generation (Python) |
| [GSM8K](https://huggingface.co/datasets/openai/gsm8k) | Math reasoning |
| [MT-Bench](https://huggingface.co/spaces/lmsys/mt-bench) | Multi-turn conversation quality |
| [HellaSwag](https://huggingface.co/datasets/Rowan/hellaswag) | Common sense reasoning |
| [Chatbot Arena](https://lmarena.ai) | Human preference rankings (head-to-head) |

- Scores don't always reflect real-world performance - test on your own tasks

---

# Looking ahead

Where the field is going

- Key trends
- Limitations

---

## Key trends

1. **Longer context** - From 4K to 1M+ tokens
2. **Smaller, more efficient** - Better performance at smaller sizes
3. **Open alternatives improving** - Closing the gap with closed models
4. **Specialization** - Domain-specific fine-tuned variants
5. **Autonomous agents** - Models that can use tools and take actions
6. **Reasoning models** - Dedicated chain-of-thought architectures (o1, DeepSeek-R1)

---

## Limitations and considerations

- **Hallucinations**: LLMs are probabilistic text generators, not databases of facts
- **Reasoning gaps**: struggle with multi-step logic, math, and planning
- **Cost**: API usage is metered; scales with tokens and context length
- **Privacy**: closed models send data to third-party servers
- **Ethics**: training data bias, copyright, and environmental impact

---

## Summary

- **The landscape**: closed weights for performance, open weights for control
- **Model catalog**: major text and code generation models from many providers
- **Evaluating models**: size, context length, and benchmarks help compare options
- **Looking ahead**: longer context, smaller models, reasoning, and agents
- Always test on your own tasks - benchmarks and hype don't tell the full story

---

## Next lesson

**Lesson 45: Practical LLM deployment**
- Decoding strategies and hyperparameters
- Quantization for running models locally
- Local hosting, cloud hosting, and API access
- Performance and cost tradeoffs
