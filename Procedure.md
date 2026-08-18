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
```

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

- Drop the whole row
- Drop the whole column

### Replace Data

- Replace with the mean
- Replace with the frequency
- Replace based on other functions

## 4. Correct Data Format

The last step in data cleaning is checking and making sure that all data is in the correct format.

Examples:

- Integer
- Float
- Text
- Other appropriate formats

### Check Data Types

Use `.dtypes` to check the data type of each column.

```python
df.dtypes
```

### Change Data Types

Use `.astype()` to change the data type.

```python
df["column"] = df["column"].astype("int")
```

### Convert Multiple Columns Using `pd.to_numeric()`

List the columns you want to convert.

```python
cols = ["bore", "stroke", "normalized-losses", "price", "peak-rpm"]

df[cols] = df[cols].apply(pd.to_numeric, errors="coerce")
```

`errors="coerce"` converts values that cannot be converted into `NaN`.

## 5. Data Standardization

Data is usually collected from different agencies in different formats.

Data standardization is the process of transforming data into a common format, allowing meaningful comparisons.

### Example: Convert MPG to L/100km

The fuel consumption columns `city-mpg` and `highway-mpg` are represented using MPG.

Formula:

```text
L/100km = 235 / mpg
```

Using Pandas:

```python
df["city-mpg"] = 235 / df["city-mpg"]
df["highway-mpg"] = 235 / df["highway-mpg"]
```

## 6. Data Normalization

Normalization is the process of transforming values of several variables into a similar range.

Typical normalization approaches include:

- Scaling the variable so the average is 0
- Scaling the variable so the variance is 1
- Scaling the variable so the values range from 0 to 1

### Example

Normalize the columns:

- `length`
- `width`
- `height`

Target: Normalize the variables so their values range from 0 to 1.

Formula:

```text
normalized value = original value / maximum value
```

Using Pandas:

```python
df["length"] = df["length"] / df["length"].max()
df["width"] = df["width"] / df["width"].max()
df["height"] = df["height"] / df["height"].max()
```

## 7. Binning

Binning is the process of transforming continuous numerical variables into discrete categorical bins for grouped analysis.

### Example

The `horsepower` column contains values ranging from 48 to 288 with many unique values.

If you only care about:

- Low horsepower
- Medium horsepower
- High horsepower

You can divide the values into three bins.

### Using `pd.cut()`

```python
bins = [48, 120, 200, 288]
labels = ["Low", "Medium", "High"]

df["horsepower-binned"] = pd.cut(
    df["horsepower"],
    bins=bins,
    labels=labels
)
```

## Final Result

After completing the data cleaning steps, the goal is to obtain a cleansed dataset with:

- No missing values
- Correct data formats
- Standardized values
- Normalized variables where required
- Binned numerical variables where required