# Exploratory Data Analysis

Step-by-step procedure for exploring data, understanding individual feature patterns, performing descriptive statistical analysis, grouping data, creating pivot tables, and analyzing correlation and causation.

## Objectives

After completing this analysis, you will be able to:

- Explore features or characteristics to predict car price
- Analyze patterns and perform descriptive statistical analysis
- Group data based on identified parameters and create pivot tables
- Identify the effect of independent attributes on car price

---

## 1. Import Data

Load the cleaned dataset prepared during data wrangling.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("clean_df.csv")
```

Inspect the dataset:

```python
df.head()
```

---

## 2. Analyzing Individual Feature Patterns Using Visualization

Before selecting a visualization, identify the type of variables being analyzed.

### Continuous Numerical Variables

Continuous numerical variables are numerical variables such as:

- `int`
- `float`

Examples include:

- Engine size
- Horsepower
- Price
- Length
- Width
- Height

When analyzing the relationship between two continuous numerical variables, use a **scatter plot**.

### Scatter Plot

A scatter plot shows the relationship between two continuous numerical variables.

For example:

- `engine-size` → independent variable
- `price` → dependent variable

### Syntax

```python
plt.scatter(
    df["attribute1"],
    df["attribute2"]
)
```

### Example

```python
plt.scatter(
    df["engine-size"],
    df["price"]
)

plt.xlabel("Engine Size")
plt.ylabel("Price")
plt.show()
```

### Regression Plot

A regression plot combines a scatter plot with a generated linear regression line.

It is useful when exploring the relationship between two continuous numerical variables.

### Syntax

```python
sns.regplot(
    x="attribute1",
    y="attribute2",
    data=df
)
```

### Example

```python
sns.regplot(
    x="engine-size",
    y="price",
    data=df
)

plt.show()
```

### Categorical Variables

Categorical variables represent groups or categories.

Examples include:

- Drive wheels
- Body style
- Fuel type
- Engine location
- Number of cylinders

When analyzing a categorical variable against a continuous numerical variable, use a **box plot**.

### Box Plot

A box-and-whisker plot shows the distribution of numerical values across different categories.

It can show:

- Median
- Quartiles
- Distribution
- Outliers

### Syntax

```python
sns.boxplot(
    x="attribute1",
    y="attribute2",
    data=df
)
```

### Example

```python
sns.boxplot(
    x="drive-wheels",
    y="price",
    data=df
)

plt.show()
```

### Visualization Selection

| Variable Types | Recommended Visualization |
|---|---|
| Continuous + Continuous | Scatter Plot |
| Continuous + Continuous with regression | Regression Plot |
| Categorical + Continuous | Box Plot |
| Categorical | Value Counts / Bar Plot |

### Simple Rule

```text
Continuous + Continuous
        ↓
   Scatter Plot
        ↓
   Regression Plot

Categorical + Continuous
        ↓
     Box Plot
```

---

## 3. Descriptive Statistical Analysis

Use `describe()` to obtain statistical information about numerical variables.

### Syntax

```python
df.describe()
```

### Example

```python
df.describe()
```

This provides:

- Count
- Mean
- Standard deviation
- Minimum
- 25% quartile
- 50% quartile
- 75% quartile
- Maximum

### Value Counts

Use `value_counts()` to summarize categorical data.

### Syntax

```python
df["attribute"].value_counts()
```

### Example

```python
df["body-style"].value_counts()
```

This shows the number of observations in each category.

---

## 4. Grouping Data

Grouping allows you to analyze relationships between categorical variables and numerical values.

### Select Attributes

Create a subset containing the attributes needed for analysis.

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

### Group By One Attribute

Group data by one categorical attribute and calculate the average numerical values.

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

### Group By Multiple Attributes

Group data by multiple categorical attributes and calculate the average numerical values.

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

## 5. Pivot Tables

Pivot tables provide a better representation of grouped data based on selected parameters.

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

## 6. Pseudocolor Plot

A pseudocolor plot can be used to visualize the values in a pivot table.

The grouped attributes form the x-axis and y-axis, while the values are represented through color.

### Syntax

```python
plt.pcolor(
    grouped_pivot,
    cmap="RdBu"
)
```

### Example

```python
plt.pcolor(
    grouped_pivot,
    cmap="RdBu"
)

plt.colorbar()
plt.show()
```

---

## 7. Correlation

Correlation is a statistical measure that indicates how changes in one variable may be associated with changes in another variable.

### Complete DataFrame Correlation

Create a correlation matrix using all numerical attributes.

### Syntax

```python
df.corr()
```

### Example

```python
correlation = df.corr()

print(correlation)
```

### Specific Attribute Correlation

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

## 8. Pearson Correlation

Pearson correlation is used to measure the relationship between two continuous numerical variables.

It provides:

- **Pearson correlation coefficient** — indicates the strength and direction of the relationship
- **P-value** — indicates the certainty of the correlation

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

print("Pearson Correlation Coefficient:", pearson_coef)
print("P-value:", p_value)
```

---

## 9. Correlation and Regression Visualization

When exploring correlation between continuous variables, use a scatter plot together with a regression line.

```python
sns.regplot(
    x="engine-size",
    y="price",
    data=df
)

plt.show()
```

A correlation coefficient close to:

```text
+1
```

indicates a strong positive correlation.

A coefficient close to:

```text
-1
```

indicates a strong negative correlation.

A coefficient close to:

```text
0
```

suggests little or no correlation.

### P-Value

The p-value helps evaluate the statistical significance of the correlation.

As the p-value decreases, the evidence for statistical significance increases.

As the p-value increases, the evidence for statistical significance decreases.

```text
P-value decreases ↓
        |
        v
Evidence of significance increases ↑
```

```text
P-value increases ↑
        |
        v
Evidence of significance decreases ↓
```

Practical reference:

| P-Value | Evidence |
|---|---|
| `< 0.001` | Strong evidence |
| `< 0.05` | Moderate evidence |
| `< 0.10` | Weak evidence |
| `> 0.10` | No evidence of statistical significance |

Both the correlation coefficient and p-value should be considered when evaluating the relationship.

---

## 10. Heatmap

A heatmap provides a visual summary of the strength and direction of correlations among multiple numerical variables.

### Syntax

```python
sns.heatmap(
    df.corr()
)
```

### Example

```python
plt.figure(figsize=(10, 8))

sns.heatmap(
    df.corr(),
    annot=True
)

plt.show()
```

---

## Important Notes

### `%matplotlib inline`

`%matplotlib inline` is a Jupyter/IPython magic command used to display Matplotlib plots directly inside a notebook.

```python
%matplotlib inline
```

It is commonly used in Jupyter Notebook, JupyterLab, and similar IPython environments.

It is not standard Python syntax and is not required in a normal `.py` script.

In a standard Python script:

```python
import matplotlib.pyplot as plt

plt.show()
```

### `plt.ylim(0,)`

Sets the lower limit of the y-axis to `0` while allowing Matplotlib to determine the upper limit automatically.

```python
plt.ylim(0,)
```

This is optional and is useful when the y-axis should start at zero.

### `reset_index()`

`reset_index()` converts the existing DataFrame index into a normal column and creates a new default numeric index.

```python
df.reset_index(inplace=True)
```

When you do not want to keep the old index as a column:

```python
df.reset_index(
    drop=True,
    inplace=True
)
```

This is commonly useful after operations such as `value_counts()`, `groupby()`, filtering, or dropping rows.

---

## EDA Workflow

```text
Import Data
     ↓
Identify Variable Types
     ↓
Analyze Individual Features
     ↓
Continuous + Continuous
     ↓
Scatter Plot / Regression Plot
     ↓
Categorical + Continuous
     ↓
Box Plot
     ↓
Descriptive Statistics
     ↓
Group Data
     ↓
Create Pivot Tables
     ↓
Pseudocolor Plot
     ↓
Correlation Analysis
     ↓
Pearson Correlation
     ↓
Heatmap
     ↓
Identify Important Characteristics
```

Created by Guruvendra