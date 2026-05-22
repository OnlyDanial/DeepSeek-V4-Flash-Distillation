# DeepSeek V4 Flash Distillation

A curated collection of high quality distillation datasets, reasoning traces, and fine-tuning pipelines generated using the DeepSeek V4 Flash (Max Thinking) teacher model.

DeepSeek V4 Flash (Max Thinking) was selected as the teacher model for this distillation pipeline. Although the Max Thinking mode generates a high volume of output tokens per prompt compared to other models, its token pricing remains unmatched. The model offers exceptional reasoning and agentic capabilities at an extremely low token cost.

The datasets are structured inside the s1K/ directory to accommodate future expansions and additional distillation runs.

---

## Distillation Datasets
| Dataset | Focus | Status |
| ----- | ----- | ----- |
| [s1K](https://huggingface.co/datasets/simplescaling/s1K) | Logic, Math, Science | [Complete](https://huggingface.co/datasets/OnlyDanial/s1K-DeepSeek-V4-Flash-Max-Thinking) |
| [GSM8K](https://huggingface.co/datasets/openai/gsm8k) | Math | Coming Soon |

---

## Repository Structure

```
.
├── README.md
└── s1K/
    ├── 01_raw_full_metadata.jsonl       # Complete base records and comprehensive metadata
    ├── 02_sharegpt.jsonl                # ShareGPT-compatible multi-turn format
    ├── 03_alpaca.jsonl                  # Classic Alpaca instruction-output format
    ├── 04_openai_chat_finetune.jsonl    # OpenAI-style chat message schema
    ├── 05_trl_messages.jsonl            # Hugging Face TRL and SFTTrainer format
    ├── 06_text_sft.jsonl                # Raw text completion and sequence format
    └── 07_reasoning_traces.jsonl        # Pure chain-of-thought (CoT) extraction
```

## Dataset Formats (s1K/)

| File | Target Framework / Loader | Core Fields |
| ----- | ----- | ----- |
| 01_raw_full_metadata.jsonl | Custom analysis and parsing | id, instruction, input, teacher_response, teacher_reasoning, solution, answer |
| 02_sharegpt.jsonl | ShareGPT data loaders | id, conversations |
| 03_alpaca.jsonl | Alpaca and SFT pipelines | instruction, input, output, system |
| 04_openai_chat_finetune.jsonl | OpenAI Fine-Tuning API | messages |
| 05_trl_messages.jsonl | Hugging Face TRL / SFTTrainer | id, messages |
| 06_text_sft.jsonl | Text completion pipelines | id, text |
| 07_reasoning_traces.jsonl | Explicit chain-of-thought distillation | id, problem, solution, answer, teacher_reasoning |

## Token Use & Cost

| Dataset / Run | Input Tokens | Output Tokens | Total Tokens | Input Cost | Output Cost | Total Cost |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| s1k | 274,875 | 23,038,561 | 23,313,436 | $0.04 | $6.45 | $6.49 |
| **TOTAL** | **274,875** | **23,038,561** | **23,313,436** | **$0.04** | **$6.45** | **$6.49** |

## DeepSeek V4 Flash Max Thinking Benchmarks

### Knowledge & Reasoning

| Benchmark | Score |
| ----- | ----- |
| MMLU-Pro (EM) | 86.2 |
| SimpleQA-Verified (Pass@1) | 34.1 |
| Chinese-SimpleQA (Pass@1) | 78.9 |
| GPQA Diamond (Pass@1) | 88.1 |
| HLE (Pass@1) | 34.8 |
| LiveCodeBench (Pass@1) | 91.6 |
| Codeforces (Rating) | 3052 |
| HMMT 2026 Feb (Pass@1) | 94.8 |
| IMOAnswerBench (Pass@1) | 88.4 |
| Apex (Pass@1) | 33.0 |
| Apex Shortlist (Pass@1) | 85.7 |

### Long Context

| Benchmark | Score |
| ----- | ----- |
| MRCR 1M (MMR) | 78.7 |
| CorpusQA 1M (ACC) | 60.5 |

### Agentic

| Benchmark | Score |
| ----- | ----- |
| Terminal Bench 2.0 (Acc) | 56.9 |
| SWE Verified (Resolved) | 79.0 |
| SWE Pro (Resolved) | 52.6 |
| SWE Multilingual (Resolved) | 73.3 |
| BrowseComp (Pass@1) | 73.2 |
| HLE w/ tools (Pass@1) | 45.1 |
| MCPAtlas (Pass@1) | 69.0 |
| GDPval-AA (Elo) | 1395 |
| Toolathlon (Pass@1) | 47.8 |

## Credits

* **s1K Dataset (Simple Scaling s1 Project)**
  * Repository: [simplescaling/s1 on GitHub](https://github.com/simplescaling/s1)
  * Hugging Face Dataset: [simplescaling/s1K on Hugging Face](https://huggingface.co/datasets/simplescaling/s1K)

* **Teacher Model (DeepSeek V4 Flash)**
  * Hugging Face Repository: [deepseek-ai/DeepSeek-V4-Flash on Hugging Face](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)
