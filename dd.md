# Data Wrangling in Pandas

Step-by-step procedure for cleaning, transforming, normalizing, binning, and preparing data for analysis using Pandas.

## 1. Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
```

## 2. Download the Dataset

Use `requests` or the provided download function to download the dataset.

```python
import requests

def download(url, filename):
    response = requests.get(url)
    if response.status_code == 200:
        with open(filename, "wb") as f:
            f.write(response.content)

download(file_path, "usedcars.csv")
```

## 3. Define Column Headers

Create a list containing the names of the columns.

```python
headers = [
    "symboling",
    "normalized-losses",
    "make",
    "fuel-type",
    "aspiration",
    "num-of-doors",
    "body-style",
    "drive-wheels",
    "engine-location",
    "wheel-base",
    "length",
    "width",
    "height",
    "curb-weight",
    "engine-type",
    "num-of-cylinders",
    "engine-size",
    "fuel-system",
    "bore",
    "stroke",
    "compression-ratio",
    "horsepower",
    "peak-rpm",
    "city-mpg",
    "highway-mpg",
    "price"
]
```

## 4. Read the Dataset

Load the dataset into a Pandas DataFrame.

### Syntax

```python
df = pd.read_csv(file_name, names=headers)
```

### Example

```python
df = pd.read_csv("usedcars.csv", names=headers)
```

## 5. View the Dataset

Use `head()` to display the first few rows.

### Syntax

```python
df.head(n)
```

### Example

```python
df.head()
```

The default value of `n` is 5.

## 6. Identify Missing Values

The dataset contains missing values represented by `?`.

### Convert `?` to `NaN`

Use NumPy's `np.nan` to represent missing values.

### Syntax

```python
df.replace(old_value, new_value, inplace=True)
```

### Example

```python
df.replace("?", np.nan, inplace=True)
```

## 7. Check for Missing Values

Use `isnull()` or `notnull()` to identify missing values.

### Syntax

```python
df.isnull()
```

### Example

```python
missing_data = df.isnull()

missing_data.head()
```

`True` means the value is missing.

`False` means the value is present.

## 8. Count Missing Values in Each Column

Use a loop and `value_counts()` to count missing and non-missing values.

### Syntax

```python
for column in dataframe.columns.values.tolist():
    print(column)
    print(dataframe[column].value_counts())
    print("")
```

### Example

```python
for column in missing_data.columns.values.tolist():
    print(column)
    print(missing_data[column].value_counts())
    print("")
```

## 9. Deal With Missing Data

There are two main approaches for dealing with missing data.

### Drop Data

1. Drop the whole row
2. Drop the whole column

### Replace Data

1. Replace with the mean
2. Replace with the frequency
3. Replace based on other functions

## 10. Replace Missing Values With the Mean

### Calculate the Mean

### Syntax

```python
average = df["column"].astype("float").mean(axis=0)
```

### Example

```python
avg_norm_loss = df["normalized-losses"].astype("float").mean(axis=0)

print("Average of normalized-losses:", avg_norm_loss)
```

### Replace `NaN` With the Mean

### Syntax

```python
df["column"].replace(np.nan, average, inplace=True)
```

### Example

```python
df["normalized-losses"].replace(np.nan, avg_norm_loss, inplace=True)
```

### Bore

```python
avg_bore = df["bore"].astype("float").mean(axis=0)

print("Average of bore:", avg_bore)

df["bore"].replace(np.nan, avg_bore, inplace=True)
```

### Stroke

```python
avg_stroke = df["stroke"].astype("float").mean(axis=0)

print("Average of stroke:", avg_stroke)

df["stroke"].replace(np.nan, avg_stroke, inplace=True)
```

### Horsepower

```python
avg_horsepower = df["horsepower"].astype("float").mean(axis=0)

print("Average horsepower:", avg_horsepower)

df["horsepower"].replace(np.nan, avg_horsepower, inplace=True)
```

### Peak RPM

```python
avg_peakrpm = df["peak-rpm"].astype("float").mean(axis=0)

print("Average peak rpm:", avg_peakrpm)

df["peak-rpm"].replace(np.nan, avg_peakrpm, inplace=True)
```

## 11. Replace Missing Values With the Most Frequent Value

Use `value_counts()` to find the frequency of values.

### Syntax

```python
df["column"].value_counts()
```

Use `idxmax()` to find the most frequent value.

### Syntax

```python
df["column"].value_counts().idxmax()
```

### Example

```python
df["num-of-doors"].value_counts()
```

```python
df["num-of-doors"].value_counts().idxmax()
```

Replace the missing values with the most frequent value.

```python
df["num-of-doors"].replace(np.nan, "four", inplace=True)
```

## 12. Drop Rows With Missing Values

Drop rows where the `price` column contains `NaN`.

### Syntax

```python
df.dropna(subset=["column"], axis=0, inplace=True)
```

### Example

```python
df.dropna(subset=["price"], axis=0, inplace=True)
```

Reset the index after dropping rows.

### Syntax

```python
df.reset_index(drop=True, inplace=True)
```

### Example

```python
df.reset_index(drop=True, inplace=True)
```

## 13. Check the Data Types

The next step is to make sure that all data is in the correct format.

### Syntax

```python
df.dtypes
```

### Example

```python
df.dtypes
```

Numerical variables should generally have `int` or `float` data types.

Categorical variables containing strings should generally have `object` data types.

## 14. Convert Data Types

Use `astype()` to convert columns to the correct data type.

### Syntax

```python
df["column"] = df["column"].astype("data_type")
```

### Example

```python
df[["bore", "stroke"]] = df[["bore", "stroke"]].astype("float")

df[["normalized-losses"]] = df[["normalized-losses"]].astype("int")

df[["price"]] = df[["price"]].astype("float")

df[["peak-rpm"]] = df[["peak-rpm"]].astype("float")
```

Check the data types again.

```python
df.dtypes
```

## 15. Data Standardization

Data standardization transforms data into a common format so meaningful comparisons can be made.

### Example: Convert MPG to L/100km

The `city-mpg` and `highway-mpg` columns are represented in miles per gallon.

### Formula

```text
L/100km = 235 / mpg
```

### Convert City MPG

```python
df["city-L/100km"] = 235 / df["city-mpg"]
```

### Convert Highway MPG

```python
df["highway-mpg"] = 235 / df["highway-mpg"]
```

Rename the column.

### Syntax

```python
df.rename(columns={"old_name": "new_name"}, inplace=True)
```

### Example

```python
df.rename(
    columns={"highway-mpg": "highway-L/100km"},
    inplace=True
)
```

## 16. Data Normalization

Normalization transforms values of several variables into a similar range.

Common normalization approaches include:

- Scaling the variable so the average is 0
- Scaling the variable so the variance is 1
- Scaling values so they range from 0 to 1

### Example

Normalize the following columns:

- `length`
- `width`
- `height`

### Formula

```text
normalized value = original value / maximum value
```

### Normalize Length

```python
df["length"] = df["length"] / df["length"].max()
```

### Normalize Width

```python
df["width"] = df["width"] / df["width"].max()
```

### Normalize Height

```python
df["height"] = df["height"] / df["height"].max()
```

The normalized values range from `0` to `1`.

## 17. Binning

Binning transforms continuous numerical variables into discrete categorical bins for grouped analysis.

### Example

The `horsepower` column contains many unique values.

Create three categories:

- Low
- Medium
- High

## 18. Convert Horsepower to Integer

```python
df["horsepower"] = df["horsepower"].astype(int, copy=True)
```

## 19. View the Distribution of Horsepower

```python
plt.pyplot.hist(df["horsepower"])

plt.pyplot.xlabel("horsepower")
plt.pyplot.ylabel("count")
plt.pyplot.title("horsepower bins")
```

## 20. Create Bins Using `linspace()`

Use NumPy's `linspace()` to create equally spaced bin boundaries.

### Syntax

```python
np.linspace(start_value, end_value, number_of_values)
```

### Example

```python
bins = np.linspace(
    min(df["horsepower"]),
    max(df["horsepower"]),
    4
)

bins
```

Four boundaries create three bins.

## 21. Create Group Names

```python
group_names = ["Low", "Medium", "High"]
```

## 22. Apply `pd.cut()`

Use `pd.cut()` to determine which bin each horsepower value belongs to.

### Syntax

```python
pd.cut(
    column,
    bins,
    labels=group_names,
    include_lowest=True
)
```

### Example

```python
df["horsepower-binned"] = pd.cut(
    df["horsepower"],
    bins,
    labels=group_names,
    include_lowest=True
)
```

View the result.

```python
df[["horsepower", "horsepower-binned"]].head(20)
```

## 23. Count Values in Each Bin

Use `value_counts()`.

### Syntax

```python
df["column"].value_counts()
```

### Example

```python
df["horsepower-binned"].value_counts()
```

## 24. Visualize the Bins

```python
plt.pyplot.bar(
    group_names,
    df["horsepower-binned"].value_counts()
)

plt.pyplot.xlabel("horsepower")
plt.pyplot.ylabel("count")
plt.pyplot.title("horsepower bins")
```

A histogram can also be used to visualize the distribution.

```python
plt.pyplot.hist(df["horsepower"], bins=3)

plt.pyplot.xlabel("horsepower")
plt.pyplot.ylabel("count")
plt.pyplot.title("horsepower bins")
```

## 25. Indicator Variables

An indicator variable, also called a dummy variable, is a numerical variable used to represent categories.

The categories are represented using `0` and `1`.

### Create Indicator Variables

Use Pandas `get_dummies()`.

### Syntax

```python
dummy_variable = pd.get_dummies(df["column"])
```

### Example

```python
dummy_variable_1 = pd.get_dummies(df["fuel-type"])

dummy_variable_1.head()
```

## 26. Rename Indicator Variable Columns

### Syntax

```python
dataframe.rename(
    columns={"old_name": "new_name"},
    inplace=True
)
```

### Example

```python
dummy_variable_1.rename(
    columns={
        "gas": "fuel-type-gas",
        "diesel": "fuel-type-diesel"
    },
    inplace=True
)
```

## 27. Merge Indicator Variables With the Original DataFrame

Use `pd.concat()` to merge the new DataFrame with the original DataFrame.

### Syntax

```python
df = pd.concat([df, dummy_variable], axis=1)
```

### Example

```python
df = pd.concat([df, dummy_variable_1], axis=1)
```

## 28. Drop the Original Categorical Column

### Syntax

```python
df.drop("column", axis=1, inplace=True)
```

### Example

```python
df.drop("fuel-type", axis=1, inplace=True)
```

## 29. Create Indicator Variables for Aspiration

```python
dummy_variable_2 = pd.get_dummies(df["aspiration"])
```

Rename the columns.

```python
dummy_variable_2.rename(
    columns={
        "std": "aspiration-std",
        "turbo": "aspiration-turbo"
    },
    inplace=True
)
```

## 30. Merge Aspiration Indicator Variables

```python
df = pd.concat([df, dummy_variable_2], axis=1)
```

Drop the original `aspiration` column.

```python
df.drop("aspiration", axis=1, inplace=True)
```

## 31. Save the Cleaned Dataset

Save the final cleaned DataFrame as a CSV file.

### Syntax

```python
df.to_csv("filename.csv")
```

### Example

```python
df.to_csv("clean_df.csv")
```

## Final Result

The final dataset has been:

- Loaded into Pandas
- Checked for missing values
- Missing values handled
- Data types corrected
- Data standardized
- Data normalized
- Continuous data converted into bins
- Categorical data converted into indicator variables
- Saved as a cleaned CSV file

---

Created by Guruvendra