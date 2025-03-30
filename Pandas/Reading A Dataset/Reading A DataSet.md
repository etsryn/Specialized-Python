# Reading Datasets in Different File Formats

> #### When working with data, we often encounter datasets stored in various file formats. Python provides multiple libraries to efficiently read and process these files. Among them, **Pandas** is one of the most widely used libraries for handling structured data.

> #### `Pandas` offers built-in functions to read and write datasets in different formats, including **Excel** (`.xlsx`), **CSV** (`.csv`), **JSON** (`.json`), **TSV** (`.tsv`), **Parquet** (`.parquet`), and more. This guide covers how to work with these file formats effectively.

---

# Installing Required Libraries
- Install Pandas (*if not already installed* )
  - If Installing on `Google Colab`
    - `!pip install pandas`
  - If Installing on `Command Prompt` or `Powershells` like of `VS Code`
    - `pip install pandas`

```
!pip install pandas
```

- Install OpenPyXL (*if not already installed* )
  - If Installing on `Google Colab`
    - `!pip install openpyxl`
  - If Installing on `Command Prompt` or `Powershells` like of `VS Code`
    - `pip install openpyxl`

```
!pip install openpyxl
```

# Importing Required Library

```
import pandas as pd
```

### What's `as pd` ?

- This assigns the **alias** `pd` to the **Pandas library**
- Instead of writing `pandas.function_name()`, you can simply use `pd.function_name()`
- It reduces typing effort and improves code readability
- **Industry Standard:** Almost all Python developers use pd as the alias
- **Saves Time:** Instead of writing `pandas.DataFrame()`, we write `pd.DataFrame()`
- **Improves Readability:** Shortens code while keeping it understandable

# Reading Excel (`.xlsx`) File

- Pandas provides the `read_excel()` function to load Excel files

```python
df = pd.read_excel("data.xlsx", engine="openpyxl")
```

> The `engine="openpyxl"` parameter ensures compatibility with `.xlsx` files although it is optional to use

> Pandas can automatically detect and use openpyxl if it is installed, if you simply run

```python
df = pd.read_excel("data.xlsx")
```

> Pandas will internally select `openpyxl` as the engine by default if the file format is `.xlsx`

### When Should You Explicitly Use engine="openpyxl"?

- To Avoid Compatibility Issues:

  - If multiple engines (`xlrd`, `openpyxl`, `odf`) are installed, explicitly specifying `engine="openpyxl"` ensures Pandas does not default to an incompatible engine

- Older Pandas Versions (`Before 1.2.0`):

  - Before `Pandas v1.2.0`, `xlrd` was used for `.xlsx` files, but newer versions of `xlrd` dropped support for `.xlsx`

- In such cases, explicitly setting `engine="openpyxl"` avoids errors

- Writing `.xlsx` Files (`to_excel()` method):

If you want to write an Excel file, specifying `engine="openpyxl"` ensures proper formatting:

```
df.to_excel("output.xlsx", engine="openpyxl")
```

## Final Recommendation
- If only working with `.xlsx`, you can **omit** `engine="openpyxl"` if openpyxl is installed.

- If dealing with multiple formats or ensuring compatibility, explicitly specify `engine="openpyxl"` to avoid unexpected issues.

## Reading Specific Sheets from an Excel File
- Use `sheet_name` to specify which sheet to read

```python
df = pd.read_excel("data.xlsx", sheet_name="Sheet1", engine="openpyxl")
```

## Reading Multiple Sheets into a Dictionary of DataFrames
- This will load all sheets into a `dictionary` where `keys` are `sheet names`

```python
dfs = pd.read_excel("data.xlsx", sheet_name=None, engine="openpyxl")
```

---

# Reading (`.csv`) File

- Pandas provides the `read_csv()` function to load **CSV** Files

```python
df = pd.read_csv("data.csv")
```

### Reading **CSV** with Custom Delimiters
> Semicolon-separated file

```python
df = pd.read_csv("data.csv", delimiter=";")
```

### Understanding **delimiter** in `pd.read_csv()`

- The delimiter parameter in `pd.read_csv()` is used to specify the character that separates values in a CSV file. By default, CSV files are **comma-separated** (`delimiter=","`), but sometimes, data might be separated by other characters like **semicolons** (`;`), **tabs** (`\t`), or **pipes** (`|`)

### How It Works?

- `pd.read_csv("data.csv")` assumes that the default separator is a **comma** (`,`)

- If the data uses **semicolons** (`;`) instead of commas to separate values, Pandas will misinterpret it as a `single-column dataset`

- The `delimiter=";"` argument tells Pandas to correctly **split columns based on semicolons**

### Example Dataset (`data.csv` with `;` as delimiter)
- Contents of `data.csv` (Incorrect Interpretation without delimiter)

```
Name;Age;Country
Alice;25;USA
Bob;30;UK
Charlie;28;Canada
```

-  If we load this without specifying the delimiter:

```
df = pd.read_csv("data.csv")  # Default delimiter is ","
```

-  Incorrect Reading
> Pandas reads the entire row as a single column because it expected `,` but found `;` instead!

```
        Name;Age;Country
0     Alice;25;USA
1       Bob;30;UK
2  Charlie;28;Canada
```

- Correcting It Using delimiter=";"

```
df = pd.read_csv("data.csv", delimiter=";")
```
- Correct Output:
> Now, Pandas correctly splits the columns based on `;` instead of treating the entire row as one value

```
     Name  Age Country
0   Alice   25     USA
1     Bob   30      UK
2  Charlie   28  Canada
```

## Other Common Delimiters:

| Delimiter        | Example Usage                                     |
|------------------|---------------------------------------------------|
| Comma (`,`)      | Default separator in CSV files                    |
| Semicolon (`;`)  | Used in some European datasets                    |
| Tab (`\t`)       | Often used in `.tsv` (Tab-Separated Values) files |
| Pipe (`|`)       | Used in logs or structured text formats           |

### Summary
> The delimiter parameter ensures Pandas correctly interprets different column separators

> Use `delimiter=";"` if your dataset uses semicolons instead of commas

> Helps when working with `European CSVs`, `log files`, or `custom-formatted data`

---

# Reading `.json` File
- Pandas provides the `read_json()` function to load **CSV** Files

```python
df = pd.read_json("data.json")
```

- Sometimes it needs additional parameters depending on the structure of the **JSON** file

|Parameter      | Description |
|---------------|-------------|
| orient        | Defines JSON structure (e.g., "records", "columns", "index", "split")        |
| lines         |	If True, reads JSON where each line is a separate record (useful for large datasets) |
| dtype         |	Specifies data types for each column |
| convert_dates |	Automatically converts date columns |

---

# Reading `.parquet` or .`pqt` Files

Install Required Library

```
!pip install pyarrow
```

# Reading a Parquet File:

```python
df = pd.read_parquet("data.parquet")
```
