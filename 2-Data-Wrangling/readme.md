# Data Analysis and Visualization

A summary of key statistical analysis and visualization techniques used to explore relationships, distributions, and correlations in data.

## Statistical Summary

Use Pandas `describe()` to quickly calculate important statistical measures for numerical variables.

### Syntax

```python
df.describe()
```

Provides measures such as:

- Mean
- Standard deviation
- Minimum
- Quartiles
- Maximum

## Categorical Data

Use `value_counts()` to summarize categorical data into different categories.

### Syntax

```python
df["column"].value_counts()
```

### Example

```python
df["fuel-type"].value_counts()
```

## Box Plot

A box plot provides a visual representation of the distribution of numerical data.

It shows:

- Median
- Quartiles
- Outliers

### Syntax

```python
sns.boxplot(
    x="column",
    y="column",
    data=df
)
```

## Scatter Plot

Scatter plots are useful for exploring relationships between continuous variables.

For example:

- Engine size
- Price

### Syntax

```python
plt.scatter(x, y)
```

### Example

```python
plt.scatter(
    df["engine-size"],
    df["price"]
)
```

## GroupBy

Use Pandas `groupby()` to explore relationships between categorical variables.

### Syntax

```python
df.groupby("column")
```

### Example

```python
df.groupby("fuel-type").mean()
```

## Pivot Tables

Pivot tables can be used to summarize relationships between variables and support data visualization.

### Syntax

```python
df.pivot_table(
    values="value",
    index="row",
    columns="column"
)
```

## Heatmaps

Heatmaps provide a visual summary of relationships and correlation values between multiple variables.

### Syntax

```python
sns.heatmap(data)
```

## Correlation

Correlation is a statistical measure that indicates how changes in one variable may be associated with changes in another variable.

Correlation can be explored using:

- Scatter plots
- Regression lines
- Pearson correlation
- Heatmaps

## Regression Plot

A scatter plot combined with a regression line can be used to visualize relationships between continuous variables.

Seaborn's `regplot()` is useful for exploring correlation.

### Syntax

```python
sns.regplot(
    x="column1",
    y="column2",
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
```

## Pearson Correlation

Pearson correlation is used to assess the correlation between continuous numerical variables.

It provides two important values:

- **Correlation coefficient** — indicates the strength and direction of the relationship.
- **P-value** — indicates the certainty of the correlation.

### Correlation Coefficient

A coefficient close to:

```text
+1  → Strong positive correlation
-1  → Strong negative correlation
 0  → Little or no correlation
```

## P-value

P-values help assess the certainty of the correlation.

```text
P-value < 0.001
```

indicates strong certainty in the correlation.

Larger P-values indicate less certainty.

Both the correlation coefficient and P-value are important when evaluating correlation.

## Heatmap for Correlation

A heatmap provides a comprehensive visual summary of the strength and direction of correlations among multiple variables.

### Syntax

```python
sns.heatmap(
    df.corr()
)
```

## Analysis Workflow

```text
Statistical Summary
        ↓
Categorical Analysis
        ↓
Distribution Analysis
        ↓
Scatter Plots
        ↓
GroupBy / Pivot Tables
        ↓
Correlation Analysis
        ↓
Regression Plot
        ↓
Heatmap
```

Created by Guruvendra