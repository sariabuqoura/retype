```python
from textattack.attack_recipes import TextFoolerJin2019
from textattack import Attacker
from textattack.datasets import Dataset
from transformers import pipeline
from textattack.models.wrappers import ModelWrapper
import torch

class SentimentWrapper(ModelWrapper):
    def __init__(self):
        self.model = pipeline('sentiment-analysis')

    def __call__(self, text_inputs):
        outputs = []
        for text in text_inputs:
            result = self.model(text)[0]
            if result['label'] == 'POSITIVE':
                probs = [0.0, float(result['score'])]
            else:
                probs = [float(result['score']), 0.0]
            outputs.append(probs)
        return torch.tensor(outputs)

model_wrapper = SentimentWrapper()

examples = [("This movie is great and amazing!", 1),
            ("This was a terrible waste of time.", 0),
            ("I really enjoyed watching this film.", 1),
            ("The worst movie I've ever seen.", 0)]

dataset = Dataset(examples)
attack = TextFoolerJin2019.build(model_wrapper)
attacker = Attacker(attack, dataset)
results = attacker.attack_dataset()

```
