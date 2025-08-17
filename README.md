# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

## Data Cleaning Process
```
import pandas as pd
df = pd.read_csv("Data_set.csv")
df
```

![alt text](image.png)

```
print(df.shape)
df.info()
```

![alt text](image-1.png)

```
df.isnull()
```

![alt text](image-2.png)

```
df.notnull()
```

![alt text](image-3.png)

```
df.dropna(axis=0) 
```

![alt text](image-4.png) 

```
df.dropna(axis=1)
```

![alt text](image-5.png) 

```
df.iloc[:3]
df.iloc[1:3]
df.iloc[1:3,1:3]
df.iloc[[1,2,3],[1,2,3]]
```

![alt text](image-6.png) 

```
df.dropna(subset=['show_name'])
```

![alt text](image-7.png) 

```
df.fillna(0)
```

![alt text](image-8.png)

```
df.fillna(df['rating'].mean())
```

![alt text](image-9.png) 

```
df.fillna(method='ffill')
```

![alt text](image-10.png) 

```
df.fillna(method='bfill')
```

![alt text](image-11.png) 

```
df.interpolate()
```

![alt text](image-12.png)  

## Outlier Detection & Removal

```
import pandas as pd
df = pd.read_csv("heights.csv")
df
```

<img width="213" height="683" alt="image" src="https://github.com/user-attachments/assets/6268ba37-fd7d-471d-a024-c34863dd905f" />

```
import seaborn as sns
sns.boxplot(data=df)
```

<img width="824" height="620" alt="image" src="https://github.com/user-attachments/assets/2090aeb3-a088-4da1-b653-4d9ec0d30e4b" />

```
sns.scatterplot(data=df)
```

<img width="826" height="649" alt="image" src="https://github.com/user-attachments/assets/94f059ac-c116-431c-9f2f-a6754ffb669b" />

```
max = df['height'].quantile(0.75)
min = df['height'].quantile(0.25)
iqr = max - min
print(iqr)
```

<img width="458" height="172" alt="image" src="https://github.com/user-attachments/assets/6706172f-f889-4bba-a0ee-366e2bb8b645" />

```
lb = min - 1.5 * iqr
ub = max + 1.5 * iqr
outliers = df[(df['height']<lb)|(df['height']>ub)]
print("Lower bound = ",lb)
print("Upper bound = ",ub)
print("Outliers: ",outliers)
```

<img width="595" height="340" alt="image" src="https://github.com/user-attachments/assets/0e6443a5-b813-41df-aeb4-a5d8cbf8b7b6" />

```
no_outliers = df[~((df['height']<lb)|(df['height']>ub))]
no_outliers
```

<img width="673" height="713" alt="image" src="https://github.com/user-attachments/assets/0ab8af17-7e8d-40d6-8681-4fd068e62cdb" />

```
sns.boxplot(data=no_outliers)
```

<img width="822" height="670" alt="image" src="https://github.com/user-attachments/assets/8636f7c2-e730-45d8-91a4-a293186ed9ef" />

```
sns.scatterplot(data=no_outliers)
```

<img width="787" height="692" alt="image" src="https://github.com/user-attachments/assets/faeca148-8c75-42f9-bb19-407f3e2f0062" />

```
import matplotlib.pyplot as plt
df
```

<img width="490" height="740" alt="image" src="https://github.com/user-attachments/assets/15cec454-28b7-4213-ac64-f3d87b68b7de" />

```
max = df['height'].quantile(0.75)
q2 = df['height'].quantile(0.5)
min = df['height'].quantile(0.25)
iqr = max - min
lb = min - 1.5 * iqr
ub = max + 1.5 * iqr
dfs = df[(df['height']>=lb)&(df['height']<=ub)]
dfs
```

<img width="524" height="792" alt="image" src="https://github.com/user-attachments/assets/42456aa6-1317-4b2e-973f-74edd6a8c0f9" />

```
import numpy as np
from scipy import stats
z = np.abs(stats.zscore(df['height']))
print(z)
```

<img width="755" height="187" alt="image" src="https://github.com/user-attachments/assets/2a109653-80ae-441a-81b2-9c06a7b4d768" />

```
df1 = df[z<3]
df1
```

<img width="296" height="683" alt="image" src="https://github.com/user-attachments/assets/c3349cba-8329-412a-afbf-f6ff1c2a1726" />

```
val = df['height']
val
```

<img width="393" height="467" alt="image" src="https://github.com/user-attachments/assets/58ea6e9c-194a-4a57-9855-e7d13707dae5" />

```
out=[]
def d_o(val):
    ts = 3
    m = np.mean(val)
    sd = np.std(val)
    for i in val:
        z = (i-m)/sd
        if np.abs(z)>ts:
            out.append(i)
    return out
op = d_o(val)
op
```

<img width="385" height="397" alt="image" src="https://github.com/user-attachments/assets/e29b9912-70ae-4e26-b3c7-54dcc640e9ce" />












# Result
          
The given data has been read and data has been cleaned and the data has been saved to a file.
