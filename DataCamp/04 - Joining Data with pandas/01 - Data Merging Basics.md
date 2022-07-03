# Joining Data with pandas

## Data Merging Basics

### Inner Join

The pandas package is a powerful tool for manipulating and transforming data in Python. However, when working on an analysis, the data needed could be in multiple DataFrames.
This course will focus on the vital skill of merging DataFrames together.

**Merging DataFrames** -

1. We have two DataFrames are related by their ward column.
2. We can merge them together, matching the ward number from each row of the wards DataFrame to the ward numbers from the census DataFrame.
3. The pandas package has excellent DataFrame method for performing this kind of merge called merge.

E.g - `wards_censes = wards.merge(census, on='ward')`

> When the returned rows have the matching value for the column on which the merge is happening, in the both DataFrame. It is called as a **Inner Join**.

> An Inner join will only return rows that have matching values in both DataFrames.

### One-to-many relationships

**Types of Relationships in a DataFrame** -

1. **One - To - One** ->
   1. Every row on the left DataFrame is related to only one row in the right DataFrame.
   2. In the relationship between the ward DataFrame and the censes DataFrame.
   3. Every row in the wards DataFrame is related to only one row in the census DataFrame so there is only one row for each ward in the resulting DataFrame.
      ![One to One Relationship](Images/Img%20-%201.png)
2. **One - To - Many** ->
   1. In a One - To - Many relationship every row, in the left table is related to one or more rows in the right table.
   2. We use the same syntax as we did with one-to-one relationships.
   3. Pandas takes care of the one-to-many relationships for us and doesn't require anything special on our end.
   4. By printing `wards.shape`, we can see that the our original wards table has 50 rows.
   5. After merging with the Wards Dataframe with the licenses table, the resulting table has 10,000 rows.
   6. When you merge the DataFrames in a one to many relationships, the number of rows returned will likely be different than the number in the left table.
      ![One To Many Relationship](Images/Img%20-%202.png)

### Merging multiple DataFrames

1. Sometimes we need to merge together more than just two tables to complete our analysis.
2. E.g - `grants.license = grants.merge(licenses, on='zip')`.
3. By using the above command we would get some repeated data.
4. The same would happen if we merge it on the address.
5. Therefore, the best option is to merge the tables using the combination of both address and zip code.

> To do a merge on multiple column - `grants.merge(licenses, on=['address', 'zip'])`

6. We pass a list of column names we want to merge on to the 'on' argument.
7. This allows us to use multiple columns in the merge.
8. As before, the matching rows between the two DataFrames are returned with the columns of the grant table listed first.
9. However, when we merge on two columns, in this case address and zip code, we are requiring that both the address and the zip code of the rows in the left table to match the address and zip code of a row in the right table in order for them to be linked to each other in the merge.

## Types of Functions -

1. `wards_censes = wards.merge(census, on='ward', suffixes=('_ward', '_cen'))` -

   1. The merge method takes the first DataFrame, here _wards_, and merges it with the second dataframe, which is _censes_.
   2. We use the on argument to tell the method that we want to merge the two DataFrames on the ward column.
   3. E.g - `wards_censes = wards.merge(census, on='ward')`
   4. Since we listed the wards DataFrame first it's column will appear first in the output, followed by the DataFrames of the census DataFrame.
   5. The merge DataFrame may have suffixes of underscore x or y.
   6. This happens because both the DataFrames have some same columns.
   7. To avoid multiple columns with the same name, they are automatically given a suffix by the merge method.
   8. We can use the suffix argument of the merge method to control this behavior.
   9. We provided a tuple where all of the overlapping columns in the left DataFrame are given a suffix _\_ward_, and those of the right DataFrame will be given the suffix _\_cen_.
   10. This makes it easier for us to tell the difference between the columns.

2. `grants_licenses_ward = grants.merge(licenses, on=['address', 'zip']) \ .merge(wards, on='ward', suffixes=('\_bus', '\_ward'))` -
   1. First, we merge the grants table with the wards table on the ward column again, adding suffixes to the separated column names.
   2. Note that we're using Python's backslash line continuation method to add the second merge on the next line.
   3. Python will read this as just one line of code.
   4. Without this python will throw out the syntax error since it will parse it as two separate lines of code, so don't forget to add the backslash.
   5. We could merge as many more table's as we need by just adding the backslash and DataFrames as needed.
