- Tokenizer Code
    
    ```python
    from transformers import AutoTokenizer
    
    tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
    
    inputs = tokenizer("a", return_tensors="pt")
    
    print(inputs)
    
    ```
    

- Output
    
    ```python
    {
    'input_ids': tensor([[ 101, 1037,  102]]), 
    'token_type_ids': tensor([[0, 0, 0]]),
    'attention_mask': tensor([[1, 1, 1]])
     }
    ```
