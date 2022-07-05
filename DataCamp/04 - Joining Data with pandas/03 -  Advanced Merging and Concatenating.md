# Joining Data with pandas

## Advanced Merging and Concatenating

### Filtering Joins

So far, we have only worked on mutating joins from two DataFrames. However, filtering joins filter observations from one table based on whether or not they match an observation in another table.

**Mutating Joins** -

- Combines data from two tables based on matching observations in both tables.

**Filtering Joins** -

- Filtering Observations from table based on whether or not they match an observation in another table.

**Semi Join** -

1. A semi join filters the left table down to those observations that have a match in the right and left table.
2. It is similar to an inner join where only the intersection between the tables is returned, but unlike an inner join, only the columns of left table are shown not the right.
3. Finally, no duplicate rows from the left table are returned, even if there is one-to-many relationship.
4. E.g - ![Semi Join](Images/Img%20-%207.png)

**Anti Join** -

1. An Anti Join returns the observations in the left table that do not have a matching observation in the right table. _Return the left table, excluding the intersection_
2. It also only returns the columns from the left table.

### Concatenate DataFrames together vertically

To merge the tables concatenate, we usr the merge method to concatenate, or stick tables together, vertically or horizontally, but in this lesson, we'll focus on vertical concatenation.

Often Data of Multiple periods of time will come in multiple tables, but if we want to analyze it together, we'll need to combine them into one.

### Verifying Integrity

Both merge and concat methods have special features that allow us to verify the structure of our data. When merging two tables, we might expect the tables to have a one to one relationship. However, one of the columns we are merging on may have duplicated value which will turn the relationship in one-to-many.

When concatenating tables vertically, we might unintentionally create duplicate records if a record exists in both tables.

The validate and verify_integrity arguments of a merge and concat methods will allows us to verify the data.

**Merge Method** -

If we provide the validate argument one of these key strings, it will validate the relationship between the two tables.
/.merge(validate=None):

- Check if merge is of the specified type:
  - one-to-one
  - one-to-many
  - many-to-one
  - many-to-many

For Eg, if we specify we want a one-to-one relationship, but it turns out that the relationship is not one-to-one, then an error is raised.

Merging one-to-one -> `tracks.merge(specs, on='tid', validate='one_to_one')`

Why verify integrity and what to do ?
-> Often the real world data is not clean, and it may not always be evident if the data has the expected structure.Therefore, verifying the structure is useful and saving us from having a mean skewed by duplicate value, or from creating an inaccurate plots.

If we receive a MergeError or a ValueError, we can fix the incorrect data or drop duplicates rows. In general, you should look to correct the values.

## Types of Functions -

1. Semi Join -

   1. Step 1 -> `genres_tracks = genres.shape(top_tracks, on='gid')` (Inner Join) -
      1. First, let's merge the two tables with an inner join.
      2. Since this is an inner join, the returned column 'gid' holds only the value where both the tables are matched.
   2. Step 2 -> `genres['gid'].isin(genres_tracks['gid'])` (Checking Rows) -
      1. It uses a method called isin(), which compares every 'gid' in the genres table to the 'gid' in the genres_tracks table.
      2. This will tell us if our genre appears in our merged genres_tracks table.
      3. This line of code returns boolean series of true and false values.
   3. After Combining Everything -

      ```python
         genres_tracks = genres.merge(top_tracks, on='gid')
         top_genres = genres[genres['gid'].isin(genres_tracks['gid'])]
         print(top_genres.head())
         # We have completed a Semi Join
      ```

   4. This is called a filtering join because we've filtered the genres table by what's in the top_tracks table.

2. Anti Join -

   1. Step 1 -> `genres_track = genres.merge(top_tracks, on='gid', how='left', indicator=True)`
      1. The first step is to use a left join returning all the rows from the left table.
      2. Here we'll use the indicator argument and set it to True.
      3. With the indicators set to true, the merge method adds a column called _\_merge_ to the output.
      4. This column tells the source of each row.
   2. Step 2 -> `gid_list = genres.tracks.loc[genres_tracks['_merge'] == 'left_only', 'gid']`
      1. We use the loc accessor and merge column to select the rows that only appeared in the left table and return only the 'gid' column from the genres_tracks table.
      2. We now have a list of gid's not in the tracks table.
   3. After Combining Everything -

      1. In our final step we use the isin() method to filter for the rows with gid's in our gid_list.
      2. Our Output shows those genres not in the track table.

      3. ```python
            genres_tracks = genres.merge(top_tracks, on='gid', how='left', indicator=True)
            gid_list = genres_tracks.loc[genres_tracks['_merge'] == 'left_only', 'gid']
            non_top_genres = genres[genres['gid'].isin(gid_list)]
         ```

3. `pd.concat([inv_jan, inv_feb, inv_mar])` -
   1. This is Basic Concatenation.
   2. We can pass a list of table names into pandas dot concat to combine the table in the order they are passed in.
   3. To concatenate vertically, the _axis_ argument must be set to 0, but 0 is default, so we don't need to explicitly write this.
   4. The result is a vertically combined table. Each table's index value was retained.
   5. If the index contains no valuable informantion, then we can ignore it in the concat method by setting the ignore_index to True.
   6. E.g -`pd.concat([ivc_jan, inv_feb, inv_mar], ignore_index=True)`.
   7. The result is that the index will go from 0 to n-1.
   8. Concatenate Different tables with Same Columns ->
      1. Now, suppose we wanted to associate specific keys with each of the pieces of our three original tables.
      2. We can provide a list of labels of the keys argument.
      3. We need to make sure that the ignore_index argument is False, since you can't add a key and ignore at the same time.
      4. E.g -`pd.concat([ivc_jan, inv_feb, inv_mar], ignore_index=False, keys=['jan', 'feb', 'mar'])`.
      5. This results in a table with a multi-index, with a label on the first label.
   9. Concatenate tables with different column names ->
      1. The concat method by default will include all of the columns in the different tables if it's combining.
      2. The sort argument, if true, will alphabetically sort the different column names in the result.
      3. E.g - `pd.concat([inv_jan, inv_feb], sort=True)`
   10. If we only want the matching columns between tables, we set the join argument to _inner_.
   11. Its default value is equal to _Outer_, which is why concat by default will include all of the columns.
   12. Additionally the sort argument has no effect when join equals _inner_.
   13. The order of the columns will be same as the input tables.
   14. E.g - `pd.concat([inv_jan, inv_feb], join='inner')`
4. `.append()` -
   1. Append is the simplified concat method.
   2. It supports the ignore_index and sort arguments.
   3. However it does not support keys and join. Join is always set to outer.
   4. E.g - `inv_jav.append([inv_feb, inv_mar], ignore_index=True, sort=True)`
   5. Append is a DataFrame method therefore, we list the _inv_jan_ table first then call the method.
   6. We add the other tables as a list, and set the ignore_index and sort arguments similar to the concat method.
5. Merge Validate -
   1. one_to_one -> `tracks.merge(specs, on='tid', validate='one_to_one')` ->
      1. Here we merged the two tables on the left and specs on the right.
      2. In the result, a MergeError is raised. Python then tells us that the right table has duplicates, so it is not a one-to-one merge.
      3. We know that we should handle the duplicates properly before merging.
   2. one_to_many -> `tracks.merge(specs, on='tid', validate='one_to_many')` ->
      1. Now we'll merge the album information with the tracks table.
      2. For every album there are multiple tracks, so this should be a one-to-many relationship.
      3. When we set the validate argument to one-to-many we get no errors.
6. Verifying Concatenations -
   1. It has the argument verify_integrity, which by default is false.
   2. However, if set to _True_, it will check if there are duplicates values in the index and raise an error if there are any.
   3. It will only check the index values not the columns.
   4. E.g - `pd.concat([inv_feb, inv_mar], verify_integrity=True)`
   5. The concat method raises a Value Error stating that the indexes have overlapping values.
   6. If the _verify_integrity_ is set to false, then the concat method now returns a combined table with the INVOICE_ID of number 9 repeated twice.
