# Data Manipulation with pandas

## Slicing and Indexing DataFrames

1. Subsetting using slicing
2. Indexes and subsetting using index's.

### Explicit indexes

You may be wondering why you should bother with indexes. The answer is that it makes subsetting code cleaner.

Indexes are controversial.

Although they simplify subsetting code, there are some downsides ->

1. Index values are just data.
2. Storing data in multiple forms makes it difficult to think about.
3. Indexes violate _tidy data_ principles. There is a concept called _tidy data_, where the data is stored in a tabular form - like a DataFrame.
4. Each row contains a single observation, and each variable is stored in its own column.
5. Indexes violate the last rule since index values don't get their own column.
6. In pandas, the syntax for working with indexes is different from the syntax for working with columns.
7. By using 2 syntaxes, your code is more complected, which can result in more bugs.
8. If you decide that you don't want to use indexes, that's perfectly reasonable. However, it's useful to know how they work for the cases when you need to read other people's code.

### Slicing and subsetting with .loc and .iloc

An important use of slicing is to subset dataframes by a range of dates. To demonstrate, this lets set the date_of_birth column as the index and sort by this index.

```python
dogs = dogs.set_index('date_of_birth').sort_index()
print(dogs)
# Get dogs with date_of_birth between 2014-08-05 and 2016-09-16
dogs.loc["2014-08-05" : "2016-09-16"]
dogs.loc["2014" : "2016"]
```

You slice dates with the same syntax as other types. The first and last dates are passed as strings. One helpful feature is that you can slice by partial dates.

Pandas interprets this as slicing from the start of 2014 to the end of 2016; that is all dates in 2014, 2015, 2016.

We can also slice the dataframe by row and column by using the row / column number using the iloc method.
E.g - `print(dogs.iloc[2:5, 1:4])`.

This uses a similar syntax to slicing list, except that there are 2 arguments: one for rows and one for columns.
Notice that, like list slicing but unlike loc, the final values aren't included in slice.

In above example the 5th row and the 4th column aren't included.

### Working with pivot tables

Recall that you create a pivot table by calling dot-pivot_table -

1. The first argument is the column name containing values to aggregate.
2. The index argument lists the columns to group by and display in rows, and the columns argument lists the columns to group by and display in columns.
3. We'll use the default aggregation function, which is mean.

> Pivot tables are just DataFrames with sorted indexes.

## Types of Functions -

1. `dogs_ind = dogs.set_index('name')` -
   1. You can move a column from the body of the DataFrame to the index.
   2. This is called "setting an index," and it uses the set_index method.
   3. A quick visual clue that name is now in the index is that the index values are left-aligned rather than right-aligned.
   4. Here _dogs_ind_ is the name of the new dataframe, which is derived from dataframe dogs.
   5. The values in the index don't need to be unique.
   6. Now, if you subset on "labrador" by -> `dogs_ind2.loc["labrador"]`, all the labrador data is returned.
   7. You can include multiple columns in the .set_index(), by passing a list of column names to set_index.
   8. E.g - `dogs_ind3 = dogs.set_index(['breed', 'color'])`.
   9. Here, breed and color are included.
   10. These are called multi-level indexes, or hierarchical indexes: the terms are synonymous.
   11. There is an implication here that the inner level of index, in this case, color, is nested inside the outer level, breed.
   12. To take a subset of a outer level index, you pass a list of values to loc.
   13. E.g - `dogs_ind3.loc[['Labrador', 'Chihuahua']]`.
   14. Here the list contains Labrador and Chihuahua, and the resulting subset contains all dogs from both breeds.
   15. To subset on inner levels, you need to pass a list of tuples.
   16. E.g - `dogs_ind3.loc[[('Labrador', 'Brown'), ('Chihuahua', 'Tan')]]`.
   17. Here the first tuple specifies Labrador at the outer level and Brown at the inner level. THe resulting rows have to match all conditions from the tuples.
2. `dogs_ind.reset_index()` -
   1. To undo what you just did, you can reset the index - that is, you remove it.
   2. This is done via reset_index.
   3. reset_index has a drop argument that allows you to discard an index.
   4. E.g - `dogs_ind.reset_index(drop=True)`.
   5. Here, setting drop to True entirely removes the dog names.
3. `dogs_ind3.sort_index()` -
   1. We can also sort the index values using sort_index.
   2. By default, ir sorts all the index levels from outer to inner, in ascending order.
   3. We can control the sorting by passing list to the level and ascending arguments.
   4. E.g - `dogs_ind3.sort_index(level=['color', 'breed'], ascending=[True, False])`.
4. Slicing List -

   1. [For More Information](../02%20-%20Intermediate%20Python/02%20-%20Dictionaries%20&%20Pandas.md)
   2. Slicing is a technique for selecting consecutive elements from objects.
   3. E.g -

      ```python
      breeds = ["Labrador", "Poodle", "Chow Chow", "Schnauzer", "Labrador", "Chihuahua", "St. Bernard"]
      breeds[2:5]
      # Output ->
      # ['Chow Chow', 'Schnauzer', 'Labrador']
      ```

   4. To slice a list, you pass first and last positions separated by a colon into square brackets.
   5. Remember that Python positions start from zero, so 2 refers to the third element, Chow Chow.
   6. Also remember that the last position, 5, is not included in the slice, so we finish at Labrador not Chihuahua.
   7. If you want to the slice to start from the beginning of the list you can omit the zero.
   8. E.g - `breeds[:3]` -> Output -> `['Labrador', 'Poodle', 'Chow Chow']`.
   9. Here using `[:3]` returns the first 3 elements.
   10. Slicing with `[:]` on its own returns the whole list.

5. Slicing DataFrames -
   1. [For More Information](../02%20-%20Intermediate%20Python/02%20-%20Dictionaries%20&%20Pandas.md)
   2. We can also slice dataframe, but first, you need to sort the index.
   3. E.g - `dogs_srt=dogs.set_index(['breed', 'color']).sort_index()`.
   4. Here the dogs dataset is given a multi-level index of breed and color, then, the index is sorted with `.sort_index()`.
   5. To slice rows at the outer level of an index, you call **loc**, passing the first and last values separated by a colon.
   6. E.g - `dogs_srt.loc['Chow Chow' : 'Poodle']`.
   7. Imp -> _The Final Value Poodle is included_.
   8. There are 2 differences compared to slicing list ->
      1. Rather than specifying row numbers, you specify the index values.
      2. The final value is included.
   9. The same technique doesn't work for inner index levels.
   10. Here trying to slice from "Tan" to "Gray" returns an empty DataFrame instead of 6 dogs which we wanted.
   11. E.g - `dogs_srt.loc["Tan" : "Gray"]`.
   12. It's important to know the danger here, pandas doesn't throw an error to let you know that there is a problem, so be careful while coding.
   13. The correct approach to slicing at inner index levels is to pass the first and last positions as tuples.
   14. E.g - `dogs_srt.loc[("Labrador", "Brown") : ("Schnauzer", "Grey")]`.
   15. Here the first element to include is a tuple of Labrador and Brown.
6. SLicing Columns -
   1. Since dataframes are 2-D objects, we can also slice the columns.
   2. You do this by passing 2 arguments to loc.
   3. The simplest case involves subsetting columns and keeping all rows.
   4. To do this, pass a colon as the first argument to loc. As with slicing list, a colon itself means keep everything.
   5. The second argument takes column names as the first and the last position to slice on.
   6. E.g - `dogs_srt.loc[:, "names" : "height_cm"]` -> The output will contain the last position column.
7. Slice Twice -
   1. You can also slice on rows and columns at the same time: simply pass the appropiate slice to each argument.
   2. E.g - `dogs_srt.loc[("Labrador" : "Brown") : ("Schnauzer" : "Grey"), "name" : "height_cm"]`.
   3. Here you see the previous two slices being performed in the same line of code.
8. `dogs_height_by_breed_vs_color.mean(axis='index')` -
   1. The methods for calculating the summary statistics on a DataFrame, such as mean, have an axis argument.
   2. The default value is index which means we _calculate the statistics across rows_.
   3. Here it means that it is calculated for each color. That is across the breeds.
   4. The behavior is the same if you hadn't specified the axis argument.
   5. To calculate the summary statistics for each row, that is _across the columns_, you set the axis to columns.
   6. E.g - `dogs_height_by_breed_vs_color.mean(axis='columns')`
   7. Here the mean height is calculated for each breed. That is across the colors.
   8. For most dataframes setting the axis arguments doesn't make any sense, since you'll have different datatypes in each column.
   9. Pivot tables are a special case since every column contains the same datatype.
