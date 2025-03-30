# Pandas **DataFrame**

Pandas' `DataFrame` is a powerful tool that allows us to store and manipulate data in a **structured** way, similar to an `Excel spreadsheet` or a `SQL Table`. A `DataFrame` is similar to a table with **rows** and **columns**. It helps in handling **large amounts of data**, **performing calculations**, **filtering information** with ease.

---

# Installing Required Library
- Install Pandas (*if not already installed* )

  - If Installing on `Google Colab`

  ```
  !pip install pandas
  ```

  - If Installing on `Command Prompt` or `Powershells` like of `VS Code`

  ```
  pip install pandas
  ```

---

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

<br />

# Creating an Empty DataFrame

- An empty `DataFrame` in **pandas** is a table with no data but can have defined **column** names and indexes. It is useful for setting up a structure before adding data dynamically. An empty `DataFrame` can be created just by calling a **dataframe constructor**.

```python
df = pd.DataFrame()
```

If you print `df`, following will be the output
> ```
>   Empty DataFrame
>   Columns: []
>   Index: []
> ```

# Creating a DataFrame from a List

- A simple way to create a `DataFrame` is by using a **single list**. **Pandas** automatically assigns index values to the **rows** when you pass a list.
  - Each item in the **list** becomes a **row**.
  -  The `DataFrame` consists of a single unnamed **column**.

```python
lst = ['Pandas', 'Library', 'Manipulates', 'Data', 'Faster', 'and', 'Efficiently']

df = pd.DataFrame(lst)
```

If you print `df`, following will be the output
> ```
>        0
> 0   Pandas
> 1     Library
> 2   Manipulates
> 3      Data
> 4  Faster
> 5     and
> 6   Efficiently
> ```

# Creating DataFrame from dict of Numpy Array

- We can create a **Pandas** `DataFrame` using a dictionary of **NumPy** arrays. Each key in the dictionary represents a **column** name and the corresponding **NumPy** array provides the values for that **column**.

```python
data = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
df = pd.DataFrame(data, columns=['A', 'B', 'C'])
```

If you print `df`, following will be the output
> ```
>    A  B  C
> 0  1  2  3
> 1  4  5  6
> 2  7  8  9
> ```

# Creating a DataFrame from a List of Dictionaries  

- We can also create `dataframe` using **List of Dictionaries**. It represents **data** where each dictionary corresponds to a **row**. This method is useful for handling structured data from `APIs` or `JSON` files. It is commonly used in **web scraping** and **API data processing** since `JSON` responses often contain **lists of dictionaries**.

```python
dict = {'name':["aparna", "pankaj", "sudhir", "Geeku"],
        'degree': ["MBA", "BCA", "M.Tech", "MBA"],
        'score':[90, 40, 80, 98]}

df = pd.DataFrame(dict)

```

If you print `df`, following will be the output
> ```
>      name  degree  score
> 0  aparna     MBA     90
> 1  pankaj     BCA     40
> 2  sudhir  M.Tech     80
> 3   Geeku     MBA     98
```
