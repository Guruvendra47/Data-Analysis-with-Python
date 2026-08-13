# Importing Datasets

A collection of notes covering the fundamentals of importing datasets in Python, reading data with Pandas, understanding data types, generating statistical summaries, and connecting Python to relational databases.

---

## Topics Covered

* Dataset Structure
* Python Libraries
* Importing CSV Files
* Pandas DataFrames
* Data Types
* Statistical Summary
* DataFrame Information
* Missing Values
* Database Connectivity
* SQL API
* Python DB-API

---

## Dataset Basics

* Each row in a dataset represents one record.
* Columns represent attributes (features).
* Values are typically separated by commas in CSV files.
* Understanding each column is important before performing analysis.

---

## Python Libraries

Python libraries provide pre-written functions and methods that reduce development time.

Common categories include:

* Scientific Computing
* Data Visualization
* Machine Learning

Popular libraries:

* NumPy
* Pandas
* Matplotlib
* SciPy
* Scikit-learn

> **Note:** Scikit-learn is built on top of NumPy, SciPy, and Matplotlib.

---

## Importing Data with Pandas

Two important factors when reading a dataset:

* File format
* File path

### Read CSV File

```python
import pandas as pd

df = pd.read_csv("data.csv")
```

---

## Pandas Data Types

Common data types include:

* object
* int
* float
* datetime

### Check Data Types

```python
df.dtypes
```

Knowing the correct data type helps apply appropriate Python operations and identify columns that may require conversion.

---

## Statistical Summary

Use the `describe()` method to generate summary statistics.

### Numerical Columns

```python
df.describe()
```

Returns:

* Count
* Mean
* Standard Deviation
* Minimum
* Maximum
* 25%
* 50%
* 75%

### All Columns

```python
df.describe(include="all")
```

Useful for both numerical and object-type columns.

---

## DataFrame Information

Display dataset information.

```python
df.info()
```

Provides:

* Number of rows
* Number of columns
* Column names
* Data types
* Non-null values
* Memory usage

Useful for quickly inspecting the dataset.

---

## Missing Values

Missing values are represented as:

```text
NaN
```

NaN indicates that a value is missing or unavailable, preventing some statistical calculations.

---

## Connecting Python to Databases

Python can connect to relational databases using database APIs.

Common approaches:

* SQL API
* Python DB-API

---

## SQL API

SQL APIs communicate with the Database Management System (DBMS) by:

* Opening a connection
* Creating SQL statements
* Sending SQL queries
* Receiving results
* Returning execution status

---

## Python DB-API

Python DB-API is the standard interface for interacting with relational databases.

Main objects:

### Connection Object

Used to establish and manage database connections.

Common methods:

```python
connection.cursor()

connection.commit()

connection.rollback()

connection.close()
```

### Cursor Object

Used to:

* Execute SQL queries
* Fetch records
* Navigate query results

---

## Database Connection Example

```python
import sqlite3

connection = sqlite3.connect("database.db")

cursor = connection.cursor()

cursor.execute("SELECT * FROM employees")

rows = cursor.fetchall()

connection.close()
```

---

## Key Takeaways

* Every dataset consists of rows and columns.
* Pandas is the standard library for importing datasets.
* Use `read_csv()` to load CSV files into a DataFrame.
* Check data types using `dtypes`.
* Generate summaries using `describe()`.
* Inspect datasets using `info()`.
* Missing values are represented as `NaN`.
* Python connects to databases using SQL APIs or the Python DB-API.
* Always close database connections after completing operations.
