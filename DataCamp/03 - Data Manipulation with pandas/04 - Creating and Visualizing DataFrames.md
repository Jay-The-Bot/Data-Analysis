# Data Manipulation with pandas

## Creating and Visualizing DataFrames

1. Plotting
2. Handling Missing Data
3. Reading Data into a DataFrame

### Visualizing your data

Plots are a powerful way to share the insights you've gained from your data.

**Histograms** -

We will need matplotlib.pyplot as plt to display our visualizations.
Just like pd is the standard alias for pandas, plt is the standard alias for matplotlib.pyplot.

Creating a histogram -

1. `dog_pack['height_cm'].hist()

Show the plot -> plt.show()

We can create a histogram of the height variable by selecting the column and calling dot-hist. In order to show the plot, we need to call plt-dot-show. The x-axis represents the heights of the dogs, and the y-axis represents the number of dogs in each height range. By grouping observations into ranges, the histogram allows us to see that there are a lot of dogs around 50 to 60 centimeters tall.

We can adjust the number of bars, or bins, using the "bins" argument. Increasing or decreasing this can give us a better idea of what the distribution looks like.

**Bar Plot** -

Bar plots can reveal relationships between a categorical variable and a numeric variable, like breed and weight. To compute the average weight of each breed, we group by breed, select the weight column, and take the mean, giving us the average weight of each breed. Now we can create a bar plot from the mean weights using the plot method, setting "kind" equal to "bar." Finally, we call plt-dot-show. To add a title to our plot, we can use the title argument of the plot method.
E.g - `avg_weight_by_breed = dog_pack.group_by('breed')['weight_kg'].mean()`

Creating a bar plot =
avg_weight_by_breed.plot(kind='bar')
Finally, we call plt.show()
To add title
avg_weight_by_breed.plot(kind='bar', title='Mean weight by Dog Breed')

**Line Plot** -

Line plots are great for visualizing changes in numeric variables over time.
E.g - `sully.plot(x='date', y='weight_kg', kind='line')`

We may want to rotate the x-axis labels to make the text easier to read. This can be done by passing an angle in degrees with the _rot_ argument.
E.g - `sully.plot(x='date', y='weight_kg', kind='line', rot=45)`
Here we rotate the labels by 45 degrees.

**Scatter Plots** -
Scatter plots are great for visualizing relationships between two numeric variables.
E.g - `dog_pack.plot(x='height_cm', y='weight_kg', kind=scatter)`

**Layering Plots** -
Plots can also be layered on top of one another.
E.g - dog_pack[dog_pack['sex'] == 'F']['height_cm'].hist() -> Bottom
dog_pack[dog_pack['sex'] == 'M']['height_cm'].hist() -> Top
plt.legend(['F', 'M'])
plt.show()

Making the histogram translucent ->
dog_pack[dog_pack['sex'] == 'F']['height_cm'].hist(alpha=0.7) -> Bottom
dog_pack[dog_pack['sex'] == 'M']['height_cm'].hist(alpha=0.7) -> Top
plt.legend(['F', 'M'])
plt.show()

### Missing Values

You could be given a DataFrame that has missing values, so it's important to know how to handle them. Most data is not perfect - there's always a possibility that there are some pieces missing from your dataset.

In a pandas DataFrame, missing values are indicated with N-a-N, which stands for "not a number."

### Creating a Dataframe -

A dictionary is a way of storing data in Python.
It holds a set of key-value pairs.
You can create a dictionary like this, using curly braces. Inside, each key-value pair is written as "key colon value."

E.g of a Dictionary-

```python
# Creating a Dictionary
my_dict = {
  "title": "Charlotte's Web",
  "author":"E.B. White",
  "published":1952
}
# Access a dictionary
my_dict['title'] # THis will give output Charlotte's Web
```

There are many ways to create DataFrames from scratch, but we'll discuss two ways: from a list of dictionaries and from a dictionary of lists.
In the first method, the DataFrame is built up row by row, while in the second method, the DataFrame is built up column by column.

### Reading and writing CSVs

CSV, or comma-separated values, is a common data storage file type.
It's designed to store tabular data, just like a pandas DataFrame.
It's a text file, where each row of data has its own line, and each value is separated by a comma.
Almost every database, programming language, and piece of data analysis software can read and write CSV files.
That makes it a good storage format if you need to share your data with other people who may be using different tools than you.

Now that we've changed the data let's create an updated CSV file to share with the dogs' owners.
To convert a DataFrame to a CSV, we can use new_dogs dot to-underscore-csv, and pass in a new file path.
If we take a look at the new file, it contains the BMI column.

## Types of Functions -

1. `dogs.isna()` -
   1. Here _dogs_ is the name of the dataframe and you can have any dataframe there.
   2. When you first get a DataFrame, it's a good idea to get a sense of whether it contains any missing values, and if so, how many.
   3. That's where the isna method comes in.
   4. When we call isna on a DataFrame, we get a Boolean for every single value indicating whether the value is missing or not, but this isn't very helpful when you're working with a lot of data.
   5. If we chain dot-isna with dot-any, we get one value for each variable that tells us if there are any missing values in that column.
   6. E.g - `dogs.isna().any()`
   7. Here, we see that there's at least one missing value in the weight column, but not in any of the others.
   8. Since taking the sum of Booleans is the same thing as counting the number of Trues, we can combine sum with isna to count the number of NaNs in each column.
   9. E.g - `dogs.isna().sum()`
   10. We can use those counts to visualize the missing values in the dataset using a bar plot. Plots like this are more interesting when you have missing data across different variables.
   11. E.g - `dogs.isna().sum().plot(kind='bar')`
2. `dogs.dropna()` -
   1. One option is to remove the rows in the DataFrame that contain missing values.
   2. This can be done using the dropna method.
   3. However, this may not be ideal if you have a lot of missing data, since that means losing a lot of observations.
3. `dogs.fillna(0)` -
   1. Another option is to replace missing values with another value.
   2. The fillna method takes in a value, and all NaNs will be replaced with this value.
   3. There are also many sophisticated techniques for replacing missing values, which you can learn more about in our course about missing data.
4. `new_dogs.to_csv('new_dogs_with_bmi.csv')` -
   1. Saves the edited dataframe here `new_dogs` to the csv file .
5. `air_force_nz.query('gender == "FEMALE"').tail(1)` -

   1. Here the query gives us all the females from the DataFrame air_force_nz.
   2. And then the tail method return the last row of the DataFrame.
   3. The argument 1 means last one row.
   4. For multiple rows enter the number 2, 3, 4, ...

   5. tail lets you pick a last element from DataFrame Column.
