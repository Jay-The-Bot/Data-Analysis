# Joining Data with pandas

## Merging Ordered and Time-Series Data

### Using merge_ordered()

This method can merge time-series and other ordered data.

The merge_ordered method will allows us to merge the left and right DataFrames as shown in the Image.
![Merge Ordered](Images/Img%20-%209.png)

We can see the output of the merge when we merge on the 'C' column. The results are similar to the standard merge method with a outer join, but the results are sorted.

The sorted results make this a useful method for ordered or time-series data.

They both contain arguments to allow us to merge two DataFrames on different columns. Both Methods support different types of joins. Both methods support suffixes for overlapping the column names. However, how you call the methods is different.

| .merge() method                                | .merge_ordered() method                   |
| ---------------------------------------------- | ----------------------------------------- |
| Column(s) to join on -                         | Column(s) to join on -                    |
| 1. on                                          | 1. on                                     |
| 2. left_on                                     | 2. left_on                                |
| 3. right_on                                    | 3. right_on                               |
| Types of Join -                                | Types of Join -                           |
| 1. how(_left_, _right_, _inner_, _outer_){{@}} | 1. how(_left_, _right_, _inner_, _outer_) |
| 2. default **inner**                           | 2. default **outer**                      |
| Overlapping Column Names                       | Overlapping Column Names                  |
| 1. suffixes                                    | 1. suffixes                               |
| Calling the Method                             | Calling the function                      |
| 1. df1.merge(df2)                              | 1. pd.merge_ordered(df1, df2)             |

**Forward Fill** -

1. We can fill the missing data using a technique called Forward Filling.
2. It interpolate the missing data by filling the missing values with the previous value.
3. E.g - ![Forward Fill](Images/Img%20-%2010.png)
4. In this DataFrame shown here, the second and the fourth rows of the column B are filled with the values of B in the rows proceeding them.

Q. When to use merge_ordered() ?
-> You might think about using the merge_ordered method instead of the regular merge method when you are working with order or time-series data in our example. Additionally, the fill forward method is useful for handling missing data, as most machine learning algorithms require that there are no missing value.

### Using merge_asof()

.merge_asof() is another method for merging ordered and time-series data.

The merge_asof() method is similar to an ordered left join. It has similar features as merge ordered. However, unlike a ordered left join, merge_asof() will match on the nearest value columns rather than equal values. This brings up an important point - whatever columns you merge must be sorted.

E.g - ![Merge Asof](Images/Img%20-%2011.png)

In the DataFrame shown here, when we merge on column 'C', we bring back all the rows from the left DataFrame. However, the row selected in the right DataFrame is the last row whose 'C' value is less than or equal to 'C' value in the left DataFrame.

So, for example, the second row in the left DataFrame is matched with hte third row in the right DataFrame. This is because 3 is the closest value in the right DataFrame that is still less than or equal to 5.

Q. When to use merge_asof() ?
-> Data Sampled from a process. Developing a training set(no leakage). First, you might think of this method when you are working with data sampled from a process and the dates or times may not exactly align. This is similar to what we did in our example. It could also be used when you are working on a time-series training set, where you do not want any events from the future to be visible before that point in time.

![Summary](Images/Img%20-%2012.png)

### Selecting data with .query()

Let's review a pandas method for selecting data from the DataFrame called the query() method. Pandas provides many methods for selecting data, and query() is one of them.

The query() method accepts an input string that it will use to select rows to return from the DataFrame. For those familiar with SQL, the string you provide to the query function is similar to the portion after the _WHERE_ clause of a SQL statement.

- Accepts an input String
  - Input string used to determine what rows are returned.
  - Input statement similar to statement after _WHERE_ clause in _SQL_ statement.
    - Prior Knowledge of SQL not necessary.

### Reshaping data with .melt()

This method will unpivot a DataFrame from wide to long format. This is often much more computer friendly making this a valuable method to know.

In general, wide formatted data is easier to read by people than long formatted. However, long formatted data is often more accessible for computers to work with.

The melt method will allow us to unpivot, or change the format of our dataset.

## Types of Functions -

1. `pd.merge_concat(appl, mcd, on='data', suffixes=('_aapl', '_mcd'))` -
   1. The first two arguments are the left and right DataFrames.
   2. We set the _on_ argument equal to date.
   3. Finally, we set the suffixes argument to determine which DataFrame the data originated.
   4. This result in a result is sorted by date.
2. `pd.merge_concat(appl, mcd, on='data', suffixes=('_aapl', '_mcd'), fill_method-'ffill')` -
   1. We now set the fill_method argument to 'ffill' for forward fill.
   2. In the result, notice that the missing value for the last row is filled with in row before it.
   3. Notice, that the missing value for Apple(E.g) in the first row is still missing since there isn't a row before the first row to copy the missing value for Apple.
3. `gdp_returns.corr()` -
   1. Use the .corr() method on a DataFrame to compute the correlation matrix.
4. `pd.merge_asof(visa, ibm, on='date_time', suffixes=('\_visa', '\_ibm'))` -
   1. The input arguments are very similar to that of other merges.
   2. Here we list the left and the right DataFrame first.
   3. Then we want to merge on the 'date_time' column.
   4. Finally, we provide a set of suffixes.
   5. Our output is similar to a left join so we see all of the rows from the left Visa DataFrame.
   6. However, the values from the IBM DataFrame are based on how close the date_time values match with the VISA DataFrame.
   7. E.g - `pd.merge_asof(visa, ibm, on='date_time', suffixes=('\_visa', '\_ibm', direction='forward))`
   8. This time in our merge asof() method, we list the direction argument as _\_forward_.
   9. This will change the behavior of the method to select the first row in the right DataFrame whose 'on' key column is greater than or equal to the left's key column.
   10. The default value of the direction argument is _backward_.
   11. Finally, we can set the _direction_ argument to _nearest_ which returns the nearest row in the right DataFrame regardless if it is forward or backwards.
5. stocks.query('nike>=90') -
   1. The string identifies that what we want to condition which rows are returned by the value of nike column.
   2. The method returns all rows in stocks where Nike is greater than equal to 90.
   3. E.g - `stocks.query('nike > 90 and disney < 140')`
   4. We can also select strings.
   5. E.g - `stocks_long.query('stock == "disney" or (stock == "nike" and close < 90)')`
6. `social_fin_tall = social_fin.melt(id_vars=['financial', 'company'])` -

   1. The first input argument to the method is id vars. These are _\_columns_ to be used as identifier variables.
   2. We can also think of them as columns in our original dataset that we do not want to change.
   3. This time lets use the argument _value_vars_ with the melt() method.
   4. E.g - `social_fin_tall = social_fin.melt(id_vars=['financial', 'company'], value_vars=['2018', '2017'])`
   5. This argument allows is to control which arguments are unpivoted.
   6. Here we unpivot only the 2017 and 2018 columns.
   7. Our output now only has data for the years 2018 and 2017.
   8. Additionally, the order of the _value_var_ was kept.
   9. The output starts with 2018 and then moves to 2017.
   10. E.g - `social_fin_tall = social_fin.melt(id_vars=['financial', 'company'], value_vars=['2018', '2017'], var_name=['year'], value_name='dollars')`
   11. The var_name argument will allow us to set the name of the year column in the output.
   12. Similarly, the value_name will allow us to set the name of the value column in the output.
