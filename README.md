# 🍂 Matsuo-Basho-Assistant

*A tiny haiku poet, fine-tuned from SmolLM2-135M-Instruct with LoRA.*

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Transformers](https://img.shields.io/badge/🤗-Transformers-yellow)
![Parameters](https://img.shields.io/badge/Parameters-135M-green)

---

## ✨ Overview

**Matsuo-Basho-Assistant** is a parameter-efficient fine-tune of **SmolLM2-135M-Instruct** trained on a custom dataset of approximately 920 haiku examples.

Given a few thematic keywords, the model generates short haiku-style poetry inspired by nature, seasons, solitude, observation, and impermanence.

### Quick Example

**Input**

```text
Write a haiku about: moon, silence, river
```

**Output**

```text
The moon is the water
stream in the calm tide
I don't drink it, just hold on
```

---

## 🎯 Why this project?

Large language models are powerful, but many require significant hardware resources to run or fine-tune.

This project explores how far a **135 million parameter model** can go when trained for a highly specialized creative task.

Matsuo-Basho-Assistant can:

* Be fine-tuned on a free Google Colab T4 GPU
* Run locally on modest hardware
* Generate poetry in seconds
* Serve as an educational example of LoRA fine-tuning
* Demonstrate the potential of small language models

This repository is both a creative experiment and a practical learning resource.

---

## 📦 Model Details

| Property           | Value                                 |
| ------------------ | ------------------------------------- |
| Base Model         | HuggingFaceTB/SmolLM2-135M-Instruct   |
| Parameters         | 135M                                  |
| Fine-Tuning Method | LoRA (PEFT)                           |
| Training Platform  | Google Colab                          |
| Dataset Size       | ~920 cleaned examples                 |
| Task               | Category-conditioned haiku generation |
| Language           | English                               |

---

## 🖋️ Example Generations

### Prompt

```text
Write a haiku about: snow, loneliness
```

### Generation

```text
Snow is my mirror
it reflects myself
only in winter
```

---

### Prompt

```text
Write a haiku about: cat, sunlight
```

### Generation

```text
The sun shines on the cat
through its fur and whiskers
as it eats
```

---

### Prompt

```text
Write a haiku about: stars, night
```

### Generation

```text
Night star shines in silver light
only one can see it
without sleep
```

---

### Prompt

```text
Write a haiku about: thunder, mountain
```

### Generation

```text
The thunder, it is not
his voice but an echo of
my heartbeat
```

---

### Prompt

```text
Write a haiku about: fallen leaves, path
```

### Generation

```text
Heavy on the leaf
you walk like a leaf
now it falls away
```

---

### Additional Interesting Generations

```text
Rain of memories
you keep me on my own way
```

```text
Old temple with mossy flowers
a rustling sound of leaves
```

```text
The fishing rod
sticks in the river
with a sigh and a promise
```

```text
Lampfall through lanterns
the fireflies dance
in the darkness
```
---

## 💡 Example Prompts

Try these prompts or invent your own:

```text
Write a haiku about: moon, silence, river
Write a haiku about: crow, autumn
Write a haiku about: snow, loneliness
Write a haiku about: tea, silence
Write a haiku about: mountain, dawn
Write a haiku about: ocean, storm
Write a haiku about: cherry blossom, spring
Write a haiku about: stars, night
Write a haiku about: fireflies, summer
Write a haiku about: fallen leaves, path
```

---

## 🧪 Training Data Format

Each training sample is a JSON object:

```json
{
  "haiku": "A reflection in / a spoon, my face is upside / down, I'm a frown, then grin",
  "categories": [
    "kitchen",
    "observation",
    "humor"
  ]
}
```

The model learns to generate a haiku conditioned on the supplied categories.

---

## 🚀 Usage

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_path = "./Matsuo-Basho-Assistant"

tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoModelForCausalLM.from_pretrained(model_path)

prompt = "Write a haiku about: moon, silence, river"

inputs = tokenizer(prompt, return_tensors="pt")

outputs = model.generate(
    **inputs,
    max_new_tokens=40,
    temperature=0.8,
    top_p=0.9,
    do_sample=True
)

print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

---

## ⚠️ Limitations

- Outputs do not strictly follow the traditional 5-7-5 syllable structure.
- Some generations may only loosely follow the provided themes.
- The model was trained on a relatively small custom dataset (~920 examples).
- Results are intended for creative and educational use.

---

## 📚 Educational Value

This project demonstrates:

- LoRA fine-tuning with PEFT
- Adapting a small language model for a creative task
- Instruction tuning on custom datasets
- Dataset cleaning and preparation
- Running and training models on free Google Colab GPUs
- Efficient experimentation with small language models

The goal is to show that useful and interesting fine-tuning projects do not require billion-parameter models.

---

## 🖥️ Hardware Requirements

One of the goals of this project is accessibility.

Because the model contains only **135 million parameters**, it can be:

- Run on CPUs for experimentation
- Run comfortably on consumer GPUs
- Fine-tuned on free Google Colab hardware
- Used as a lightweight local poetry assistant

This makes it a good starting point for students, hobbyists, and researchers interested in language model fine-tuning.

---

## 🙏 Acknowledgements

- Hugging Face for SmolLM2
- Transformers
- PEFT
- TRL
- Datasets
- The tradition of haiku poetry and the works of Matsuo Bashō

---
## Results

Although the model contains only 135M parameters, it successfully learned:

- Haiku-like structure
- Nature-oriented imagery
- Short-form poetic generation
- Theme-conditioned outputs

<h3><em>"The model is not intended to perfectly replicate traditional 5-7-5 haiku, but rather to explore how much poetic behavior can be learned through lightweight fine-tuning."</em></h3>
---

## 📜 License

This project inherits the licensing terms of the base model:

HuggingFaceTB/SmolLM2-135M-Instruct

Please review the base model's license before redistribution or commercial use.

---

*"Stars fall silently — even a small model can learn to see the moon."* 🌕
