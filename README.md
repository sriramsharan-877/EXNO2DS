# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
       
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
```

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

data = pd.read_csv("C:/Users/acer/Downloads/titanic_dataset.csv")

print("\nDataset Loaded Successfully\n")
print(data.head())
print("\nDataset Info:\n")
print(data.info())
print(data.describe())
```

<img width="758" height="763" alt="Screenshot 2026-05-13 184418" src="https://github.com/user-attachments/assets/ea9c75a0-1faf-45af-ab31-5e9a19602429" />
<img width="742" height="592" alt="Screenshot 2026-05-13 184432" src="https://github.com/user-attachments/assets/05d0be50-f2ca-44e7-ab93-93984aa31887" />



```
for column in data.columns:
    if data[column].dtype == 'object':
        data[column] = data[column].fillna(data[column].mode()[0])  
    else:
        data[column] = pd.to_numeric(data[column], errors='coerce')
        data[column] = data[column].fillna(data[column].median())
```
```
plt.figure(figsize=(6,4))
sns.boxplot(x=data["Age"])
plt.title("Boxplot - Age")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Fare"])
plt.title("Boxplot - Fare")
plt.show()
```



<img width="676" height="505" alt="Screenshot 2026-05-13 184444" src="https://github.com/user-attachments/assets/6fb5f681-c91c-4015-85f6-f1d6bbdc05f2" />
<img width="665" height="503" alt="Screenshot 2026-05-13 184454" src="https://github.com/user-attachments/assets/53bcac35-1d1a-4a3a-9b18-9630d10426d6" />




```
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

print("Outliers for Age:", remove_outliers_iqr(data, "Age").shape)
print("Outliers for Fare:", remove_outliers_iqr(data, "Fare").shape)

print("Outliers removed using IQR method.\n")
```


<img width="357" height="97" alt="Screenshot 2026-05-13 184501" src="https://github.com/user-attachments/assets/e567a933-a2a3-4ded-b3d6-b52e0ff5bf3f" />


```
plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=data)
plt.title("Countplot - Survival Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="SibSp", data=data)
plt.title("Countplot - Sibling/Spouse Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=data)
plt.title("Countplot - Passenger Class Distribution")
plt.show()
```


<img width="733" height="506" alt="Screenshot 2026-05-13 184511" src="https://github.com/user-attachments/assets/cca56524-0cd0-4256-bd6f-2a43af61ec84" />
<img width="698" height="497" alt="Screenshot 2026-05-13 184543" src="https://github.com/user-attachments/assets/f6683e91-054a-4fca-b306-9d2c57522dc4" />
<img width="695" height="493" alt="Screenshot 2026-05-13 184552" src="https://github.com/user-attachments/assets/eefbc28a-1990-4994-8ca6-e81cd48e62c3" />



```
sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()

sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()
```




<img width="785" height="566" alt="Screenshot 2026-05-13 184605" src="https://github.com/user-attachments/assets/b4c83fe1-7f3c-4d39-8102-3e00a083a405" />
<img width="725" height="497" alt="Screenshot 2026-05-13 184618" src="https://github.com/user-attachments/assets/9642b3ca-a506-419a-87df-2720055edcf7" />



```
print("\nCross Tabulation: SibSp vs Survived\n")
print(pd.crosstab(data["SibSp"], data["Survived"]))

print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))
```


<img width="437" height="427" alt="Screenshot 2026-05-13 184626" src="https://github.com/user-attachments/assets/3b3f82c1-e43a-46ca-aeb1-9a2afd51ab77" />



```
plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()
```



<img width="923" height="748" alt="Screenshot 2026-05-13 184637" src="https://github.com/user-attachments/assets/b353cdf4-1db2-4d2f-b96d-8892fce8dd59" />













# RESULT
The Program and The Output has been sucessfully Verified along with the Visualization.
