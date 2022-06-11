# Introduction to Data Science in Python

## Loading Data In Pandas

**What is Pandas ?**

`Pandas` is a module for working with tabular data, or data that has rows and columns.

**What can pandas do for you?**

1. Loading Tabular data from different sources (like spreadsheets or databases).
2. Search for particular rows or columns in your loaded data.
3. Calculate aggregate statistics (like averages or standard deviations), and combine data from multiple sources.

**DataFrame** -

1. Pandas introduces a new, more powerful data type: the **DataFrame** which represents tabular data.
2. Loading the data into a DataFrame is the first step in using Pandas.
3. One of the easiest way to create a DataFrame is by using a _CSV_ file.

**CSV** stands for `Comma Separated Values`, and is a common way of storing tabular data as a text-only file.

We can download `CSV` version of data from an `Excel Spreadsheet`, a `SQL Database`, or a `Google Sheet`.

### Working With Pandas

1. Importing Pandas
2. Loading a CSV

**Importing Pandas** -

`import pandas as pd`

**Loading a CSV** -

Here we load the _CSV_ file _ransom.txt_ in the df variable of DataFrame type.

```python
df = pd.read_csv('ransom.txt')
print(df)
# When you print a DataFrame you get to see the df.
```

## Selecting Columns

The first way to select data is by selecting columns.

**Why to select columns ?**

1. We might use them in calculation -> This code selects the column `price` and then calls the method `sum` to get the total amount of money spent by the suspects.
   E.g- `credit_records.price.sum()`
2. We might also want to use the data as a input to a function.
   E.g - **Plot Data** -> `plt.plot(ransom['letters'], ransom['frequency'])` -> It will create a plot of frequencies of each letter in the ransom note.

**How to Select Columns ?**

1. We can use these column name string to select a column. We store the data of a given column in a variable.
   E.g-

   ```python
   suspect = credit_records['suspect']
   print(suspect)
   # Printing suspect will give us the all the values present in the suspect column of credit_records dataframe.
   ```

2. Selecting with a Dot -

   1. If the columns notation contains letters, numbers, and underscores, we can use the dot notation.
   2. For dot natation we simply type the name of the variable, followed bhy the dot (.), followed by the name of the column.
      E.g-

   ```python
    price = credit_records.price
   ```

**Common Mistakes in Column Selection** -

1. Use brackets and strings for column name with spaces and special characters (`-`, `?` ,etc.).
   E.g- `police_report['Is Golden Retriever']` - **Correct** Way,
   `police_report.Is Golden Retriever` - **Wrong** Way.
2. Another common error is forgetting the quotation marks around the column string when using brackets and string notation.
3. Square brackets are not the same as parentheses, else python will give you a `TypeError`.

## Selecting Rows with Logic

1. We use logical statements to select the rows which give out true result.
2. In python for selecting rows we use the _boolean_ data type, we use signs to compare such as `>, <, >=, <=, ==, !=, etc.`
3. If we put that truth testing statement inside of brackets, we select only the rows where the statement is true.
   E.g-
   `credit_records[credit_records.price > 20.00]` -> Here we select the rows of credit_records where the price is greater than 20 dollars.
4. Here `credit_records` is the dataframe name, and the `credit_records.price > 20.00` is the logical statement.
5. We start with the name of the dataframe we want to select rows from, in this case it is _credit_records_.
6. Next we have a set of square brackets `[]`. Inside the square brackets we put our logical test.
7. In this case the logical test is whether the `price` column of `credit records` is greater than `$20`.
8. The statement will select all the rows of `credit_records` where column price is greater than `$20`.

## Types of Functions

`Rather than beginning of a line of a code, this function` **belongs** `to DataFrame variable and comes at the end of the line, after a period(.).We call this type of function a` **Method**.

1. `df.head()` ->
   1. Usually we don't want to print the entire _DataFrame_ to inspect it, we just want the first few lines.
   2. We do this by using **head**. Head behaves slightly differently.
   3. `The head method just selects the first five rows of DataFrame(df)`.
   4. In order to view it we need to put the `df.head()` method inside `print()` function.
2. `df.info()` ->
   1. In order to display the output we put the whole statement inside the `print()` function.
   2. We can see the **Number of Rows**, **Number of Columns** and the **DataTypes of each Column.**.
   3. This method is particularly useful for _DataFrames_ with many columns that are difficult to display using `df.head()`.
