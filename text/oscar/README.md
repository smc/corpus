# Download OSCAR corpus for Malayalam

https://huggingface.co/oscar-corpus


```bash
pip install datasets
```

```python
from datasets import load_dataset
# Load the OSCAR-2301 dataset
dataset = load_dataset("oscar", "unshuffled_deduplicated_ml", split="train")
# Save dataset to text file
with open("data/oscar_corpus.txt", "w", encoding="utf-8") as f:
    for example in dataset:
        f.write(example["text"] + "\n")

```
