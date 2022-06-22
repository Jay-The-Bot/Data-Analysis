# Intermediate Python

## Loops

### while Loop

The while loop will continue to execute the code until the condition is true.

Syntax of While loop -

```python
  while condition:
    expression
```

1. Numerically calculating model
2. "repeating action until conditions are met."
3. Example -
   1. Error starts at 50
   2. Divide error by 4 on every run
   3. Continue until the error no longer > 1

### For Loop

```python
for var in seq :
  expression
```

"for each var in sequence, execute expression"

### Loop Data Structures Part 1

Looping over dicitonary and Dataframe

### Loop Data Structures Part 2

In pandas you have to mention explicitly that you have to iterate over the rows.
You do this by calling the iterrows method in the dataframe.

**Add Column** -

A better approach to calculate an entire dataframe column by applying a function on a particular column in an element wise fashion, is apply().

E.g-

```python
import pandas as pd
brics = pd.read_csv("brics_csv", index_col = 0)
brics["name_length"] = brics["country"].apply(len)
print(brics)
```

Apply is a efficient method.

## Types of Functions -

1. `enumerate()` -

   1. Used to print the index as well as index value.
   2. Enumerate produces two values on each iteration: the index of the value, and the value itself.
   3. E.g -

   ```python
    for index, height in enumerate(fam) :
      print("index") + str(index) + ": " + str(height)
   ```

2. `world.items()` -

   1. Here world is a e.g dictionary.
   2. We cannot use the the enumerate method on a dictionary.
   3. We can fix this by calling the method items() on world.
   4. This will generate a key and value in each iteration.
   5. Dictionaries are inherently unordered: the order in which they're iterated over is not fixed, at least in Python 3.5.
   6. Here in the for loop the order matters, the first variable gets the key, second gets the value.
   7. Dictionary require a method.
   8. E.g -

   ```python
    for key, value in world.items():
      print(key + " -- " + str(value))
   ```

3. `np.nditer(meas)` -

   1. It is used for print 2-D NumPy arrays.
   2. Doing this will give us all the single element in each line.
   3. NumPy array uses a function:
   4. E.g -

   ```python
    import numpy as np
    np_height = np.array([1.73, 1.60, 1.71, 1.89, 1.79])
    np_weight = np.array([65.4, 59.2, 63.6, 88.4, 68.7])
    meas = np.array([np_height, np_weight])
    for val in np.nditor(meas):
      print(val)
   ```

4. `brics.iterrows()` -

   1. The itterrows method looks at the DataFrame, and on each iteration generates two peices of data : the label of the row and the actual data in the row as a Pandas Series.
   2. E.g -

   ```python
    import pandas as pd
    brics = pd.read_csv("brics_csv", index_col = 0)
    for lab, row in brics.iterrows():
      print(lab)
      print(row)
      # Printinh only the capital
      print(lab + ": " + row["capital"])
      # Creating series on every iteration
      brics.loc[lab, "name_length"] = len(row["country"])
   ```

5. cars["cars_per_cap"].upper() -
   1. Return the capitalized version of each word in cars_per_Cap column.
