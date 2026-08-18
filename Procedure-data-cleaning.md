# Data Cleaning in Pandas

Step-by-step procedure for cleaning and preparing a dataset using Pandas.

## 1. Import the Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
import requests
```

## 2. Download and Load the Dataset

Download the dataset and load it into a Pandas DataFrame.

```python
def download(url, filename):
    response = requests.get(url)
    if response.status_code == 200:
        with open(filename, "wb") as f:
            f.write(response.content)

download(file_path, "usedcars.csv")
```

```python
df = pd.read_csv("usedcars.csv", names=headers)
```

## 3. Inspect the Dataset

Check the first few rows and understand the structure of the data.

```python
df.head()
df.dtypes
```

## 4. Identify Missing Values

Convert `?` values to `NaN`, then check for missing data.

```python
df.replace("?", np.nan, inplace=True)
```

```python
missing_data = df.isnull()
```

Count missing values:

```python
df.isnull().sum()
```

Or check each column:

```python
for column in missing_data.columns.values.tolist():
    print(column)
    print(missing_data[column].value_counts())
    print("")
```

## 5. Handle Missing Values

Choose the appropriate method based on the column.

### Replace Numerical Values

Use the mean for numerical columns such as `normalized-losses`, `bore`, `stroke`, `horsepower`, and `peak-rpm`.

```python
average = df["column"].astype("float").mean(axis=0)

df["column"].replace(
    np.nan,
    average,
    inplace=True
)
```

### Replace Categorical Values

Use the most frequent value for categorical data.

```python
df["num-of-doors"].value_counts().idxmax()
```

```python
df["num-of-doors"].replace(
    np.nan,
    "four",
    inplace=True
)
```

### Drop Rows

If an important value such as `price` is missing, remove the row.

```python
df.dropna(
    subset=["price"],
    axis=0,
    inplace=True
)

df.reset_index(
    drop=True,
    inplace=True
)
```

## 6. Correct Data Types

Check the data types:

```python
df.dtypes
```

Convert columns to the correct format using `astype()` or `pd.to_numeric()`.

```python
df[["bore", "stroke"]] = df[
    ["bore", "stroke"]
].astype("float")
```

For multiple columns:

```python
cols = [
    "bore",
    "stroke",
    "normalized-losses",
    "price",
    "peak-rpm"
]

df[cols] = df[cols].apply(
    pd.to_numeric,
    errors="coerce"
)
```

Check the result:

```python
df.dtypes
```

## 7. Standardize Data

Convert values into a common format when necessary.

For example, convert MPG to L/100km.

```text
L/100km = 235 / mpg
```

```python
df["city-L/100km"] = (
    235 / df["city-mpg"]
)

df["highway-mpg"] = (
    235 / df["highway-mpg"]
)
```

Rename the converted column:

```python
df.rename(
    columns={
        "highway-mpg": "highway-L/100km"
    },
    inplace=True
)
```

## 8. Normalize Data

Normalize numerical variables to a similar range.

For values between 0 and 1:

```text
normalized value = original value / maximum value
```

```python
df["length"] = (
    df["length"] / df["length"].max()
)

df["width"] = (
    df["width"] / df["width"].max()
)

df["height"] = (
    df["height"] / df["height"].max()
)
```

## 9. Create Bins

Convert continuous numerical values into categories.

For example, divide `horsepower` into:

- Low
- Medium
- High

Create the bin boundaries:

```python
bins = np.linspace(
    min(df["horsepower"]),
    max(df["horsepower"]),
    4
)
```

Define the categories:

```python
group_names = [
    "Low",
    "Medium",
    "High"
]
```

Apply the bins:

```python
df["horsepower-binned"] = pd.cut(
    df["horsepower"],
    bins,
    labels=group_names,
    include_lowest=True
)
```

Check the distribution:

```python
df["horsepower-binned"].value_counts()
```

## 10. Convert Categorical Data to Indicator Variables

Convert categorical columns into numerical `0` and `1` values.

```python
dummy_variable = pd.get_dummies(
    df["fuel-type"]
)
```

Rename the columns:

```python
dummy_variable.rename(
    columns={
        "gas": "fuel-type-gas",
        "diesel": "fuel-type-diesel"
    },
    inplace=True
)
```

Merge them into the DataFrame:

```python
df = pd.concat(
    [df, dummy_variable],
    axis=1
)
```

Drop the original categorical column:

```python
df.drop(
    "fuel-type",
    axis=1,
    inplace=True
)
```

The same process can be applied to other categorical columns such as `aspiration`.

## 11. Save the Cleaned Dataset

Save the final cleaned DataFrame.

```python
df.to_csv(
    "clean_df.csv"
)
```

## Data Cleaning Workflow

```text
Download Dataset
      ↓
Load Dataset
      ↓
Inspect Data
      ↓
Identify Missing Values
      ↓
Handle Missing Values
      ↓
Correct Data Types
      ↓
Standardize Data
      ↓
Normalize Data
      ↓
Create Bins
      ↓
Create Indicator Variables
      ↓
Save Clean Dataset
```

Created by Guruvendra