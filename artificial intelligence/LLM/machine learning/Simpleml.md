## Steps

- Create simple machine learning model
- Export the model in binary format
- load the model into the code

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
    

## Resources

- https://www.youtube.com/watch?v=7eh4d6sabA0
