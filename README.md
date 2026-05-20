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
<img width="777" height="782" alt="Screenshot 2026-05-20 132210" src="https://github.com/user-attachments/assets/a50b6170-a5a0-420e-80e0-df6aff74ddc1" />
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
<img width="667" height="505" alt="Screenshot 2026-05-20 132700" src="https://github.com/user-attachments/assets/a2cc44e5-1d8b-4e01-8889-aa3d7526fb59" />
<img width="687" height="512" alt="Screenshot 2026-05-20 132649" src="https://github.com/user-attachments/assets/f7333b79-7809-41fe-acd7-59a693ee07ab" />
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
<img width="362" height="90" alt="Screenshot 2026-05-20 132822" src="https://github.com/user-attachments/assets/86913152-7080-4bfc-8819-3b9d6a7248cc" />
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
<img width="707" height="500" alt="Screenshot 2026-05-20 133002" src="https://github.com/user-attachments/assets/08238382-4b05-4a28-94e4-c4812e7dfed0" />
<img width="712" height="501" alt="Screenshot 2026-05-20 132947" src="https://github.com/user-attachments/assets/352864d3-d07c-41a3-a702-2a84f159bbce" />
```
sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()

sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()
```
<img width="740" height="505" alt="Screenshot 2026-05-20 133319" src="https://github.com/user-attachments/assets/ea3db838-c0a7-475d-8713-865c60aecda4" />
<img width="791" height="578" alt="Screenshot 2026-05-20 133251" src="https://github.com/user-attachments/assets/a303df1e-c678-4294-91dd-f7c13722d427" />
```
print("\nCross Tabulation: SibSp vs Survived\n")
print(pd.crosstab(data["SibSp"], data["Survived"]))

print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))
```
<img width="437" height="427" alt="Screenshot 2026-05-20 133442" src="https://github.com/user-attachments/assets/51a0e8d2-01c6-4af9-8847-7c8f897fc8fc" />
```
plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()
```
<img width="851" height="696" alt="Screenshot 2026-05-20 133604" src="https://github.com/user-attachments/assets/8bd00265-209d-4ccf-8d51-3a78917bf865" />














# RESULT
The Program and The Output has been sucessfully Verified along with the Visualization.
