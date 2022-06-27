# Data Manipulation with pandas

## Aggregating DataFrames

1. Summary Statistics
2. Counting
3. Grouped Summary Statistics

### Summary Statistics

In this chapter, we'll talk about aggregating data, starting with summary statistics. Summary statistics, as follows from their name, are numbers that summarize and tell you about your dataset.

There are lots of summary statistics that we can calculate on _columns_. Such as ->

1. `.mean()`
2. `.median()`
3. `.mode()`
4. `.min()`
5. `.max()`
6. `.var()` -> Variance
7. `.std()` -> Standard Deviation
8. `.sum()`
9. `.quantile()` -> Quantile calculation

We can also get the summary statistics for the date columns.

For calculating the oldest we need to use the `.min()`, and for the youngest we use `.max()`.

**The .agg() method** -

> The aggregate, or agg, method allows you to compute custom summary statistics.

Here, we create a function called pct30 that computes the thirtieth percentile of a DataFrame column.

The function takes in a column and returns out the column's thirtieth percentile. Now we can subset the weight column and call dot-agg, passing in the name of our function, pct30. It gives us the thirtieth percentile of the dogs' weights.

We can also use .agg to get multiple summary statistics at once.

Pandas has also methods for computing cumulative statistics, E.g - the cumulative sum. pandas also has methods for other cumulative statistics, such as the cumulative maximum, cumulative minimum, and the cumulative product. These all return an entire column of a DataFrame, rather than a single number.

E.g -

```python
# Definition of the function
def pct30(column):
  return column.quantile(0.3)

# Another similar definition
def pct40(column):
  return column.quartile(0.4)

# Calling the function
dogs['weight_kg'].add(pct30) # Single Column Call
dogs[['weight_kg', 'height_cm']].agg(pct30) # Multiple Column Call
dogs['weight_kg'].agg([pct30, pct40]) # Single Column Multiple Statistics Call
```

### Counting

You'll learn how to summarize categorical data using counting.

### Grouped summary statistics

Summary statistics for all rows of a dataset, but summary statistics can be useful to compare different groups.
While computing summary statistics of entire columns may be useful, you can gain many insights from summaries of individual groups.

Just like with ungrouped summary statistics, we can use the agg method to get multiple statistics.
Here, we pass a list of functions into agg after grouping by color.

You can also group by multiple columns and aggregate by multiple columns.

### Pivot Tables

Pivot tables are another way of calculating grouped summary statistics.

`dogs.groupby('color')['weight_kg'].mean()` -> this command can also be written as ->
`dogs.pivot_table(values='weight_kg', index='color')`.

## Types of Functions -

1. `dogs['height_cm'].mean()` -
   1. One of the most common summary statistics for numeric data is the mean, which is one way of telling you where the "center" of your data is.
   2. You can calculate the mean of a column by selecting the column with square brackets and calling dot-mean.
2. `dogs['weight_kg'].cumsum()` -
   1. Pandas also has methods for computing cumulative statistics, for example, the cumulative sum.
   2. Calling cumsum on a column returns not just one number, but a number for each row of the DataFrame.
   3. The first number returned, or the number in the zeroth index, is the first dog's weight.
   4. The next number is the sum of the first and second dogs' weights.
   5. The third number is the sum of the first, second, and third dogs' weights, and so on.
   6. The last number is the sum of all the dogs' weights.
3. Other methods same as (2) -
   1. `.cummax()`
   2. `.cummin()`
   3. `.cumprod()`
4. `vet_visits.drop_duplicates(subset='name')` -
   1. We'll extract a dog with each name from the dataset once.
   2. We can do this using the drop_duplicates method.
   3. It takes an argument, subset, which is the column we want to find our duplicates based on - in this case, we want all the unique names.
   4. Now we have a list of dogs where each one appears once.
   5. Because we have two different dogs with same name, we'll need to consider more than just name when dropping the duplicates.
   6. E.g - `vet_visits.drop_duplicates(subset=['name', 'breed'])`
5. `unique_dogs['breed].value_counts()` -
   1. To count the dogs of each breed, we'll subset the breed column and use the value_counts method.
   2. We can also use the sort argument to get the breeds with the biggest counts on top.
   3. E.g - `unique_dogs['breed].value_counts(sort=True)`.
   4. The normalize argument can be used to turn the counts into proportions of the total.
   5. E.g - `unique_dogs['breed].value_counts(normalize=True)`.
6. `dogs.groupby('color')['weight_kg'].mean()` -
   1. That's where the groupby method comes in.
   2. We can group by the color variable, select the weight column, and take the mean.
   3. This will give us the mean weight for each dog color.
   4. E.g - `dogs.groupby('color')['weight_kg'].agg([min, max, sum])`
   5. This gives us the minimum, maximum, and sum of the different colored dogs' weights.
   6. We can also group by multiple column and calculate summary statistics.
   7. E.g - `dogs.group_by(['color', 'breed'])['weight_kg'].mean()`.
   8. Here, we group by color and breed, select the weight column and take the mean.
   9. This gives us the mean weight of each breed of each color.
7. `dogs.pivot_table(values='weight_kg', index='color')` -
   1. The values argument is the one that you want to summarize.
   2. And the index column that you want to group by.
   3. By default, pivot table takes the mean value for each group.
   4. If we want a different summary statistic, we can use the aggfunc argument and pass it a function.
   5. E.g - `dogs.pivot_table(values='weight_kg', index='color', aggfunc = np.median)`
   6. Here, we take the median for each dog color using NumPy's median function.
   7. To get multiple summary statistics at a time, we can pass a list of functions to the aggfunc argument.
   8. E.g - `dogs.pivot_table(values='weight_kg', index='color', aggfunc = [np.mean, np.median])`
   9. Here, we get the mean and median for each dog color.
   10. To group by two variables, we can pass a second variable name into the columns argument.
   11. E.g - `dogs.pivot_table(values='weight_kg', index='color', column='breed')`
   12. While the result looks a little different than what we had before, it contains the same numbers.
   13. Instead of having lots of missing values, we can have them filled in using fill_value argument.
   14. E.g - `dogs.pivot_table(values='weight_kg', index='color', column='breed', fill_value=0)`.
   15. Here all the NaN get filled in with the zeros.
   16. If we set the margins argument to True, the last row and last column of the pivot table contain the mean of all the values in the column or row, not including the missing values that were filled in with Os.
   17. E.g - `dogs.pivot_table(values='weight_kg', index='color', column='breed', fill_value=0, margins=True)`.
