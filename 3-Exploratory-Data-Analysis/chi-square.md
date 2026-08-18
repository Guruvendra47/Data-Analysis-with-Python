# Chi-Square Test for Categorical Variables

The Chi-Square test is a statistical method used to determine whether there is a significant association between two categorical variables.

It is commonly used in areas such as:

- Market Research
- Healthcare
- Social Sciences
- Education
- Quality Control

## Concept

The Chi-Square test compares:

- **Observed frequencies** — the actual values in each category
- **Expected frequencies** — the values expected when there is no association between the variables

The test uses the **Chi-Square distribution**, which varies according to the degrees of freedom (`df`).

## Null and Alternative Hypotheses

### Null Hypothesis (H₀)

There is **no association** between the categorical variables.

Any observed differences are due to random chance.

### Alternative Hypothesis (H₁)

There is a **significant association** between the categorical variables.

The observed differences are not due to chance alone.

## Chi-Square Formula

The Chi-Square statistic is:

```text
χ² = Σ (Oᵢ - Eᵢ)² / Eᵢ
```

Where:

- `Oᵢ` = Observed frequency
- `Eᵢ` = Expected frequency

## Expected Frequency

The expected frequency for each cell is calculated as:

```text
Expected Frequency =
(Row Total × Column Total) / Grand Total
```

## Degrees of Freedom

The degrees of freedom are:

```text
df = (r - 1) × (c - 1)
```

Where:

- `r` = Number of rows
- `c` = Number of columns

## Decision Rule

The calculated Chi-Square statistic can be compared with a critical value from the Chi-Square distribution table.

For example:

```text
df = 1
α = 0.05
Critical Value = 3.841
```

Decision:

```text
If χ² > 3.841
    Reject H₀

If χ² ≤ 3.841
    Fail to Reject H₀
```

A larger Chi-Square value provides stronger evidence against the null hypothesis.

# Python Implementation

Use Pandas and SciPy to perform the Chi-Square test.

```python
import pandas as pd
from scipy.stats import chi2_contingency
```

## Create a Contingency Table

```python
data = [
    [20, 30],  # Male: [Like, Dislike]
    [25, 25]   # Female: [Like, Dislike]
]

df = pd.DataFrame(
    data,
    columns=["Like", "Dislike"],
    index=["Male", "Female"]
)
```

## Perform the Chi-Square Test

```python
chi2, p, dof, expected = chi2_contingency(df)
```

## Display the Results

```python
print("Chi-square Statistic:", chi2)
print("Degrees of Freedom:", dof)
print("P-value:", p)
print("Expected Frequencies:\n", expected)
```

### Output

```text
Chi-square Statistic: 1.008
Degrees of Freedom: 1
P-value: 0.3156
Expected Frequencies:
[[22.5 27.5]
 [22.5 27.5]]
```

## Interpretation

The p-value is:

```text
0.3156
```

Since:

```text
0.3156 > 0.05
```

we **fail to reject H₀**.

This indicates that there is **no significant association** between gender and product preference in this sample.

# Practical Example: Weak Association

Suppose a researcher wants to determine whether there is an association between:

- Gender
- Product preference

The data is:

| Category | Like | Dislike | Total |
|---|---:|---:|---:|
| Male | 20 | 30 | 50 |
| Female | 25 | 25 | 50 |
| Total | 45 | 55 | 100 |

## Step 1: Calculate Expected Frequencies

### Male, Like

```text
E = (50 × 45) / 100
  = 22.5
```

### Male, Dislike

```text
E = (50 × 55) / 100
  = 27.5
```

### Female, Like

```text
E = (50 × 45) / 100
  = 22.5
```

### Female, Dislike

```text
E = (50 × 55) / 100
  = 27.5
```

## Step 2: Calculate Chi-Square Statistic

```text
χ² =
(20 - 22.5)² / 22.5
+
(30 - 27.5)² / 27.5
+
(25 - 22.5)² / 22.5
+
(25 - 27.5)² / 27.5
```

```text
χ² = 1.008
```

## Step 3: Calculate Degrees of Freedom

```text
df = (2 - 1) × (2 - 1)

df = 1
```

## Step 4: Interpret the Result

The critical value at:

```text
df = 1
α = 0.05
```

is approximately:

```text
3.841
```

Since:

```text
1.008 < 3.841
```

we **fail to reject H₀**.

There is no significant association between gender and product preference in this sample.

# Practical Example: Strong Association

Consider the relationship between:

- Smoking status
- Lung disease

The data is:

| Category | Disease | No Disease | Total |
|---|---:|---:|---:|
| Smoker | 50 | 30 | 80 |
| Non-Smoker | 20 | 100 | 120 |
| Total | 70 | 130 | 200 |

## Step 1: Calculate Expected Frequencies

### Smoker, Disease

```text
E = (80 × 70) / 200
  = 28
```

### Smoker, No Disease

```text
E = (80 × 130) / 200
  = 52
```

### Non-Smoker, Disease

```text
E = (120 × 70) / 200
  = 42
```

### Non-Smoker, No Disease

```text
E = (120 × 130) / 200
  = 78
```

## Step 2: Calculate Chi-Square Statistic

```text
χ² =
(50 - 28)² / 28
+
(30 - 52)² / 52
+
(20 - 42)² / 42
+
(100 - 78)² / 78
```

```text
χ² = 44.33
```

## Step 3: Calculate Degrees of Freedom

```text
df = (2 - 1) × (2 - 1)

df = 1
```

## Step 4: Interpret the Result

The critical value at:

```text
df = 1
α = 0.05
```

is approximately:

```text
3.841
```

Since:

```text
44.33 > 3.841
```

we **reject H₀**.

This indicates a significant association between smoking status and lung disease in this sample.

# Applications

## Market Research

Analyze associations between customer demographics and product preferences.

## Healthcare

Study relationships between patient characteristics and disease incidence.

## Social Sciences

Investigate relationships between social factors and behavioral outcomes.

## Education

Examine associations between teaching methods and student performance.

## Quality Control

Analyze relationships between manufacturing conditions and product defects.

# Summary

The Chi-Square test is used to determine whether two categorical variables are significantly associated.

The main steps are:

```text
Create Contingency Table
        ↓
Calculate Expected Frequencies
        ↓
Calculate χ²
        ↓
Calculate Degrees of Freedom
        ↓
Compare with Critical Value or P-value
        ↓
Interpret the Result
```

Created by Guruvendra