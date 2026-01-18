```python
from transformers import DistilBertTokenizer, DistilBertForSequenceClassification
import torch

# Load pre-trained tokenizer and model
tokenizer = DistilBertTokenizer.from_pretrained("distilbert-base-uncased-finetuned-sst-2-english")
model = DistilBertForSequenceClassification.from_pretrained("distilbert-base-uncased-finetuned-sst-2-english")

# Sample text
text = "I absolutely love this product! It's amazing."

# Tokenize input text
inputs = tokenizer(text, return_tensors="pt")  # Convert to PyTorch tensors

# Perform inference
with torch.no_grad():
    outputs = model(**inputs)

# Extract logits and get prediction
logits = outputs.logits
predicted_class = torch.argmax(logits, dim=1).item()

# Interpret result
label_map = {0: "Negative", 1: "Positive"}
print(f"Sentiment: {label_map[predicted_class]}")

```
