# 03 · Fine-tuning

When to use it, how to do it, and why most of the time you shouldn't.

## The decision tree

```
Can prompt engineering solve it?
    YES → stop, you're done
    NO  ↓

Does RAG solve it?
    YES → stop, you're done
    NO  ↓

Is the problem a specific style/format/domain?
    YES → fine-tuning might help
    NO  → reconsider the problem
```

Fine-tuning makes sense for:
- Consistent output format that prompting can't reliably achieve
- Specific writing style or persona
- Domain-specific knowledge that RAG can't cover (implicit patterns, not facts)
- Latency-sensitive applications where shorter prompts matter

Fine-tuning does NOT fix:
- Bad base model for your task
- Missing knowledge (use RAG)
- Logic and reasoning problems

## LoRA vs QLoRA

| Method | GPU VRAM needed | Speed | Quality |
|---|---|---|---|
| Full fine-tuning | 40GB+ | Slow | Best |
| LoRA | 16–24GB | Medium | Very good |
| QLoRA | 8–12GB | Slower than LoRA | Good |

For most use cases: QLoRA on a 16GB consumer GPU works fine.

## Notebooks

| Notebook | Description |
|---|---|
| `01_when_to_finetune.ipynb` | Decision framework with examples |
| `02_dataset_curation.ipynb` | Building a high-quality training set |
| `03_lora_finetuning.ipynb` | LoRA fine-tuning with HuggingFace PEFT |
| `04_qlora_finetuning.ipynb` | QLoRA for smaller GPUs |
| `05_evaluation.ipynb` | Evaluating fine-tuned models properly |

## Setup

```bash
pip install transformers peft datasets accelerate bitsandbytes trl
```

## Resources

- [HuggingFace PEFT](https://huggingface.co/docs/peft/index)
- [Argilla - Dataset curation](https://docs.argilla.io/)
- [Eleuther LM Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness)
- [Unsloth - Fast fine-tuning](https://github.com/unslothai/unsloth)
