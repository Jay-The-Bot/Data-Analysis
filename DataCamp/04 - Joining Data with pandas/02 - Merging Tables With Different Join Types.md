# Joining Data with pandas

## Merging DataFrames With Different Join Types

### Left Join

**Review** -

1. In chapter 1, we introduced the pandas merge method that allows us to combine two DataFrames by specifying one or more key columns to link the DataFrames by.
2. By default, the merge method performs an inner join, returning only the rows of data with matching values in the key columns of both DataFrames.

**Left Join** -

1. Left join returns all rows of the data from the left DataFrame and only those rows from the right DataFrame where key columns match.
2. E.g - ![Left Join](Images/Img%20-%203.png)
3. Here we have two DataFrames left and right. We want to use a left join to merge them on key column C.
4. A left join returns all the rows from the left DataFrame and only those rows from the right DataFrame where column C matches in both.
5. Notice the second row of the merged DataFrame.
6. The columns from the left DataFrame are filled in, while the columns from the right DataFrame is not since there wasn't a match found for that row in the right DataFrame.

### Other Joins

The merge method supports two other join types -

1. Right Join -
   1. It will return all of the rows from the right DataFrame and includes only those rows from the left DataFrame that have matching values.
   2. It is the mirror opposite of the left join.
   3. E.g - ![Right Join](Images/Img%20-%204.png)
   4. Only rows from the left DataFrame where the column C matches are returned.
   5. Where there isn't a match, the columns from the left DataFrame will be missing in the result DataFrame, like rows one and four.
2. Outer Join -
   1. An outer join will return all of the rows from both of the DataFrames regardless if there is a match between the DataFrames.
   2. E.g - ![Outer Join](Images/Img%20-%205.png)
   3. Where the key column used to join the DataFrames has no match, null values are returned.
   4. That is why in the result the columns form the left DataFrame are missing, in rows one and five, and in column D three are missing.

### Merging a DataFrame to itself

Merging a DataFrame to itself, this type of merge is also referred to as a self join.

**So when would you ever need to merge the DataFrame to itself ?**

1. The DataFrame here is called sequels and has three columns. It contains the columns movie id, title, sequel. The sequel number refers to the movie_id that is a sequel to the original movie.
2. E.g - ![Self Join](Images/Img%20-%206.png)
3. If we would to like to see a DataFrame with the movies and the corresponding sequel movie in one row, of the DataFrame, we will need to merge the DataFrame to itself.
4. In the left DataFrame, the sequel ID for Toy Story is 863 is matched with 863 in the ID column of the right DataFrame.
5. Since the merger is an inner join, Therefore we cannot see Avatar and Titanic because they do not have sequels.

When to merge the DataFrame to itself ->

- Hierarchical Relationships (E.g - Employee, Manager)
- Sequential Relationships (E.g - Logistics Movement)
- Graph Data (E.g - Network of Friends)

### Merging on indexes

Often, the DataFrame indexes have been given a unique id that we can use when merging the two DataFrames together.

There are different methods to set the index of the DataFrame, but if our data starts off with a CSV file, we can use the _index_col_ argument of the read_csv method.

E.g - `movies_tagline = movies.merge(taglines, on='id', how='left')`
In this case we are inputting to the on argument the index level which is called id.
The merge method automatically adjusts to accept index names or column names.

**MultiIndex DataSets** -

E.g- `samuel = pd.read_csv('samuel.csv', index_col=['movie_id', 'cast_id'])`

Since this is a inner join, both the movie_id and cast_id must watch in each DataFrame to be returned in the result.

There is one more thing regarding merging on indexes. If the index level names are different between the two DataFrames that we want to merge, then we can use the left_on and right_on arguments of the merge method.

E.g - `movies_genres = movies.merge(movies_to_genres, left_on='id', left_index=True, right_on='movie_id', right_index=True)`

Additionally, since we are merging on indexes, we need to set left_index and right_index to True.
These arguments take only True or False.
Whenever we are using the left_on or right_on arguments with an index, we need to set the respective left_index and right_index arguments to True.
The left_index and right_index tell the merge method to use the separate indexes.

## Types of Functions -

1. `movies_taglines = movies.merge(taglines, on='id', how='left')` -
   1. To merge these two DataFrames with a left join, we use our merge method similar to what we learned in chapter 1.
   2. Here we list the movie DataFrame first and merge it to the taglines on the ID column in both DataFrames.
   3. The additional argument `how` defines how to merge the two DataFrames.
   4. In this case, we use _left_ for a left join.
   5. The default value for how is 'inner', so we didn't need to specify this in Chapter 1 since we are only working on inner joins.
   6. The result of the merge shows a DataFrame with all of the rows from the movies DataFrame and a value for tag line where the ID column matches in both DataFrames.
   7. Whenever there isn't a matching ID in the taglines DataFrame, a null value is entered for the tag line.
   8. Pandas uses NaN to denote the missing data.
   9. A one-to-one merge like this one, a left join will always return the same number of rows as the left DataFrame.
2. `tv_movies = movies.merge(tv_genre, how='right', left_on='id', right_on='movie_id') -
   1. First of all, we set the how argument to right so that the merge performs a right join.
   2. Additionally, we introduced two new arguments, named left_on and right_on.
   3. They allows us to merge which key column from each DataFrame to merge the DataFrames.
   4. We list movies on left DataFrame, so we set left_on to id and right_on to movie_id.
3. `family_comedy = family.merge(comedy, on='movie_id', how='outer', suffixes=('_fam', '_com'))` -
   1. In this merge, we list the family DataFrame as the left DataFrame and merge it on the movie_id column.
   2. The how argument is set to outer for an outer join.
   3. Both of our columns have same names.
   4. Therefore, we add suffixes to show what DataFrame the columns originated.
   5. In the result DataFrame, every row is returned for both DataFrames and we see some null values.
4. `scifi_only = action_scifi[action_scifi['genre_act'].isnull()]` -
   1. Checks if the action_scifi DataFrame contains null value or not.
   2. If present it will return those rows.
5. `original_sequels = sequels.merge(sequels, left_on='sequel', right_on='id', suffixes=('_org', '_seq'))` -
   1. To complete this merge, we set the sequels DataFrame as the input to the merge method for both the left and the right DataFrames.
   2. We can think of it as merging two copies of the same DataFrame.
   3. All of the aspects we have reviewed regarding merging two labels still apply here.
   4. Therefore, we can merge the DataFrames on different columns.
   5. We'll use the 'left_on' and 'right_on' attributes to match rows where the sequel's id matches the original movie's id.
   6. Finally, setting the suffixes argument in the merge method allows us to identify which columns describe the original movie and which describe the sequel.
   7. When merging a DataFrame to itself, we can use the different types of joins we have already reviewed.
   8. E.g - `original_sequels = sequels.merge(sequels, left_on='sequel', right_on='id', how='left', suffixes=('_org', '_seq'))`
