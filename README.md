# Exno:1
Data Cleaning Process

## Name: K KESAVA SAI
## Register Number: 212223230105

# AIM:
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation:
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm:
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

## Coding and Output:
# Cleaning process:
```py
import pandas as pd
data={'Name':['Alice','Bob','Charlie','Dave','Eve'],'Age':[25,32,None,41,28],'Salary':[50000,None,70000,90000,60000]}
df=pd.DataFrame(data)
df
```
## Output:
![image](https://github.com/user-attachments/assets/37ae9ec8-f65f-455d-b0f8-6d68b3c0526f)
## remove the missing value in the salary with the particular row:
```py
df_clean=df.dropna(subset=['Salary'])
df_clean
```
## Output:
![image](https://github.com/user-attachments/assets/2b53fd56-b00f-41ca-ac05-92f9524c2bf7)
## the row with complete missing value then the row get deleted:
```py
df_clean_all=df.dropna(how='all')
df_clean_all
```
## Output:
![image](https://github.com/user-attachments/assets/1a885ac7-1487-4ec2-8eae-002fb4ce9fee)
## delete the row which contain one missing value:
```py
df_cleaned_any=df.dropna(how='any')
df_cleaned_any
```
## Output:
![image](https://github.com/user-attachments/assets/5248d88d-5bc2-4091-aa5a-538bad9fd026)

```py
import pandas as pd
import numpy as np
data={'Name':['Alice','Bob','Charlie','Dave','Eve','Bob','Charlie'],'Age':[25,np.nan,35,41,np.nan,np.nan,85],'Salary':[50000,np.nan,70000,np.nan,60000,np.nan,70000]}
df=pd.DataFrame(data)
df
```
## Output:
![image](https://github.com/user-attachments/assets/7cd22527-4667-400c-b4f0-d4bc20f159f1)

```py
~df.duplicated()
```
## Output:
![image](https://github.com/user-attachments/assets/d564c8e8-3eb7-42da-8713-4d0a29fb9286)

```py
df_clean=df.dropna(how='any')
df_clean
```
## Output:
![image](https://github.com/user-attachments/assets/cc990bb0-e59a-41f8-a40a-605b571f298a)

```py
df_filled=df.fillna(0)
df_filled
```
## Output:
![image](https://github.com/user-attachments/assets/f74065fa-fd82-44f2-a2c0-5bd481865a11)

## forward fill where it will fill the before data set:
```py
df_ffill=df.fillna(method='ffill')
df_ffill
```
## Output:
![image](https://github.com/user-attachments/assets/132f1053-f3d3-4c31-bd93-15132d167b44)
## where it will fill the back ward data into the current data:
```py
df_bfill=df.bfill()
df_bfill
```
## Output:
![image](https://github.com/user-attachments/assets/ce0d2f47-efb1-49f8-b6c4-bcf3c37f8c90)
## to find the mean of an age:
```py
df_mean=df.fillna(df['Age'].mean())
df_mean
```
## Output:
![image](https://github.com/user-attachments/assets/c2c8d83a-ebec-458c-be47-a0b1fb0b095b)

# Outlier detection and removal process:
```py
import pandas as pd
import seaborn as sns
import numpy as np
df=pd.read_csv('iris.csv')
df
```
## Output:
![image](https://github.com/user-attachments/assets/a4cac69f-596b-4d0e-bf53-9222f7a6b837)

```py
sns.boxplot(data=df['sepal_width'])
```
## Output:
![image](https://github.com/user-attachments/assets/30f34619-55d1-45bc-8f42-046a54a6575c)

```py
sns.boxenplot(data=df['sepal_width'])
```
## Output:
![image](https://github.com/user-attachments/assets/1fd6777b-f4eb-44c0-8976-546b31c3e61b)

```py
q1=df['sepal_width'].quantile(0.25)
q3=df['sepal_width'].quantile(0.75)
IQR=q3-q1
IQR
```
## Output:
![image](https://github.com/user-attachments/assets/67edfd9b-dfb2-4327-b151-de5158f69237)
```py
lower_bound=q1-1.5*IQR
upper_bound=q3+1.5*IQR
print(lower_bound,upper_bound)
```
## Output:
![image](https://github.com/user-attachments/assets/776934e8-6e8f-44e3-a318-18767cf49325)
```py
print("Q1:",q1)
print("Q3:",q3)
print("IQR:",IQR)
print("Lower Bound:",lower_bound)
print("Upper_bound:",upper_bound)
```
## Output:
![image](https://github.com/user-attachments/assets/b320c7c5-320b-4724-a8cb-9cba099a136a)
```py![image](https://github.com/user-attachments/assets/194b6ee2-2b59-4008-8e47-442234f33374)

dt=df[(df['sepal_width']>=lower_bound) & (df['sepal_width']<=upper_bound)]
dt
```
## Output:
![image](https://github.com/user-attachments/assets/be83cc78-8039-4890-97b3-952b57284e10)
```py
dt['sepal_width'].dropna()
```
## Output:
![image](https://github.com/user-attachments/assets/d17c8d68-4af3-4e70-a92e-60ff87c8a3bd)
```py
sns.boxplot(data=dt['sepal_width'])
```
## Output:
![image](https://github.com/user-attachments/assets/3fd2ec01-58a8-44b0-86ef-f692625ca064)
```py
sns.boxenplot(data=dt['sepal_width'])
```
## Output:
![image](https://github.com/user-attachments/assets/a7e1aae1-2f2b-4226-b069-818a88564e7b)
```py
sns.scatterplot(data=dt['sepal_width'])
```
## Output:
![image](https://github.com/user-attachments/assets/921a237b-69e1-4a13-97f3-cd2e7cf642b8)
# Result
Hence,The data cleaning process and the outlier detection and removal of it has been done successfully.
