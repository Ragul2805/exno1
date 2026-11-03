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

## Data_set.csv
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv(r"C:\Users\acer\Downloads\Data_set.csv")

print("DATA_SET")
df.info()
print(df.describe(include='all'))

print("Null Values:")
print(df.isnull().sum())

df_nafill_0 = df.fillna(0)
print(df_nafill_0)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

df_mean = df.copy()
for col in df_mean.select_dtypes(include=np.number).columns:
    df_mean[col] = df_mean[col].fillna(df_mean[col].mean())
print(df_mean)

df_median = df.copy()
for col in df_median.select_dtypes(include=np.number).columns:
    df_median[col] = df_median[col].fillna(df_median[col].median())
print(df_median)

df_dropna = df.dropna()
print(df_dropna)

df_mean.to_csv("clean_Data_set.csv", index=False)

print("DATA CLEANING COMPLETED SUCCESSFULLY")
```
<img width="1245" height="386" alt="Screenshot 2026-11-03 153945" src="https://github.com/user-attachments/assets/a450c187-0961-4c8b-88e8-31da0a86e91f" />

## SAMPLEIDS.csv
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv(r"C:\Users\acer\Downloads\SAMPLEIDS.csv")

print("SAMPLE IDS")
df.info()
print(df.describe(include='all'))

print("Null Values:")
print(df.isnull().sum())

df_nafill_0 = df.fillna(0)
print(df_nafill_0)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

df_mean = df.copy()
for col in df_mean.select_dtypes(include=np.number).columns:
    df_mean[col] = df_mean[col].fillna(df_mean[col].mean())
print(df_mean)

df_median = df.copy()
for col in df_median.select_dtypes(include=np.number).columns:
    df_median[col] = df_median[col].fillna(df_median[col].median())
print(df_median)

df_dropna = df.dropna()
print(df_dropna)

df_median.to_csv("clean_SAMPLEIDS.csv", index=False)

print("DATA CLEANING COMPLETED SUCCESSFULLY")
```
<img width="1100" height="334" alt="image" src="https://github.com/user-attachments/assets/b1190370-fda3-4577-91d8-acbbd4b1b711" />


## Heights.csv
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv(r"C:\Users\acer\Downloads\heights.csv")

print("HEIGHTS")
df.info()
print(df.describe(include='all'))

print("Null Values:")
print(df.isnull().sum())

df_nafill_0 = df.fillna(0)
print(df_nafill_0)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

df_mean = df.copy()
for col in df_mean.select_dtypes(include=np.number).columns:
    df_mean[col] = df_mean[col].fillna(df_mean[col].mean())
print(df_mean)

df_median = df.copy()
for col in df_median.select_dtypes(include=np.number).columns:
    df_median[col] = df_median[col].fillna(df_median[col].median())
print(df_median)

df_dropna = df.dropna()
print(df_dropna)

df_median.to_csv("clean_heights.csv", index=False)

col = df.select_dtypes(include=np.number).columns[0]

z = np.abs(stats.zscore(df[col], nan_policy='omit'))

threshold = 3

outliers = df[z > threshold]
print("Outliers:")
print(outliers)

df_cleaned = df[z <= threshold]
print("After Removing Outliers:")
print(df_cleaned)

df_cleaned.to_csv("heights_zscore_clean.csv", index=False)

print("DATA CLEANING COMPLETED SUCCESSFULLY")
```
<img width="1079" height="332" alt="image" src="https://github.com/user-attachments/assets/2a5349bd-f097-4f87-b87b-27e3e241b57f" />

## Iris.csv
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv(r"C:\Users\acer\iris.csv")

print("IRIS")
df.info()
print(df.describe(include='all'))

print("Null Values:")
print(df.isnull().sum())

df_nafill_0 = df.fillna(0)
print(df_nafill_0)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

df_mean = df.copy()
for col in df_mean.select_dtypes(include=np.number).columns:
    df_mean[col] = df_mean[col].fillna(df_mean[col].mean())
print(df_mean)

df_median = df.copy()
for col in df_median.select_dtypes(include=np.number).columns:
    df_median[col] = df_median[col].fillna(df_median[col].median())
print(df_median)

df_dropna = df.dropna()
print(df_dropna)

df_median.to_csv("clean_iris.csv", index=False)

sns.boxplot(data=df.select_dtypes(include=np.number))
plt.title("Iris Dataset Boxplot")
plt.show()

sns.scatterplot(data=df, x='sepal_length',
                y='sepal_width', hue='species')
plt.title("Iris Dataset Scatterplot")
plt.show()

q1 = df['sepal_width'].quantile(0.25)
q3 = df['sepal_width'].quantile(0.75)

iqr = q3 - q1

print("IQR:", iqr)

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outliers = df[(df['sepal_width'] < lower) |
              (df['sepal_width'] > upper)]

print("Outliers:")
print(outliers)

df_cleaned = df[(df['sepal_width'] >= lower) &
                (df['sepal_width'] <= upper)]

print("After Removing Outliers:")
print(df_cleaned)

df_cleaned.to_csv("iris_iqr_clean.csv", index=False)

print("DATA CLEANING COMPLETED SUCCESSFULLY")
```
<img width="1107" height="343" alt="Screenshot 2026-11-03 154446" src="https://github.com/user-attachments/assets/49b297ad-0140-4806-a4f6-cd744f0dbb2c" />

## Loan_data.csv
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv(r"C:\Users\acer\Downloads\Loan_data.csv")

print("LOAN DATA")
df.info()
print(df.describe(include='all'))

print("Null Values:")
print(df.isnull().sum())

df_nafill_0 = df.fillna(0)
print(df_nafill_0)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

df_mean = df.copy()
for col in df_mean.select_dtypes(include=np.number).columns:
    df_mean[col] = df_mean[col].fillna(df_mean[col].mean())
print(df_mean)

df_median = df.copy()
for col in df_median.select_dtypes(include=np.number).columns:
    df_median[col] = df_median[col].fillna(df_median[col].median())
print(df_median)

df_dropna = df.dropna()
print(df_dropna)

df_median.to_csv("clean_Loan_data.csv", index=False)

num = df_median.select_dtypes(include=np.number)

sns.boxplot(data=num)
plt.title("Loan Dataset Boxplot")
plt.show()

col = num.columns[0]

q1 = num[col].quantile(0.25)
q3 = num[col].quantile(0.75)

iqr = q3 - q1

print("IQR:", iqr)

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outliers = df_median[(df_median[col] < lower) |
                     (df_median[col] > upper)]

print("IQR Outliers:")
print(outliers)

df_iqr_clean = df_median[(df_median[col] >= lower) &
                         (df_median[col] <= upper)]

print("After Removing IQR Outliers:")
print(df_iqr_clean)

df_iqr_clean.to_csv("Loan_IQR_Clean.csv", index=False)

z = np.abs(stats.zscore(df_median[col], nan_policy='omit'))

threshold = 3

outliers = df_median[z > threshold]
print("Z-Score Outliers:")
print(outliers)

df_zclean = df_median[z <= threshold]
print("After Removing Z-Score Outliers:")
print(df_zclean)

df_zclean.to_csv("Loan_Zscore_Clean.csv", index=False)

if len(num.columns) >= 2:
    sns.scatterplot(data=num, x=num.columns[0], y=num.columns[1])
    plt.title("Loan Dataset Scatterplot")
    plt.show()

print("DATA CLEANING COMPLETED SUCCESSFULLY")
```
<img width="1069" height="336" alt="Screenshot 2026-11-03 154649" src="https://github.com/user-attachments/assets/c8739c9c-ce7b-4a16-92b7-d2a8c0dfd350" />


# Result
Thus, the five datasets (Data_set, Heights, Iris, Loan_data, and SAMPLEIDS) were successfully analyzed and cleaned using Python Pandas and NumPy. Missing values were handled using different imputation methods, and outliers were detected and removed using IQR and Z-Score methods. Boxplots and scatterplots were used for data visualization. The cleaned datasets were successfully saved as CSV files.
