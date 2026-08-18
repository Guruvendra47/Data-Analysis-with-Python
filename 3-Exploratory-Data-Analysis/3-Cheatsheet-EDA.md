# Exploratory Data Analysis Cheat Sheet

Quick reference for common Pandas, Matplotlib, Seaborn, and SciPy methods used for exploratory data analysis.

## Complete DataFrame Correlation

Create a correlation matrix using all attributes in the DataFrame.

### Syntax

```python
df.corr()
```

### Example

```python
correlation = df.corr()
```

---

## Specific Attribute Correlation

Create a correlation matrix using selected attributes.

### Syntax

```python
df[
    ["attribute1", "attribute2"]
].corr()
```

### Example

```python
df[
    ["engine-size", "price"]
].corr()
```

---

## Scatter Plot

Create a scatter plot to visualize the relationship between two attributes.

### Syntax

```python
from matplotlib import pyplot as plt

plt.scatter(
    df["attribute1"],
    df["attribute2"]
)
```

### Example

```python
from matplotlib import pyplot as plt

plt.scatter(
    df["engine-size"],
    df["price"]
)
```

---

## Regression Plot

Create a scatter plot with a generated linear regression line.

### Syntax

```python
import seaborn as sns

sns.regplot(
    x="attribute1",
    y="attribute2",
    data=df
)
```

### Example

```python
import seaborn as sns

sns.regplot(
    x="engine-size",
    y="price",
    data=df
)
```

---

## Box Plot

Create a box-and-whisker plot to visualize the relationship between two attributes.

### Syntax

```python
import seaborn as sns

sns.boxplot(
    x="attribute1",
    y="attribute2",
    data=df
)
```

### Example

```python
import seaborn as sns

sns.boxplot(
    x="body-style",
    y="price",
    data=df
)
```

---

## Grouping by Attributes

Create a subset of the DataFrame using selected attributes.

### Syntax

```python
df_group = df[
    ["attribute1", "attribute2"]
]
```

### Example

```python
df_group = df[
    ["drive-wheels", "price"]
]
```

---

## GroupBy Statements

### Group by One Attribute

Group data by categories of one attribute and calculate the average of numerical attributes.

### Syntax

```python
df_group = df.groupby(
    ["attribute1"],
    as_index=False
).mean()
```

### Example

```python
df_group = df.groupby(
    ["drive-wheels"],
    as_index=False
).mean()
```

### Group by Multiple Attributes

Group data by multiple attributes and calculate the average of numerical attributes.

### Syntax

```python
df_group = df.groupby(
    ["attribute1", "attribute2"],
    as_index=False
).mean()
```

### Example

```python
df_group = df.groupby(
    ["drive-wheels", "body-style"],
    as_index=False
).mean()
```

---

## Pivot Tables

Create a pivot table for better representation of grouped data.

### Syntax

```python
grouped_pivot = df_group.pivot(
    index="attribute1",
    columns="attribute2"
)
```

### Example

```python
grouped_pivot = df_group.pivot(
    index="drive-wheels",
    columns="body-style"
)
```

---

## Pseudocolor Plot

Create a heatmap-style visualization using a pseudocolor (`pcolor`) plot and a pivot table.

### Syntax

```python
from matplotlib import pyplot as plt

plt.pcolor(
    grouped_pivot,
    cmap="RdBu"
)
```

### Example

```python
from matplotlib import pyplot as plt

plt.pcolor(
    grouped_pivot,
    cmap="RdBu"
)
```

---

## Pearson Correlation Coefficient and P-Value

Calculate the Pearson correlation coefficient and p-value for two attributes.

### Syntax

```python
from scipy import stats

pearson_coef, p_value = stats.pearsonr(
    df["attribute1"],
    df["attribute2"]
)
```

### Example

```python
from scipy import stats

pearson_coef, p_value = stats.pearsonr(
    df["engine-size"],
    df["price"]
)
```

## Quick Reference

| Method | Purpose |
|---|---|
| `df.corr()` | Correlation matrix for all attributes |
| `df[["a", "b"]].corr()` | Correlation for selected attributes |
| `plt.scatter()` | Scatter plot |
| `sns.regplot()` | Regression plot |
| `sns.boxplot()` | Box plot |
| `df.groupby()` | Group data by attributes |
| `df.pivot()` | Create pivot table |
| `plt.pcolor()` | Pseudocolor plot |
| `stats.pearsonr()` | Pearson coefficient and p-value |

Created by Guruvendra