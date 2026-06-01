# Appendix - Fine-tuning

Fine-tuning is rarely the right first move. Most production problems are better solved by improving the prompt, adding RAG, or switching to a better base model. This appendix exists so you know when it is the right call and how to approach it when it is.

## When fine-tuning actually makes sense

- You need consistent output format or style that prompting cannot reliably produce
- You have a specific domain or persona that is too complex for a system prompt
- Latency is critical and you need a smaller, faster model that behaves like a larger one
- You have 50+ high-quality labeled examples and can measure the improvement objectively

When it does not make sense:
- You want the model to know new facts (use RAG for that)
- You have fewer than 50 examples
- You have not tried prompt engineering first

## Decision tree

```
Can better prompting fix it?
    YES -> fix the prompt
    NO  |
        v
Can RAG fix it (knowledge gap)?
    YES -> use RAG
    NO  |
        v
Is it a style/format/behavior issue?
    YES -> consider fine-tuning
    NO  -> reconsider the problem
```

## LoRA and QLoRA

Full fine-tuning requires 40GB+ of GPU VRAM. LoRA and QLoRA make fine-tuning practical on consumer hardware by training only a small set of adapter weights.

| Method | VRAM needed | Quality |
|---|---|---|
| Full fine-tuning | 40GB+ | Best |
| LoRA | 16-24GB | Very good |
| QLoRA | 8-12GB | Good |

```python
from peft import LoraConfig, get_peft_model
from transformers import AutoModelForCausalLM

model = AutoModelForCausalLM.from_pretrained("mistralai/Mistral-7B-v0.1")
config = LoraConfig(r=16, lora_alpha=32, target_modules=["q_proj", "v_proj"])
model = get_peft_model(model, config)
```

## Resources

- [HuggingFace PEFT](https://huggingface.co/docs/peft/index)
- [Unsloth - fast fine-tuning](https://github.com/unslothai/unsloth)
- [Argilla - dataset curation](https://docs.argilla.io/)
- [Eleuther LM Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness)
