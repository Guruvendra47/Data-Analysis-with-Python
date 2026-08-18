# Importing Data Sets

A collection of notes covering the fundamentals of importing datasets into Python using Pandas. This includes reading CSV files, inspecting data, assigning headers, handling missing values, generating statistical summaries, and exporting cleaned datasets.

---

## Topics Covered

- Reading CSV Files
- Viewing Data
- Assigning Column Headers
- Handling Missing Values
- Data Types
- Statistical Summary
- Dataset Information
- Exporting Data

---

## Read CSV Dataset

Reads a CSV file into a Pandas DataFrame.

**Syntax**

```python
df = pd.read_csv("file.csv", header=None)

df = pd.read_csv("file.csv", header=0)
```

**Example**

```python
import pandas as pd

df = pd.read_csv("cars.csv", header=None)
```

> **Note:**  
> - `header=None` → No column headers in the file.
> - `header=0` → Uses the first row as column names.

---

## Print First Few Rows

Displays the first *n* rows of the DataFrame.

**Syntax**

```python
df.head(n)
```

**Example**

```python
df.head()

df.head(10)
```

---

## Print Last Few Rows

Displays the last *n* rows of the DataFrame.

**Syntax**

```python
df.tail(n)
```

**Example**

```python
df.tail()

df.tail(10)
```

---

## Assign Column Headers

Assigns column names to the DataFrame.

**Syntax**

```python
df.columns = headers
```

**Example**

```python
headers = ["Name", "Age", "Salary"]

df.columns = headers
```

---

## Replace Missing Values

Replaces `"?"` with NumPy's `NaN`.

**Syntax**

```python
df = df.replace("?", np.nan)
```

**Example**

```python
import numpy as np

df = df.replace("?", np.nan)
```

---

## Retrieve Data Types

Displays the data type of each column.

**Syntax**

```python
df.dtypes
```

**Example**

```python
print(df.dtypes)
```

---

## Statistical Summary

Generates summary statistics.

**Syntax**

```python
df.describe()

df.describe(include="all")
```

**Example**

```python
df.describe()

df.describe(include="all")
```

Returns:

- Count
- Mean
- Standard Deviation
- Minimum
- Maximum
- Quartiles (25%, 50%, 75%)

---

## Dataset Information

Displays a summary of the DataFrame.

**Syntax**

```python
df.info()
```

**Example**

```python
df.info()
```

Shows:

- Number of rows
- Number of columns
- Column names
- Data types
- Non-null values
- Memory usage

---

## Save DataFrame to CSV

Exports the DataFrame to a CSV file.

**Syntax**

```python
df.to_csv("output.csv", index=False)
```

**Example**

```python
df.to_csv("cleaned_data.csv", index=False)
```

---

## Common Workflow

```python
import pandas as pd
import numpy as np

# Read dataset
df = pd.read_csv("data.csv")

# View data
df.head()

# Check information
df.info()

# Check data types
df.dtypes

# Replace missing values
df.replace("?", np.nan)

# Generate summary statistics
df.describe()

# Save cleaned dataset
df.to_csv("cleaned_data.csv", index=False)
```