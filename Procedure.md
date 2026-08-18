Yes. I’ll keep it **Markdown (`README.md`)**, add the missing `pd.to_numeric()` step, and not add unrelated content.

````markdown
# Data Cleaning in Pandas

Step-by-step procedure for cleaning data in Pandas.

Created by Guruvendra

## 1. Download the Dataset

Use `requests` to download the dataset.

```python
import requests

def download(url, filename):
    response = requests.get(url)
    if response.status_code == 200:
        with open(filename, "wb") as f:
            f.write(response.content)

# Usage
download(file_path, "laptops.csv")
````

## 2. Check for Missing Values

### Method 1: Using `sum()`

```python
df["Name"].isnull().sum()
```

### Method 2: Check Missing Values in Each Column

```python
k = df.isnull()

for i in k.columns.values.tolist():
    print(i)
    print(k[i].value_counts())
    print("")
```

## 3. Deal With Missing Data

There are two main approaches.

### Drop Data

* Drop the whole row
* Drop the whole column

### Replace Data

* Replace with the mean
* Replace with the frequency
* Replace based on other functions

## 4. Correct Data Format

The data should be in the correct format, such as:

* Integer
* Float
* Text
* Other appropriate formats

### Check Data Types

```python
df.dtypes
```

### Convert Data Types

Use `astype()` when converting a column to a specific data type.

```python
df["column"] = df["column"].astype("int")
```

### Convert Multiple Columns Using `pd.to_numeric()`

List the columns that need to be converted:

```python
cols = ["bore", "stroke", "normalized-losses", "price", "peak-rpm"]

df[cols] = df[cols].apply(pd.to_numeric, errors="coerce")
```

`errors="coerce"` converts invalid values to `NaN`.

## 5. Data Standardization

Data may be collected from different agencies in different formats.

Standardization transforms data into a common format so meaningful comparisons can be made.

### Example: Convert MPG to L/100km

Formula:

```text
L/100km = 235 / mpg
```

Example:

```python
df["city-mpg"] = 235 / df["city-mpg"]
df["highway-mpg"] = 235 / df["highway-mpg"]
```

## 6. Data Normalization

Normalization transforms values of several variables into a similar range.

Common approaches include:

* Scale the variable so the average is 0
* Scale the variable so the variance is 1
* Scale values so they range from 0 to 1

### Example

For `length`, `width`, and `height`, normalize values from 0 to 1.

Formula:

```text
normalized value = original value / maximum value
```

Example:

```python
df["length"] = df["length"] / df["length"].max()
df["width"] = df["width"] / df["width"].max()
df["height"] = df["height"] / df["height"].max()
```

## 7. Binning

Binning transforms continuous numerical variables into discrete categorical bins for grouped analysis.

### Example

`horsepower` ranges from 48 to 288 with many unique values.

If you only want three categories:

* Low horsepower
* Medium horsepower
* High horsepower

Use Pandas `cut()` to create 3 bins.

```python
bins = [48, 120, 200, 288]
labels = ["Low", "Medium", "High"]

df["horsepower-binned"] = pd.cut(
    df["horsepower"],
    bins,
    labels=labels
)
```

## Final Result

After these steps, the goal is to obtain a cleansed dataset with no missing values and data in the proper format.

```
```
