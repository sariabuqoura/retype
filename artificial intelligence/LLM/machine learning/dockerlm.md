## Steps

- Create simple machine learning model
- Export the model in binary format
- load the model into the code
- Create Simple HTTP Get Web API and add Load model into it

## Install Packages

`pip install scikit-learn`

`pip install pandas`

## Download Data

We need to download the Music file 

`https://github.com/mosh-hamedani/python-supplementary-materials`

`https://github.com/mosh-hamedani/python-supplementary-materials/blob/main/music.csv`

# Codes for ML

## Step 1: ML Learning code

- Sample learning code
    
    ```python
    import pandas as pd
    from sklearn.tree import DecisionTreeClassifier 
    from sklearn.model_selection import train_test_split
    from sklearn.metrics import accuracy_score
    
    music_data = pd.read_csv('music.csv')
    X = music_data.drop(columns = ['genre'])
    y = music_data['genre']
    
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2)
    
    model = DecisionTreeClassifier()
    model.fit(X_train,y_train)
    predictions = model.predict(X_test)
    score = accuracy_score(y_test, predictions)
    print(score)
    
    ```
    

- Expected result
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/585431fa-2adb-46a3-a359-fe3fc8c38571/image.png)
    

---

## Step 2: Save the Model

- Export the model into joblib format
    
    ```python
    import pandas as pd
    from sklearn.tree import DecisionTreeClassifier 
    from sklearn import tree
    import joblib
    
    music_data = pd.read_csv('music.csv')
    X = music_data.drop(columns = ['genre'])
    y = music_data['genre']
    
    model = DecisionTreeClassifier()
    model.fit(X,y)
    
    joblib.dump(model,'music-recommender.joblob')
    ```
    

- Expected Result (New file will be created)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/caf68513-b655-4731-8dee-a7c36b54c3e0/image.png)
    

---

## Step3: Load the model

- Load the model into the code

```python
import joblib

model = joblib.load('music-recommender.joblob')

predictions = model.predict([[21,1]])
print(predictions)
```

- Expected result
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/f5a55410-c974-4114-8bf4-a27db384b358/image.png)
    
    ---
    

## Create Simple HTTP Get Method with load ML model

- Code
    
    ```python
    from fastapi import FastAPI, HTTPException
    import uvicorn
    import joblib
    app = FastAPI()
    
    @app.get("/chat")
    def char(number=20):
       
        model = joblib.load('music-recommender.joblob')
        predictions = model.predict([[number,1]])
    
        return {"predictions for the age: "+ number +"" :predictions[0]}
    
    if __name__ == "__main__":
    
        uvicorn.run(app, host="127.0.0.1", port=8080)
    ```
    

- Create Requirements file
    - File
        
        ```
        fastapi[all]==0.109.0
        uvicorn[standard]==0.27.0
        joblib==1.4.2
        scikit-learn==1.5.2
        
        ```
        
    - Noting that we don't any other library
- Create Docker file
    - File
        
        ```docker
        # For more information, please refer to https://aka.ms/vscode-docker-python
        FROM python:3-slim
        
        EXPOSE 8080
        
        # Keeps Python from generating .pyc files in the container
        ENV PYTHONDONTWRITEBYTECODE=1
        
        # Turns off buffering for easier container logging
        ENV PYTHONUNBUFFERED=1
        
        # Install pip requirements
        COPY requirements.txt .
        RUN python -m pip install -r requirements.txt
        
        WORKDIR /app
        COPY . /app
        
        # Creates a non-root user with an explicit UID and adds permission to access the /app folder
        # For more info, please refer to https://aka.ms/vscode-docker-python-configure-containers
        RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
        USER appuser
        
        # During debugging, this entry point will be overridden. For more information, please refer to https://aka.ms/vscode-docker-python-debug
        #CMD ["gunicorn", "--bind", "0.0.0.0:8080", "-k", "uvicorn.workers.UvicornWorker", "main:app"]
        CMD ["uvicorn","main:app","--host" ,"0.0.0.0", "--port","8080" ]
        ```
        
- Exclude files
    - Create `.dockerignore` file
        
        ```
        1_learn.py
        2_export.py
        3_load.py
        music.csv
        ```
        
- Noting excluding unneeded files from the production docker
- File tree
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/57541655-67d8-4ee6-a1e2-d36b8e845dba/image.png)
    

## Build the code and dockerfile into docker (Image)

- Command line
    - `docker build -t ml_docker:v1 .`
    - Expected result
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/96b37882-c792-4859-9b48-da5a6a25d907/image.png)
        
    - `docker images`
        - Expected result
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/7b29ba9f-1af8-4db5-b15a-09a858b67ea0/image.png)
            
    - `docker run -p 8080:8080 ml_docker:v1`
        - Expected result
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/fafd20f0-c87e-432b-b6bd-a6ceabe80607/image.png)
            

## Verify the Model response from the web browser

- `http://127.0.0.1:8080/chat?number=35`
- Expected result
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f957728d-52bc-414a-aad5-c7916a4193eb/0414bb62-5c24-495d-b7e9-7c02dcbcfa10/image.png)
    

## Resources

- https://hub.docker.com/repository/docker/sariabuqoura/ml_docker/general
- https://www.youtube.com/watch?v=7eh4d6sabA0
