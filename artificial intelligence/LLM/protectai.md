## Online Protect AI Scanner

- Search for the name of the model before downloading
    - [https://protectai.com/insights](https://protectai.com/insights/models)

## Protect AI Scanner CLI

https://protectai.com/

https://github.com/protectai/modelscan

https://github.com/protectai/modelscan/blob/main/docs/attack-1.png

**What Models and Frameworks Are Supported?**

https://github.com/protectai/modelscan?tab=readme-ov-file#what-models-and-frameworks-are-supported

This will be expanding continually, so look out for changes in our release notes.

At present, ModelScan supports any Pickle derived format and many others:

| ML Library | API | Serialization Format | modelscan support |
| --- | --- | --- | --- |
| Pytorch | [torch.save() and torch.load()](https://pytorch.org/tutorials/beginner/saving_loading_models.html) | Pickle | Yes |
| Tensorflow | [tf.saved_model.save()](https://www.tensorflow.org/guide/saved_model) | Protocol Buffer | Yes |
| Keras | [keras.models.save(save_format= 'h5')](https://www.tensorflow.org/guide/keras/serialization_and_saving) | HD5 (Hierarchical Data Format) | Yes |
|  | [keras.models.save(save_format= 'keras')](https://www.tensorflow.org/guide/keras/serialization_and_saving) | Keras V3 (Hierarchical Data Format) | Yes |
| Classic ML Libraries (Sklearn, XGBoost etc.) | pickle.dump(), dill.dump(), joblib.dump(), cloudpickle.dump() | Pickle, Cloudpickle, Dill, Joblib | Yes |

---

## Command line

- First download the file to scan locally, you cant scan it on online repo
    - Harmless model
        - https://huggingface.co/ykilcher/totally-harmless-model/blob/main/pytorch_model.bin
- Commands
    
    `pip install modelscan`
    
    `modelscan -p /path/to/model_file.pkl`
    
- Expected Result
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/b5fd7bf7-b9a1-4e51-953d-f274f78d50d0/image.png)
    

## For later

https://github.com/protectai#protect-ai-oss

| Project | Description |
| --- | --- |
| [**ModelScan**](https://github.com/protectai/modelscan) | 🔍 ML Model Security Scanner |
| [**AI Exploits**](https://github.com/protectai/ai-exploits) | 🗡️ Collection of AI/ML Exploits |
| [**LLM Guard**](https://github.com/protectai/llm-guard) | 🛡️ Security Toolkit for LLM Interactions |
| [**rebuff**](https://github.com/protectai/rebuff) | 💉 LLM Prompt Injection Attack Detection |
| [**NB Defense**](https://github.com/protectai/nbdefense) | 📓 Jupyter Notebooks Security |
| [**Vulnhuntr**](https://github.com/protectai/vulnhuntr) | 🏹 Autonomous AI-Discovered 0Day Tool |
