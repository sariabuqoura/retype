```python
from transformers import pipeline

# Load the sentiment-analysis pipeline
sentiment_analyzer = pipeline('sentiment-analysis')

# Example text
text = "I love using Hugging Face's Transformers library!"

# Perform sentiment analysis
result = sentiment_analyzer(text)

print(result)
```
