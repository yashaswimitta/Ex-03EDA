# Ex-03EDA

## AIM
To perform EDA on the given data set. 

# Explanation
The primary aim with exploratory analysis is to examine the data for distribution, outliers and 
anomalies to direct specific testing of your hypothesis.
 

# ALGORITHM
### STEP 1
Import the required packages(pandas,numpy,seaborn).
### STEP 2
Read and Load the Dataset.
### STEP 3
Remove the null values from the data and remove the outliers.
### STEP 4
Remove the non numerical data columns using drop() method.
### STEP 5
returns object containing counts of unique values using (value_counts()).
### STEP 6
Plot the counts in the form of Histogram or Bar Graph.
### STEP 7
find the pairwise correlation of all columns in the dataframe(.corr()).
### STEP 8
Save the final data set into the file.
# CODE
```
Program 
Developed by:Yashaswi.Mitta
Register no:212221230062
'''
import pandas as pd
import numpy as np
import seaborn as sns
df=pd.read_csv("titanic_dataset.csv")
df

#removing data containing too many null values
df.isnull().sum()
df.drop('Cabin',axis=1,inplace=True)

#analysing dataframe contents
df.info()
df.isnull().sum()

#cleaning data
df['Age']=df['Age'].fillna(df['Age'].median())
df['Embarked']=df['Embarked'].fillna(df['Embarked'].mode()[0])
df.isnull().sum()

#data is cleaned, checking for outliers
df.boxplot()
#removing outliers
cols = ['Age', 'Fare','SibSp','Parch','Fare']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
df
df.boxplot()

#maximum outliers removed
# performing data analysis
#statistical analysis for single data group
df['Survived'].value_counts()
df['Pclass'].value_counts()
df['SibSp'].value_counts()
df['Embarked'].value_counts()
df['Sex'].value_counts()

#statistical analysis for two data groups
pd.crosstab(df["Pclass"],df["Survived"])
pd.crosstab(df["Sex"],df["Survived"])
pd.crosstab(df["Embarked"],df["Survived"])
pd.crosstab(df["SibSp"],df["Survived"])

#graphical analysis of categorical data--univariate
sns.countplot(x="Survived",data=df)
sns.countplot(x="Pclass",data=df)
sns.countplot(x="SibSp",data=df)
sns.countplot(x="Embarked",data=df)
sns.countplot(x="Sex",data=df)

#graphical analysis of non-categorical data or data with multiple categories--univariate
sns.displot(df["Fare"])
sns.displot(df["Age"])

#graphical analysis of categorical data--bivariate
sns.countplot(x="Sex",hue="Survived",data=df)
sns.countplot(x='Pclass',hue='Survived',data=df)
sns.countplot(x='Embarked',hue='Survived',data=df)

#graphical analysis of non-categorical data or data with multiple categories--bivariate
sns.displot(df[df["Survived"]==0]["Age"])
sns.displot(df[df["Survived"]==1]["Age"])

#Graphical representation of data--multivariate 
df.drop('Parch',axis=1,inplace=True)
sns.heatmap(df.corr(),annot=True)

#analysing pairwise correlation of columns in dataset
df.corr()
```

# OUPUT
# 0RIGINAL DATA
![image](https://user-images.githubusercontent.com/94619247/162871882-0084a345-3132-40c9-a353-9c71bc2fb29d.png)
# Data after removing values with multiple null entries
![image](https://user-images.githubusercontent.com/94619247/162872194-3fcbe9ea-fdce-4a14-8ce2-154edabd9ce9.png)
![image](https://user-images.githubusercontent.com/94619247/162872222-3a5bec6b-f457-4f82-a528-87799c816847.png)
![image](https://user-images.githubusercontent.com/94619247/162872287-c6dabbda-1da9-4940-b284-52bcdb65c4ed.png)
# Data Cleaning Process
![image](https://user-images.githubusercontent.com/94619247/162872340-9cab26a5-ff64-4625-a7b8-ebdd0c2c2177.png)
# Removing Outliers Process
![image](https://user-images.githubusercontent.com/94619247/162872432-0c8245f1-88f4-492a-b61c-4c02849dd12c.png)
![image](https://user-images.githubusercontent.com/94619247/162872448-1a6e9052-abed-41d5-b0df-f61730f75884.png)
![image](https://user-images.githubusercontent.com/94619247/162872475-f314f7ad-09c3-4769-be8d-dde27d11ff02.png)
# performing data analysis
# statistical analysis for single data group
![image](https://user-images.githubusercontent.com/94619247/162872636-49a8b361-e99d-4f3c-8a8a-65d0549904eb.png)
![image](https://user-images.githubusercontent.com/94619247/162872680-6ee358a3-d636-4e2e-8efe-921740d4034f.png)
![image](https://user-images.githubusercontent.com/94619247/162872756-7d1ea5a9-d1c4-431e-8dbb-fcfc76de9a03.png)
![image](https://user-images.githubusercontent.com/94619247/162872788-930974fb-7266-4bc7-bb0f-b2b2fe1298a2.png)
![image](https://user-images.githubusercontent.com/94619247/162872809-0aba9971-7e73-470d-ac09-e408ea9e9ddd.png)
# statistical analysis for two data groups
![image](https://user-images.githubusercontent.com/94619247/162872886-78a20574-8cb6-4eb3-8753-8069571ed1db.png)
![image](https://user-images.githubusercontent.com/94619247/162872917-6929ca6e-82e3-42dd-b0c3-b59af70e9b09.png)
![image](https://user-images.githubusercontent.com/94619247/162872940-094c78e5-dbbd-49a6-b97c-cb6eeb7dd18a.png)
![image](https://user-images.githubusercontent.com/94619247/162872960-a6310345-2ffd-4b0d-9a53-48d84fac7f8a.png)
# graphical analysis of categorical data--univariate
![image](https://user-images.githubusercontent.com/94619247/162873035-b147317d-48c1-4085-8225-6137d69ae1f3.png)
![image](https://user-images.githubusercontent.com/94619247/162873060-14a40a21-2703-4a52-90d5-365fa2cba595.png)
![image](https://user-images.githubusercontent.com/94619247/162873083-d60a5add-b8c2-4684-a884-9697ff9f467e.png)
![image](https://user-images.githubusercontent.com/94619247/162873123-8e9a2967-c923-4553-97e2-cba372b35939.png)
![image](https://user-images.githubusercontent.com/94619247/162873154-31cc239b-3009-49d1-9cc0-71522c5e744f.png)
# graphical analysis of non-categorical data or data with multiple categories--univariate
![image](https://user-images.githubusercontent.com/94619247/162876087-14a58ba1-654f-41e8-88db-bca6458de833.png)
![image](https://user-images.githubusercontent.com/94619247/162876100-9cdd9d76-5d3b-4149-82fe-826f76971f93.png)
# graphical analysis of categorical data--bivariate
![image](https://user-images.githubusercontent.com/94619247/162876200-2dd2ecf0-a5b8-44fa-8bea-3248354d65a7.png)
![image](https://user-images.githubusercontent.com/94619247/162876220-7248603f-9248-4813-95f4-8c69efc95aaf.png)
![image](https://user-images.githubusercontent.com/94619247/162876242-24251ee5-7423-4f7e-8d8d-57cffe3b2759.png)
# graphical analysis of non-categorical data or data with multiple categories--bivariate
![image](https://user-images.githubusercontent.com/94619247/162876303-9d40cd14-911d-4499-9804-e20c4f1fec86.png)
![image](https://user-images.githubusercontent.com/94619247/162876322-c9a3d931-3a1e-432c-9c05-8f3382d2ea35.png)
# graphical representation of data--multivariate
![image](https://user-images.githubusercontent.com/94619247/162876402-3cda5da1-d9f4-46e4-92a3-fb34d70bafe7.png)
# pairwise correlation of columns in dataset
![image](https://user-images.githubusercontent.com/94619247/162876461-1d362104-ffc2-4ff7-b025-897ffef110e1.png)
# RESULT
The data has been cleaned, outlier has been removed and the EDA on the given data has been performed.


