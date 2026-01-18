---
label: LLM Guard
icon: book 
order: 999
---

!!!
Last Update on Jan, 2026.
!!!
Prerequisites

https://llm-guard.com/get_started/installation/

Supported Python versions:

- 3.9
- 3.10
- 3.11

## Install Python 11.4

[https://www.python.org/downloads/windows/#:~:text=3.11.4 cannot be used on Windows 7 or earlier.-,Download,-Windows installer (64-bit)](https://www.python.org/downloads/windows/#:~:text=3.11.4%20cannot%20be%20used%20on%20Windows%207%20or%20earlier.-,Download,-Windows%20installer%20(64%2Dbit))

## Create virtual environment

- Create venv using the prerequisites Python

## Required packages

```bash
pip install llm-guard
```

## Code

```jsx
from llm_guard import scan_output, scan_prompt
from llm_guard.input_scanners import Anonymize, PromptInjection, TokenLimit, Toxicity
from llm_guard.output_scanners import Deanonymize, NoRefusal, Relevance, Sensitive
from llm_guard.vault import Vault

vault = Vault()
input_scanners = [Anonymize(vault)]
output_scanners = [Deanonymize(vault)]

#input_scanners = [Anonymize(vault), Toxicity(), TokenLimit(), PromptInjection()]
#output_scanners = [Deanonymize(vault), NoRefusal(), Relevance(), Sensitive()]

prompt = input('Write your prompt here :')

sanitized_prompt, results_valid, results_score = scan_prompt(input_scanners, prompt)
if not all(results_valid.values()):
    print(f"Prompt {prompt} is not valid, scores: {results_score}")
    exit(1)

print(f"Prompt: {sanitized_prompt}")

```

## Explanation

Here's a table that explains various scanners, categorized into input and output scanners, with simple terms for each:

| **Category** | **Scanner** | **Explanation** |
| --- | --- | --- |
| **Input Scanners** | **Anonymize** | Removes or hides personal details from the input text to protect privacy. |
|  | **BanCode** | Detects and blocks code-related inputs, especially those that might be harmful or inappropriate. |
|  | **BanCompetitors** | Prevents input related to specific competitor products or brands. |
|  | **BanSubstrings** | Detects and blocks specific words or patterns (substrings) in the input text. |
|  | **BanTopics** | Blocks input that discusses specific topics (e.g., politics, violence). |
|  | **Code** | Identifies and manages input that contains computer code. |
|  | **Gibberish** | Detects random, nonsensical input that does not make sense (e.g., typing errors or random characters). |
|  | **InvisibleText** | Identifies and handles invisible or hidden characters in the input text, which may affect processing. |
|  | **Language** | Detects the language of the input text. |
|  | **PromptInjection** | Prevents manipulation of the system by injecting unwanted prompts or commands into the input. |
|  | **Regex** | Uses regular expressions to identify and block certain patterns in the text (e.g., email addresses, phone numbers). |
|  | **Secrets** | Detects sensitive information like passwords or keys hidden in the input. |
|  | **Sentiment** | Analyzes the emotional tone of the input, such as detecting if it's positive, negative, or neutral. |
|  | **TokenLimit** | Monitors the length of the input to ensure it does not exceed the maximum token (word unit) limit. |
|  | **Toxicity** | Detects harmful or abusive language in the input (e.g., hate speech or offensive comments). |
| **Output Scanners** | **BanCode** | Identifies and blocks harmful or inappropriate code outputs. |
|  | **BanCompetitors** | Prevents the output from mentioning or referencing specific competitors. |
|  | **BanSubstrings** | Detects and blocks specific unwanted words or patterns in the output text. |
|  | **BanTopics** | Prevents the model from outputting content on certain topics (e.g., politics, violence). |
|  | **Bias** | Detects biased or unfair representations in the output. |
|  | **Code** | Identifies if the output contains code and handles it accordingly. |
|  | **Deanonymize** | Detects if the output accidentally reveals personal or identifying information. |
|  | **JSON** | Validates if the output is properly formatted as JSON (a common data format). |
|  | **Language** | Ensures the output is in the desired language. |
|  | **LanguageSame** | Ensures the output maintains consistency in language usage throughout. |
|  | **MaliciousURLs** | Detects harmful or unsafe URLs in the output that could lead to security risks. |
|  | **NoRefusal** | Ensures the output does not refuse or block valid requests. |
|  | **ReadingTime** | Estimates the time required to read the output, ensuring it's not too long or short for a specific purpose. |
|  | **FactualConsistency** | Checks if the output is factually consistent and accurate. |
|  | **Gibberish** | Detects if the output contains nonsensical or meaningless content. |
|  | **Regex** | Uses regular expressions to filter or format the output based on specific patterns (e.g., phone numbers, dates). |
|  | **Relevance** | Ensures the output is relevant to the user's input or request. |
|  | **Sensitive** | Detects and blocks sensitive or inappropriate information in the output. |
|  | **Sentiment** | Analyzes and classifies the emotional tone (positive, negative, neutral) of the output. |
|  | **Toxicity** | Identifies and blocks harmful, offensive, or toxic language in the output. |
|  | **URLReachability** | Checks if URLs in the output are reachable (i.e., the link works). |
