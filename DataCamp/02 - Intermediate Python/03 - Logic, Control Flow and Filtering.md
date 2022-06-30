# Intermediate Python

## Logic, Control Flow and Filtering

### Comparison Operators

Using the greater than sign we can find out which whether the value is greater than some value.

Comparison operators are operators that can tell how two values relate, and the result in a boolean.
In the simplest sense we can use these operators on numbers.

We can also check that the 2 values are equal with == sign.

All the comparison operators also work for strings.

While checking, if the integer 3 is smaller than the string chris.

We get an error.

Typically, Python can't tell how two objects with different types relate.

Different numeric types, such as floats and integers, are exceptions as this example shows: no error this time.

In general, always make sure that you make comparisons between objects of the same type.

E.g - bmi = [21.852, 20.975, 21.75, 24.747, 21.441].

For bmi > 23.

For the comparison, NumPy builds a numpy array of the same size filled with the number 23, and then performs element wise comparison. This is concise yet very efficient code.

**Comparators** -

| Comparators | Meaning               |
| ----------- | --------------------- |
| <           | Strictly less than    |
| <=          | Less than or equal    |
| >           | Strictly greater than |
| >=          | Greater than or equal |
| ==          | Equal                 |
| !=          | Not Equal             |

### Boolean Operators

Combining Booleans -
We can use various operators for combining booleans.

Boolean Operators -

1. and - The and operator takes 2 booleans and returns true only if both the boolean themselves are true.
2. or - The or operator works similarly, but the difference is that only at least one of the boolean should be true.
3. not - It simply negates the boolean value you use it on.

E.g - `bmi > 21 and bmi < 22` gives the error -> The truth value of an array with more than one element is ambiguous. and clearly doesn't like an array of booleans to work on.

After some digging in the numpy documentation, you can find the functions logical_and, logical_or and logical_not, the "array equivalents" of and or and not.

For NumPy -

1. logical_and()
2. logical_or()
3. logical_not()

To actually select the only these bmis from the bmi array, we can use the resulting array of booleans in square brackets.
E.g - `bmi[np.logical_and(bmi > 21, bmi < 21)]`

### if, elif, else

Conditional Statements -

1. if -

   1. If the condition holds then the expression will get executed.
   2. E.g -

   ```python
   if condition :
    expression
   ```

2. else - For the else statement you dont need to specify a condition.
3. elif -

### Filtering pandas DataFrames

Select data from Pandas dataframe -
3 steps are required -

1. Select the column
   1. The are various ways to select the column.
   2. What's important here, is that we ideally get a Pandas Series, not a Pandas DataFrame.
   3. E.g - `brics['area']`
   4. Selecting Multiple Columns only of intrest ->
   5. E.g - `netflix_movies_col_subset = netflix_df_movies_only[['title', 'country', 'genre', 'release_year', 'duration']] `
2. do the comparison on the selected column
   1. E.g - `is_huge = brics['area'] > 8`.
   2. Now we will get a series containing booleans.
3. Use result to do appropriate selection of the dataframe.
   1. E.g - `brics[is_huge]`
   2. The final step is using this boolean Series to subset the Pandas DataFrame.
   3. To do this, you put is_huge inside square brackets.

We can also do this as a one line -
`brics[brics['area'] > 8]`

Using boolean operators on dataframe -

```python
import numpy as np
np.logical_and(brics['area'] > 8, brics['area'] < 10)
# The above code will create a boolean series.
# To subset the dataframe
brics[np.logical_and(brics['area'] > 8, brics['area'] < 10)]
```

## Types of Functions -

1. `np.logical_and()` -
   1. NumPy Array Equivalent of and.
   2. E.g - `np.logical_and(bmi > 21, bmi < 21)`
2. `np.logical_or()` -
   1. NumPy Array Equivalent of or.
3. `np.logical_not()` -
   1. NumPy Array Equivalent of not.
