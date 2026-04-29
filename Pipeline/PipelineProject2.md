```python
!pip install pymongo
```

    Requirement already satisfied: pymongo in /usr/local/lib/python3.12/dist-packages (4.17.0)
    Requirement already satisfied: dnspython<3.0.0,>=2.6.1 in /usr/local/lib/python3.12/dist-packages (from pymongo) (2.8.0)





```python
!pip install pymongo python-dotenv scikit-learn
```

    Requirement already satisfied: pymongo in /usr/local/lib/python3.12/dist-packages (4.17.0)
    Requirement already satisfied: python-dotenv in /usr/local/lib/python3.12/dist-packages (1.2.2)
    Requirement already satisfied: scikit-learn in /usr/local/lib/python3.12/dist-packages (1.6.1)
    Requirement already satisfied: dnspython<3.0.0,>=2.6.1 in /usr/local/lib/python3.12/dist-packages (from pymongo) (2.8.0)
    Requirement already satisfied: numpy>=1.19.5 in /usr/local/lib/python3.12/dist-packages (from scikit-learn) (2.0.2)
    Requirement already satisfied: scipy>=1.6.0 in /usr/local/lib/python3.12/dist-packages (from scikit-learn) (1.16.3)
    Requirement already satisfied: joblib>=1.2.0 in /usr/local/lib/python3.12/dist-packages (from scikit-learn) (1.5.3)
    Requirement already satisfied: threadpoolctl>=3.1.0 in /usr/local/lib/python3.12/dist-packages (from scikit-learn) (3.6.0)



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from pymongo import MongoClient
from urllib.parse import quote_plus
import os

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report
```


```python

```


```python
os.environ["MONGO_USERNAME"] = "mpcotheremail"
os.environ["MONGO_PASSWORD"] = "Beluga10"
```

### Get data


```python
from pymongo import MongoClient
from urllib.parse import quote_plus
import os

# Get credentials from environment variables
username = os.getenv("MONGO_USERNAME")
password = os.getenv("MONGO_PASSWORD")

# Safety check
if username is None or password is None:
    raise ValueError("Please set MONGO_USERNAME and MONGO_PASSWORD environment variables.")

password = quote_plus(password)

connection_string = f"mongodb+srv://{username}:{password}@cluster0.4pqvr.mongodb.net/?retryWrites=true&w=majority"

client = MongoClient(connection_string)

db = client["diabetes_db_v2"]
collection = db["encounters"]

print(collection.count_documents({}))
```

    10000



```python
data = list(collection.find())
df = pd.DataFrame(data)

# Drop MongoDB id
df.drop(columns=["_id"], inplace=True)

print("Shape:", df.shape)
df.head()
```

    Shape: (10000, 39)






  <div id="df-80610bc4-7997-40d1-9249-e83203f4b2e4" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num_medications</th>
      <th>change</th>
      <th>diabetesMed</th>
      <th>metformin</th>
      <th>repaglinide</th>
      <th>nateglinide</th>
      <th>chlorpropamide</th>
      <th>glimepiride</th>
      <th>acetohexamide</th>
      <th>glipizide</th>
      <th>...</th>
      <th>readmitted</th>
      <th>age</th>
      <th>gender</th>
      <th>race</th>
      <th>time_in_hospital</th>
      <th>number_diagnoses</th>
      <th>number_inpatient</th>
      <th>number_emergency</th>
      <th>A1Cresult</th>
      <th>max_glu_serum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>[50-60)</td>
      <td>1.0</td>
      <td>Caucasian</td>
      <td>1</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>[70-80)</td>
      <td>0.0</td>
      <td>Caucasian</td>
      <td>11</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>32</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>[50-60)</td>
      <td>1.0</td>
      <td>Caucasian</td>
      <td>8</td>
      <td>6</td>
      <td>2</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>[60-70)</td>
      <td>1.0</td>
      <td>AfricanAmerican</td>
      <td>8</td>
      <td>8</td>
      <td>1</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>[80-90)</td>
      <td>0.0</td>
      <td>Caucasian</td>
      <td>6</td>
      <td>9</td>
      <td>2</td>
      <td>0</td>
      <td>&gt;7</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 39 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-80610bc4-7997-40d1-9249-e83203f4b2e4')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-80610bc4-7997-40d1-9249-e83203f4b2e4 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-80610bc4-7997-40d1-9249-e83203f4b2e4');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




### Feature engineering


```python
# Drop high-missing lab variables
df = df.drop(columns=["A1Cresult", "max_glu_serum"])

# Encode race (handle missing just in case)
df['race'] = df['race'].fillna("Unknown")
df['race'] = df['race'].astype('category').cat.codes

# Convert age bins → numeric (take lower bound of range)
df['age'] = df['age'].str.extract('(\d+)')[0].astype(float)

# Drop any remaining missing values (should be minimal now)
df = df.dropna()

print("Final shape:", df.shape)
```

    Final shape: (9999, 37)


    <>:9: SyntaxWarning: invalid escape sequence '\d'
    <>:9: SyntaxWarning: invalid escape sequence '\d'
    /tmp/ipykernel_24408/873073752.py:9: SyntaxWarning: invalid escape sequence '\d'
      df['age'] = df['age'].str.extract('(\d+)')[0].astype(float)



```python
df.isnull().sum().sort_values(ascending=False).head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>num_medications</th>
      <td>0</td>
    </tr>
    <tr>
      <th>change</th>
      <td>0</td>
    </tr>
    <tr>
      <th>diabetesMed</th>
      <td>0</td>
    </tr>
    <tr>
      <th>metformin</th>
      <td>0</td>
    </tr>
    <tr>
      <th>repaglinide</th>
      <td>0</td>
    </tr>
    <tr>
      <th>nateglinide</th>
      <td>0</td>
    </tr>
    <tr>
      <th>chlorpropamide</th>
      <td>0</td>
    </tr>
    <tr>
      <th>glimepiride</th>
      <td>0</td>
    </tr>
    <tr>
      <th>acetohexamide</th>
      <td>0</td>
    </tr>
    <tr>
      <th>glipizide</th>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> int64</label>






```python
print([col for col in df.columns if col not in [
    'readmitted','age','gender','race',
    'time_in_hospital','number_diagnoses',
    'number_inpatient','number_emergency',
    'treatment_complexity'
]])
```

    ['num_medications', 'change', 'diabetesMed', 'metformin', 'repaglinide', 'nateglinide', 'chlorpropamide', 'glimepiride', 'acetohexamide', 'glipizide', 'glyburide', 'tolbutamide', 'pioglitazone', 'rosiglitazone', 'acarbose', 'miglitol', 'troglitazone', 'tolazamide', 'examide', 'citoglipton', 'insulin', 'glyburide-metformin', 'glipizide-metformin', 'glimepiride-pioglitazone', 'metformin-rosiglitazone', 'metformin-pioglitazone', 'num_active_meds', 'med_change_flag']


### Modeling


```python
y = df['readmitted']
```


```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report

X1 = df[['treatment_complexity']]
y = df['readmitted']

X_train, X_test, y_train, y_test = train_test_split(
    X1, y, test_size=0.2, random_state=42
)

model1 = LogisticRegression(max_iter=1000, class_weight='balanced')  # ⭐ FIX
model1.fit(X_train, y_train)

y_pred1 = model1.predict(X_test)

print("MODEL 1: Treatment Complexity Only")
print("Accuracy:", accuracy_score(y_test, y_pred1))
print(classification_report(y_test, y_pred1))
```

    MODEL 1: Treatment Complexity Only
    Accuracy: 0.528
                  precision    recall  f1-score   support
    
               0       0.89      0.53      0.67      1773
               1       0.12      0.48      0.19       227
    
        accuracy                           0.53      2000
       macro avg       0.50      0.51      0.43      2000
    weighted avg       0.80      0.53      0.61      2000
    



```python
X2 = df[
    ['treatment_complexity',
     'age','gender','race',
     'time_in_hospital',
     'number_diagnoses',
     'number_inpatient',
     'number_emergency']
]

X_train, X_test, y_train, y_test = train_test_split(
    X2, y, test_size=0.2, random_state=42
)

model2 = LogisticRegression(max_iter=1000, class_weight='balanced')  # ⭐ FIX
model2.fit(X_train, y_train)

y_pred2 = model2.predict(X_test)

print("\nMODEL 2: With Controls")
print("Accuracy:", accuracy_score(y_test, y_pred2))
print(classification_report(y_test, y_pred2))
```

    
    MODEL 2: With Controls
    Accuracy: 0.659
                  precision    recall  f1-score   support
    
               0       0.91      0.69      0.78      1773
               1       0.15      0.45      0.23       227
    
        accuracy                           0.66      2000
       macro avg       0.53      0.57      0.51      2000
    weighted avg       0.82      0.66      0.72      2000
    



```python
med_columns = [
'metformin','repaglinide','nateglinide','chlorpropamide','glimepiride',
'acetohexamide','glipizide','glyburide','tolbutamide','pioglitazone',
'rosiglitazone','acarbose','miglitol','troglitazone','tolazamide',
'examide','citoglipton','insulin','glyburide-metformin',
'glipizide-metformin','glimepiride-pioglitazone',
'metformin-rosiglitazone','metformin-pioglitazone'
]

X3 = df[
    ['treatment_complexity',
     'age','gender','race',
     'time_in_hospital',
     'number_diagnoses',
     'number_inpatient',
     'number_emergency']
    + med_columns
]

X_train, X_test, y_train, y_test = train_test_split(
    X3, y, test_size=0.2, random_state=42
)

model3 = LogisticRegression(max_iter=1000, class_weight='balanced')
model3.fit(X_train, y_train)

y_pred3 = model3.predict(X_test)

print("\nMODEL 3: With Controls + Medications")
print("Accuracy:", accuracy_score(y_test, y_pred3))
print(classification_report(y_test, y_pred3))
```

    
    MODEL 3: With Controls + Medications
    Accuracy: 0.6535
                  precision    recall  f1-score   support
    
               0       0.91      0.67      0.77      1773
               1       0.16      0.50      0.25       227
    
        accuracy                           0.65      2000
       macro avg       0.54      0.59      0.51      2000
    weighted avg       0.83      0.65      0.72      2000
    


### Visualizations


```python
coeffs.sort_values(by="Coefficient", ascending=False).head(10)
```





  <div id="df-e660af04-3617-4603-b52b-956b2ebcec68" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Feature</th>
      <th>Coefficient</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>number_inpatient</td>
      <td>0.283391</td>
    </tr>
    <tr>
      <th>5</th>
      <td>number_diagnoses</td>
      <td>0.045393</td>
    </tr>
    <tr>
      <th>0</th>
      <td>treatment_complexity</td>
      <td>0.044329</td>
    </tr>
    <tr>
      <th>4</th>
      <td>time_in_hospital</td>
      <td>0.018356</td>
    </tr>
    <tr>
      <th>1</th>
      <td>age</td>
      <td>0.006288</td>
    </tr>
    <tr>
      <th>7</th>
      <td>number_emergency</td>
      <td>0.001610</td>
    </tr>
    <tr>
      <th>3</th>
      <td>race</td>
      <td>-0.041071</td>
    </tr>
    <tr>
      <th>2</th>
      <td>gender</td>
      <td>-0.092877</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-e660af04-3617-4603-b52b-956b2ebcec68')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-e660af04-3617-4603-b52b-956b2ebcec68 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-e660af04-3617-4603-b52b-956b2ebcec68');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>





```python
df.groupby('treatment_complexity')['readmitted'].mean().plot(kind='bar')

plt.title("Readmission Rate by Treatment Complexity")
plt.xlabel("Treatment Complexity")
plt.ylabel("Readmission Rate")
plt.show()
```


    
![png](PipelineProject2_files/PipelineProject2_21_0.png)
    



```python
df['complexity_group'] = df['treatment_complexity'].apply(
    lambda x: '3+' if x >= 3 else str(int(x))
)
```


```python
df.groupby('complexity_group')['readmitted'].mean().plot(kind='bar')

plt.title("Readmission Rate by Treatment Complexity (Grouped)")
plt.xlabel("Treatment Complexity")
plt.ylabel("Readmission Rate")
plt.show()
```


    
![png](PipelineProject2_files/PipelineProject2_23_0.png)
    



```python
import matplotlib.pyplot as plt

top_features = coeffs.head(10)

plt.figure()
plt.barh(top_features["Feature"], top_features["Coefficient"])
plt.title("Top Predictors of Readmission")
plt.xlabel("Logistic Regression Coefficient")
plt.gca().invert_yaxis()
plt.show()
```


    
![png](PipelineProject2_files/PipelineProject2_24_0.png)
    



```python
# Predicted probabilities from Model 3
probs = model3.predict_proba(X_test)[:,1]

temp_df = X_test.copy()
temp_df['prob'] = probs

temp_df.groupby('treatment_complexity')['prob'].mean().plot(marker='o')

plt.title("Predicted Readmission Risk vs Treatment Complexity")
plt.xlabel("Treatment Complexity")
plt.ylabel("Predicted Probability")
plt.show()
```


    
![png](PipelineProject2_files/PipelineProject2_25_0.png)
    



```python
from sklearn.metrics import ConfusionMatrixDisplay

ConfusionMatrixDisplay.from_estimator(model3, X_test, y_test)
plt.title("Confusion Matrix (Model 3)")
plt.show()
```


    
![png](PipelineProject2_files/PipelineProject2_26_0.png)
    


### Analysis Rationale

The goal of this analysis is to evaluate whether treatment complexity is associated with hospital readmission risk among diabetic patients.

Logistic regression was selected as the modeling approach because the outcome variable (readmitted) is binary and the model provides interpretable coefficients that allow for direct assessment of how each feature influences readmission probability.

A stepwise modeling strategy was used to isolate the effect of treatment complexity:

- Model 1 includes only treatment complexity to assess its standalone relationship with readmission.
- Model 2 adds demographic and clinical control variables (such as age, time in hospital, and prior inpatient visits) to account for underlying patient severity.
- Model 3 further incorporates individual medication indicators to capture more granular treatment information.

This progression allows for evaluation of whether treatment complexity remains significant after accounting for potential confounding factors.

Class imbalance in the readmission variable was addressed using class_weight='balanced', ensuring that the model does not default to predicting the majority class and can better identify high-risk patients.

In addition to modeling, visualization techniques were used to support interpretation. Treatment complexity was grouped (0, 1, 2, 3+) to reduce noise from sparse observations at higher levels and provide a clearer view of trends in readmission rates.

Overall, this approach prioritizes interpretability and structured comparison across models to understand the role of treatment complexity relative to other clinical factors.

### Visualization Rationale

Visualizations were used to support interpretation of the relationship between treatment complexity and hospital readmission risk, as well as to illustrate model behavior.

A grouped bar chart of readmission rates by treatment complexity (0, 1, 2, 3+) was used to clearly display trends while reducing noise from sparse observations at higher complexity levels. Grouping improves interpretability and prevents small sample sizes from distorting the pattern.

A coefficient plot from the logistic regression model was used to compare the relative importance of predictors. This allows for direct visualization of how treatment complexity compares to other clinical variables, such as prior inpatient visits.

A confusion matrix was included to evaluate model performance, specifically showing the tradeoff between correctly identifying readmitted patients and the rate of false positives.

Additionally, a plot of predicted readmission probability versus treatment complexity was used to illustrate how the model translates complexity into risk. This provides a more intuitive understanding of model outputs beyond raw coefficients.

Together, these visualizations provide both descriptive and model-based perspectives, reinforcing the conclusion that treatment complexity is associated with readmission risk while highlighting the stronger influence of clinical severity factors.
