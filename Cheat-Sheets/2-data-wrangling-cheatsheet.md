# Data Wrangling Cheat Sheet

Quick reference for common Pandas and NumPy methods used for data wrangling.

## Replace Missing Data With Frequency

Replace missing values with the most frequently occurring value (mode) in the column.

### Syntax

```python
MostFrequentEntry = df["attribute_name"].value_counts().idxmax()

df["attribute_name"].replace(
    np.nan,
    MostFrequentEntry,
    inplace=True
)
```

### Example

```python
MostFrequentEntry = df["num-of-doors"].value_counts().idxmax()

df["num-of-doors"].replace(
    np.nan,
    MostFrequentEntry,
    inplace=True
)
```

---

## Replace Missing Data With Mean

Replace missing values with the mean of the column.

### Syntax

```python
AverageValue = df["attribute_name"].astype("<data_type>").mean(axis=0)

df["attribute_name"].replace(
    np.nan,
    AverageValue,
    inplace=True
)
```

### Example

```python
AverageValue = df["normalized-losses"].astype("float").mean(axis=0)

df["normalized-losses"].replace(
    np.nan,
    AverageValue,
    inplace=True
)
```

---

## Fix the Data Types

Convert DataFrame columns to the appropriate data type.

### Syntax

```python
df[[
    "attribute1_name",
    "attribute2_name"
]] = df[[
    "attribute1_name",
    "attribute2_name"
]].astype("data_type")
```

`data_type` can be `int`, `float`, or another appropriate type.

### Example

```python
df[["bore", "stroke"]] = df[
    ["bore", "stroke"]
].astype("float")
```

---

## Data Normalization

Normalize a column so that its values are restricted between `0` and `1`.

### Syntax

```python
df["attribute_name"] = (
    df["attribute_name"] /
    df["attribute_name"].max()
)
```

### Example

```python
df["length"] = (
    df["length"] /
    df["length"].max()
)
```

---

## Binning

Create bins for numerical data to make analysis and visualization easier.

### Syntax

```python
bins = np.linspace(
    min(df["attribute_name"]),
    max(df["attribute_name"]),
    n
)

GroupNames = [
    "Group1",
    "Group2",
    "Group3"
]

df["binned_attribute_name"] = pd.cut(
    df["attribute_name"],
    bins,
    labels=GroupNames,
    include_lowest=True
)
```

`n` represents the number of values used to create the bin boundaries.

### Example

```python
bins = np.linspace(
    min(df["horsepower"]),
    max(df["horsepower"]),
    4
)

GroupNames = [
    "Low",
    "Medium",
    "High"
]

df["horsepower-binned"] = pd.cut(
    df["horsepower"],
    bins,
    labels=GroupNames,
    include_lowest=True
)
```

---

## Change Column Name

Change the label of a DataFrame column.

### Syntax

```python
df.rename(
    columns={
        "old_name": "new_name"
    },
    inplace=True
)
```

### Example

```python
df.rename(
    columns={
        "highway-mpg": "highway-L/100km"
    },
    inplace=True
)
```

---

## Indicator Variables

Create indicator variables for categorical data.

### Syntax

```python
dummy_variable = pd.get_dummies(
    df["attribute_name"]
)

df = pd.concat(
    [df, dummy_variable],
    axis=1
)
```

### Example

```python
dummy_variable = pd.get_dummies(
    df["fuel-type"]
)

df = pd.concat(
    [df, dummy_variable],
    axis=1
)
```

---

## Quick Reference

| Method | Purpose |
|---|---|
| `value_counts().idxmax()` | Find the most frequent value |
| `replace()` | Replace missing values |
| `astype()` | Change data type |
| `mean()` | Calculate the mean |
| `np.linspace()` | Create evenly spaced values for bins |
| `pd.cut()` | Create categorical bins |
| `rename()` | Change column names |
| `pd.get_dummies()` | Create indicator variables |
| `pd.concat()` | Combine DataFrames |

Created by Guruvendra