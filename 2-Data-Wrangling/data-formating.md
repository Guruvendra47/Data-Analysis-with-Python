# Data Formatting

A collection of notes covering the fundamentals of data formatting and preprocessing using Pandas and NumPy. These techniques help prepare raw data for analysis and machine learning.

---

## Topics Covered

- Data Formatting
- Unit Conversion
- Data Types
- Data Normalization
- Feature Scaling
- Min-Max Normalization
- Z-Score Normalization
- Binning
- Histograms
- One-Hot Encoding

---

## Data Formatting

Data formatting makes data from different sources consistent, clean, and ready for analysis.

Examples include:

- Converting units
- Correcting data types
- Handling inconsistent values

---

## Unit Conversion

Convert values from one unit to another.

**Syntax**

```python
df["new_column"] = df["column"] * conversion_factor
```

**Example**

```python
# Convert city MPG to L/100km

df["city-L/100km"] = 235 / df["city-mpg"]
```

---

## Data Types

Check and convert data types for accurate analysis.

### Check Data Types

**Syntax**

```python
df.dtypes
```

**Example**

```python
print(df.dtypes)
```

### Convert Data Type

**Syntax**

```python
df["column"] = df["column"].astype(data_type)
```

**Example**

```python
df["price"] = df["price"].astype(float)

df["year"] = df["year"].astype(int)
```

---

## Data Normalization

Normalization scales values so different variables become comparable.

Common methods:

- Feature Scaling
- Min-Max Normalization
- Z-Score Normalization

---

## Feature Scaling

Scales values between 0 and 1.

**Syntax**

```python
df["column"] = df["column"] / df["column"].max()
```

**Example**

```python
df["length"] = df["length"] / df["length"].max()
```

---

## Min-Max Normalization

Transforms values into a range between 0 and 1.

**Syntax**

```python
df["column"] = (
    df["column"] - df["column"].min()
) / (
    df["column"].max() - df["column"].min()
)
```

**Example**

```python
df["horsepower"] = (
    df["horsepower"] - df["horsepower"].min()
) / (
    df["horsepower"].max() - df["horsepower"].min()
)
```

---

## Z-Score Normalization

Centers data around a mean of 0 with a standard deviation of 1.

**Syntax**

```python
df["column"] = (
    df["column"] - df["column"].mean()
) / df["column"].std()
```

**Example**

```python
df["price"] = (
    df["price"] - df["price"].mean()
) / df["price"].std()
```

---

## Binning

Groups continuous numerical values into intervals (bins).

Useful for:

- Improving model accuracy
- Simplifying visualization
- Grouping continuous data

---

### Create Bins

**Syntax**

```python
bins = np.linspace(start, stop, number_of_bins)
```

**Example**

```python
import numpy as np

bins = np.linspace(
    df["price"].min(),
    df["price"].max(),
    4
)
```

---

### Assign Values to Bins

**Syntax**

```python
pd.cut(column, bins, labels=labels)
```

**Example**

```python
labels = ["Low", "Medium", "High"]

df["price-binned"] = pd.cut(
    df["price"],
    bins,
    labels=labels
)
```

---

## Histogram

Visualize the distribution of binned data.

**Syntax**

```python
plt.hist(column)
```

**Example**

```python
import matplotlib.pyplot as plt

plt.hist(df["price"])
plt.show()
```

---

## One-Hot Encoding

Converts categorical variables into numerical variables.

Useful for machine learning models.

**Syntax**

```python
pd.get_dummies(df["column"])
```

**Example**

```python
fuel = pd.get_dummies(df["fuel-type"])

df = pd.concat([df, fuel], axis=1)

df.drop("fuel-type", axis=1, inplace=True)
```

---

## Common Workflow

```python
import pandas as pd
import numpy as np

# Check data types
df.dtypes

# Convert data type
df["price"] = df["price"].astype(float)

# Normalize data
df["length"] = df["length"] / df["length"].max()

# Create bins
bins = np.linspace(
    df["price"].min(),
    df["price"].max(),
    4
)

labels = ["Low", "Medium", "High"]

df["price-binned"] = pd.cut(
    df["price"],
    bins,
    labels=labels
)

# One-hot encoding
fuel = pd.get_dummies(df["fuel-type"])

df = pd.concat([df, fuel], axis=1)
```