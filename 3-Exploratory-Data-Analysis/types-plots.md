# Creating Different Types of Plots in Python

A reference guide for creating common data visualizations using **Matplotlib** and **Seaborn** in Python.

## Importing Libraries

### Matplotlib

```python
from matplotlib import pyplot as plt
```

Alternative:

```python
import matplotlib.pyplot as plt
```

For Jupyter Notebooks:

```python
%matplotlib inline
```

### Seaborn

```python
import seaborn as sns
```

# Matplotlib Plots

## 1. Line Plot

A line plot displays the relationship between two variables by connecting ordered data points with line segments.

### Syntax

```python
plt.plot(x, y)
```

### Example

```python
plt.plot(x, y)
```

- `x` represents the independent variable.
- `y` represents the dependent variable.

## 2. Scatter Plot

A scatter plot displays the relationship between two variables using individual data points.

It is useful for:

- Paired numerical data
- Multiple values of the dependent variable
- Studying relationships between variables

### Syntax

```python
plt.scatter(x, y)
```

### Example

```python
plt.scatter(x, y)
```

Additional arguments can be used to modify marker size, color, and shape.

## 3. Histogram

A histogram displays data in bins.

- The x-axis represents the bins.
- The y-axis represents the number of observations in each bin.

### Syntax

```python
plt.hist(x, bins)
```

### Example

```python
plt.hist(x, bins=5)
```

An `edgecolor` argument can be used to improve the visibility of the bins.

```python
plt.hist(
    x,
    bins=5,
    edgecolor="black"
)
```

## 4. Bar Plot

A bar plot is used to visualize categorical data.

- `x` represents the categories.
- `height` represents the number or value associated with each category.

### Syntax

```python
plt.bar(x, height)
```

### Example

```python
plt.bar(x, height)
```

The `width` argument can be used to adjust the width of the bars.

```python
plt.bar(
    x,
    height,
    width=0.5
)
```

## 5. Pseudocolor Plot

A pseudocolor plot displays matrix data as colored cells.

It can be used to visualize a pivot table where:

- The x-axis represents one grouping variable.
- The y-axis represents another grouping variable.
- The cell color represents the value in the pivot table.

### Syntax

```python
plt.pcolor(C)
```

### Example

```python
plt.pcolor(C)
```

A `cmap` argument can be used to specify the color scheme.

```python
plt.pcolor(
    C,
    cmap="RdBu"
)
```

# Seaborn Plots

## 6. Regression Plot

A regression plot creates a scatter plot and fits a regression line with a 95% confidence interval.

### Syntax

```python
sns.regplot(
    x="header_1",
    y="header_2",
    data=df
)
```

### Example

```python
sns.regplot(
    x="horsepower",
    y="price",
    data=df
)
```

## 7. Box and Whisker Plot

A box plot shows the distribution of quantitative data and is useful for comparing variables or categories.

The box represents the quartiles, while the whiskers represent the remaining distribution, excluding identified outliers.

The interquartile range (IQR) is the range between the 25th and 75th percentiles.

Outliers are generally identified as observations outside 1.5 times the interquartile range.

### Syntax

```python
sns.boxplot(
    x="header_1",
    y="header_2",
    data=df
)
```

### Example

```python
sns.boxplot(
    x="fuel-type",
    y="price",
    data=df
)
```

## 8. Residual Plot

A residual plot displays the residuals from a regression model.

Residuals are the differences between observed values and predicted values.

### Syntax

```python
sns.residplot(
    data=df,
    x="header_1",
    y="header_2"
)
```

### Alternative Syntax

```python
sns.residplot(
    x=df["header_1"],
    y=df["header_2"]
)
```

### Example

```python
sns.residplot(
    data=df,
    x="horsepower",
    y="price"
)
```

## 9. KDE Plot

A Kernel Density Estimate (KDE) plot displays a probability distribution curve based on the likelihood of values occurring.

It can be used to compare the distributions of actual and predicted data.

### Syntax

```python
sns.kdeplot(X)
```

### Example

```python
sns.kdeplot(X)
```

## 10. Distribution Plot

A distribution plot combines a histogram and KDE-style distribution curve.

The histogram can optionally be displayed or hidden.

### Syntax

```python
sns.distplot(
    X,
    hist=False
)
```

### Example

```python
sns.distplot(
    X,
    hist=False
)
```

To display the histogram:

```python
sns.distplot(
    X,
    hist=True
)
```

# Quick Reference

| Plot | Library | Syntax | Purpose |
|---|---|---|---|
| Line Plot | Matplotlib | `plt.plot(x, y)` | Show relationships or trends |
| Scatter Plot | Matplotlib | `plt.scatter(x, y)` | Show relationship between variables |
| Histogram | Matplotlib | `plt.hist(x, bins)` | Show distribution using bins |
| Bar Plot | Matplotlib | `plt.bar(x, height)` | Visualize categorical data |
| Pseudocolor Plot | Matplotlib | `plt.pcolor(C)` | Visualize matrix or pivot-table values |
| Regression Plot | Seaborn | `sns.regplot()` | Show regression relationship |
| Box Plot | Seaborn | `sns.boxplot()` | Compare distributions |
| Residual Plot | Seaborn | `sns.residplot()` | Evaluate regression residuals |
| KDE Plot | Seaborn | `sns.kdeplot(X)` | Show probability distribution |
| Distribution Plot | Seaborn | `sns.distplot(X)` | Combine histogram and distribution curve |

Created by Guruvendra