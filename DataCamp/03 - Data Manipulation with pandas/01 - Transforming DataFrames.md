# Data Manipulation with pandas

## Transforming DataFrames

1. Sorting and Sub-setting
2. Creating New Columns

### Introducing DataFrames

**What's the point in pandas ?**
-> Pandas is a Python package for data manipulation. It can also be used for -

1. Data Manipulation
2. Data Visualization

Pandas is built on top of two essential Python Packages, NumPy and Matplotlib.

Numpy provides multidimensional array objects for easy data manipulation that pandas uses to store data, and Matplotlib has powerful data visualization capabilities that pandas takes advantage of.

There are several ways to store data for analysis, but rectangular data, sometimes called "tabular data" is the most common form.

In pandas, rectangular data is represented as a DataFrame Object.

When you first receive a new dataset, you want to quickly explore it and get a sense of its contents. Pandas has several methods for this.

### Sorting and Sub-setting

### New Columns

However, often when you first receive a DataFrame, the contents aren't exactly what you want. You may have to add new columns derived from existing columns.

Creating and adding new columns can go by many names, including _mutating a DataFrame_, _transforming a DataFrame_, and _feature engineering_.

## Types of Functions

1. `df.head()` -
   1. [For More Information](../01%20-%20Introduction%20to%20Data%20Science%20in%20Python/02%20-%20Loading%20Data%20Into%20Pandas.md)
   2. The first is head, which returns the first few rows of the DataFrame.
   3. We only had seven rows to begin with, so it's not super exciting, but this becomes very useful if you have many rows.
2. `df.info()` -
   1. [For More Information](../01%20-%20Introduction%20to%20Data%20Science%20in%20Python/02%20-%20Loading%20Data%20Into%20Pandas.md)
   2. The info method displays the names of columns, the data types they contain, and whether they have any missing values.
3. `df.shape` -
   1. A DataFrame's shape attribute contains a tuple that holds the number of rows followed by the number of columns.
   2. Since this is an attribute instead of a method, you write it without parentheses.
4. `df.describe()` -
   1. The describe method computes some summary statistics for numerical columns, like mean and median.
   2. "count" is the number of non-missing values in each column.
   3. Describe is good for a quick overview of numeric variables, but if you want more control, you'll see how to perform more specific calculations later in the course.
5. `dogs.values` -
   1. Here dogs is a dataframe. It can be replaced with any df name.
   2. DataFrames consist of three different components, accessible using attributes.
   3. The values attribute, as you might expect, contains the data values in a 2-dimensional NumPy array.
6. `dogs.column` and `dogs.index` -
   1. The other two components of a DataFrame are labels for columns and rows.
   2. The columns attribute contains column names, and the index attribute contains row numbers or row names.
   3. Be careful, since row labels are stored in _dot-index_, not in dot-rows.
   4. Notice that these are Index objects.
   5. This allows for flexibility in labels.
7. `dogs.sort_values("weight_kg", ascending=False)` -
   1. Here dogs is the name of the dataframe, it can be replaced by anything.
   2. And `weight_kg` is a column of the that needs to be sorted.
   3. You can sort rows using the sort_values method, passing in a column name that you want to sort by.
   4. Setting the ascending argument to False will sort the data the other way around.
   5. We can sort by multiple columns by passing a list of column names to sort_values - `dogs.sort_values(["weight_kg","height_cm"])`.
   6. Above we sort first by weight then by height.
   7. To change the direction values are sorted in, we pass a list to the ascending argument to specify which direction sorting should be done for each variable.
   8. E.g - `dogs.sort_values(["weight_kg","height_cm"], ascending=[True, False])`.
8. Sub-setting Columns -

   1. `dogs['name']` -
      1. For a single column selection
   2. `dogs[['breed', 'height_cm']]` -

      1. It is used for selecting two or more columns.
      2. In this code, the inner and outer square brackets are performing different tasks.
      3. The outer square brackets are responsible for sub-setting the DataFrame.
      4. The inner square brackets are creating a list of column names to subset.
      5. This means that we can provide a separate list of columns names as a variable and then use that list to perform same sub-setting.
      6. E.g -

      ```python
      cols_to_subset = ['breed', 'height_cm']
      dogs[cols_to_subset]
      ```

9. Sub-setting Rows -

   1. There are lots of ways to subset rows. The most common way is to do this by creating a logical condition to filter against.
   2. E.g - Find all the dogs whose height is greater than 50cm -> `dogs['height_cm'] > 50`.
   3. We can use the logical condition inside the square brackets to subset the rows we're interested in to get all of the dogs taller than 50cm -> `dogs[dogs['height_cm' > 50]]`.
   4. We can also subset rows according to text data. Here we use the double equal (==) sign in the logical condition to filter the dogs that are Labradors -> `dogs[dogs['breed'] == 'Labrador']`.
   5. We can also subset rows based on dates. Here we filter the dogs born before 2015 -> `dogs[dogs['date_of_birth'] < '2015-01-01']`.
   6. Notice that the dates are in quotes and are written as _YY-MM-DD_. This is the international standard date form.
   7. To subset the rows that meet multiple conditions, you can combine conditions using logical operators, such as and operator seen here. This means that only rows that meet the both conditions will be subsetted.
   8. E.g -

   ```python
   is_lab = dogs["breed"] == "Labrador"
   is_brown = dogs["color"] == "Brown"
   dogs[is_lab & is_brown]
   ```

   9. We can also do this in one line of code, but you'll also need to add parenthesis around each condition.
   10. E.g- dogs[(dogs['breed'] == 'Labrador') & (dogs['color'] == 'Brown')]
   11. If you want to filter on multiple values of a categorical variable, the easiest way is to use the **isin** method.
   12. E.g - is_black_or_brown = `dogs['color'].isin(['Black', 'Brown'])`.
   13. This takes in a list of values to filter for.
   14. Here, we check if the color of a dog is black or brown, and use this condition to subset the data.

10. Adding New Column -
    1. Add a new column -> `dogs['height_m'] = dogs['height_cm'] / 100`.
    2. On the left-hand side of the equals, we use square brackets with the name of the new column we want to create.
    3. On the right-hand side, we have the calculation.
    4. Notice that both the existing column and the new column we just created are in the same DataFrame.
11. Multiple Manipulation -

    1. E.g - Figure out the names of skinny and tall dogs.
    2. E.g -

    ```python
      bmi_lt_100 = dogs[dogs['bmi'] < 100] # To get Skinny dogs
      bmi_lt_100_height = bmi_lt_100.sort_values('height_cm', ascending = False) # Gets tall and skinny dogs
      bmi_lt_100_height[['name', 'height_cm', 'bmi']] # Printing the columns that are only needed.
    ```
