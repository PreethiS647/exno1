# Exno:1
Data Cleaning Process


# Register no: 212223230157


# Name: Preethi S

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
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```

![image](https://github.com/user-attachments/assets/f5a3704f-8be4-47b4-94e6-74183e8b82a3)

```
df.shape
```

![image](https://github.com/user-attachments/assets/a0e74b07-fd05-4d06-bd56-c364aeda11b1)

```
df.describe()
```

![image](https://github.com/user-attachments/assets/c78dcb8c-fe3d-4118-b014-dd2a2ffe497c)

```
df.info()
```

![image](https://github.com/user-attachments/assets/4083a6cd-b636-423d-aafe-6859762e4dbe)

```
df.head(5)
```

![image](https://github.com/user-attachments/assets/cd595796-06ec-4a1b-97dd-438b231dc836)

```
df.tail(2)
```

![image](https://github.com/user-attachments/assets/6d1bbec6-4035-475c-ada8-9dec854f9c47)

df.isnull().sum()

![image](https://github.com/user-attachments/assets/f9b2d67e-def0-4208-9d31-cf6425ab8c78)

df.dropna(how='any').shape

![image](https://github.com/user-attachments/assets/2a1e31de-ae0d-4cbd-be39-0ef538e2b8d8)

df.shape

![image](https://github.com/user-attachments/assets/580a729d-c52e-4b03-8d35-29bba75c71b2)

mn=df.TOTAL.mean()
df.TOTAL.fillna(mn,inplace=True)
df

![image](https://github.com/user-attachments/assets/98ebfc5a-5115-471d-8566-c3457f32abf4)

df.M1.dropna(inplace=True)
df

![image](https://github.com/user-attachments/assets/5d7dbc0a-23db-49b7-8bd6-b7d39ba5e2f0)

df['M1'].fillna(method='ffill',inplace=True)

![image](https://github.com/user-attachments/assets/f51ada99-abf7-4ec6-8810-dc1f14238ef8)

df.isna().sum()

![image](https://github.com/user-attachments/assets/2f1d5c87-5aa4-4421-bda1-2fdcdbe99296)

df.duplicated()

![image](https://github.com/user-attachments/assets/1574a3da-9712-47bf-9eb4-d98574794265)

df.drop_duplicates(inplace=True)
df

![image](https://github.com/user-attachments/assets/a8c25291-bc08-4cdd-bc49-cd78ee949de4)

df.duplicated()

![image](https://github.com/user-attachments/assets/45560c5d-6318-4b18-ac30-9adfc46bf33b)

df['DOB']

![image](https://github.com/user-attachments/assets/53749277-aa6e-48b5-8f21-f90313925f7f)

import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)

![image](https://github.com/user-attachments/assets/c7a02c59-4bea-49b0-8c13-9d38068bf243)
```

## OUTLIER DETECTION AND REMOVAL USING IQR

```
import pandas as pd
import seaborn as sns
import numpy as np
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af

![image](https://github.com/user-attachments/assets/6cc98289-5313-443d-ad28-f5d5528a418b)

sns.boxplot(data=af)

![image](https://github.com/user-attachments/assets/cab42321-0113-4981-a950-343e5004eb05)

sns.scatterplot(data=af)

![image](https://github.com/user-attachments/assets/e88eed17-0127-4fe1-bf6b-f3fd2228fa7a)

q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr

![image](https://github.com/user-attachments/assets/33f4d320-9deb-401c-bf91-9088cb0b6954)

Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-q1
IQR

![image](https://github.com/user-attachments/assets/75bb9972-b0c8-43cd-9a65-e8e453a85c05)

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound

![image](https://github.com/user-attachments/assets/012e8e5a-c5ae-422f-8f3c-a365c3862c5c)

upper_bound

![image](https://github.com/user-attachments/assets/b4b88613-b463-4660-b9af-6923afc3a2dd)

outliers = [x for x in age if (x < lower_bound.iloc[0]) or (x > upper_bound.iloc[0])]
# Extract the numeric values from the Series for comparison
print("q1",q1)
print("q3",q3)
print("iqr",iqr)
print("lower bound",lower_bound)
print("upper bound",upper_bound)
print("outliers",outliers)

![image](https://github.com/user-attachments/assets/0e72353b-946b-43c1-b97c-8c7f0e7217c2)

af=af[((af>=lower_bound)&(af<=upper_bound))]

![image](https://github.com/user-attachments/assets/1ae62e2c-4afb-4df5-8f69-5d848138532d)

af.dropna()

![image](https://github.com/user-attachments/assets/88a0da36-4eda-4761-8900-1203e947b67a)

data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)

![image](https://github.com/user-attachments/assets/1c9e18af-4fad-46c9-bad2-2599d9adbff4)

threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
    print('Outlier in dataset is:',outlier)

![image](https://github.com/user-attachments/assets/d1a5be38-760e-4f83-bc84-d81b7f6a9100)

import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}

df=pd.DataFrame(data)
df

![image](https://github.com/user-attachments/assets/58ce13c2-496e-4df3-93eb-28ad3590c69c)

z=np.abs(stats.zscore(df))
print(df[z['weight']>3])

![image](https://github.com/user-attachments/assets/300fa3d3-7239-4bfe-8981-2634e7885a5f)

val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]

import numpy as np
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out

op=d_o(val)
op

![image](https://github.com/user-attachments/assets/92c6a893-04a6-4e65-898c-d0d52386dffa)














































































```
# Result
          <<include your Result here>>
