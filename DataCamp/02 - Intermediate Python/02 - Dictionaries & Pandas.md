# Intermediate Python

## Dictionaries & Pandas

### Dictionaries, Part - 1

**Dictionary** -

1. A Dictionary is a set of key value pairs.
2. The keys in a dictionary should be unique.
3. These unique keys should be immutable. Basically the immutable objects cannot be changed after they are created.
4. Strings, Booleans, Integers, Floats are immutable objects.
5. But the list is mutable because you can change its contents after its created.
6. A dictionary with all immutable objects as keys is perfectly valid.
7. However, `{["just", "to", "test"]: "value"}`, this dictionary uses a list as a key, it is not valid, Hence we will get an error.

**Adding into a Dictionary** -

1. Suppose we want to add a key, value pair into the dictionary.
2. To add int we just write the name of the key value pair.

```python
   #E.g
   world["sealand"] = 0.000027
```

3. If we check out world again we will see the changes in the dictionary.
4. We can also use `sealand in world` this will return the value `true`.

**Creating a Dictionary** -

1. To create the dictionary, you need curly brackets.
2. Next, inside the curly brackets, you have a bunch of what are called key:value pairs.
3. To find the value of something in dictionary - E.g - `world["albania"]`.
4. Here `albania` is the key and the E.g will give the index of 'albania' in the array europe.

```python
world = {"afghanistan" : 30.55, "albania" : 2.77, "algeria" : 39.21}
```

### Dictionaries, Part - 2

**List V/S Dictionary** -

| List                                                                   | Dictionary                       |
| ---------------------------------------------------------------------- | -------------------------------- |
| Select, Update, Remove with [ ].                                       | Select, Update, remove with [ ]. |
| Indexed by range of numbers.                                           | Indexed by unique keys.          |
| Collection of Values - order matters, for selecting the entire subset. | Lookup tables with unique keys.  |

### Pandas - 1

Pandas is a high level data manipulation tool, built on NumPy package.

Data can come in many forms: every row is a measurement, or an observation, and for each observation, there are different variables.

**Datasets in Python** -

1. 2D NumPy Array ->
   1. It is a option to work with for our data, but it is not the best.
   2. In previous examples there are different datatypes and NumPy arrays are not good at handling these.
   3. Your datasets will typically comprise different data types, so we need a tool that's better suited for the job.
   4. To easily and efficiently handle this data, there's the Pandas package.

**Pandas** -

1. Pandas is a high level data manipulation tool developed by Wes McKinney, built on the NumPy package.
2. Compared to NumPy, it's more high level, making it very interesting for data scientists all over the world.
3. In pandas, we store the tabular data like the `brics table` here in an object called a **DataFrame**.
4. You see a similar structure as 2D NumPy Array in **DataFrame**: the rows represent the observations, and the columns represent the variables.

**Creating a DataFrame** -

1. DataFrame from a Dictionary -

   1. First of all you can make a dataframe manually, from a dictionary.
   2. Using the distinctive curly brackets, we create `key - value` pairs.
   3. The keys are the column labels, and the values are the corresponding column, in the list form.
   4. After importing the `Pandas` module. We can create a **DataFrame**.
   5. Code ->

   ```python
   import pandas as pd
   brics = pd.DataFrame(dict)
   #Here the brics is the new dataframe and dict the dictionary
   ```

   7. Pandas assign some automatic row labels.
   8. To specify them manually, you can set the index attribute of brics list with correct labels.

For huge amounts of data, we cannot use the Manual Method.

2. Import data from an External File to create a DataFrame -

   1. Code ->

   ```python
      brics = pd.read_csv('brics.csv')
   ```

   2. If you now print brics, there's still something wrong. The row labels are seen as a column in their own right.
   3. To solve this, we'll have to tell the read_csv function that the first column contains the row indexes.
   4. You do this by setting the index_col argument, like this `brics = pd.read_csv('brics.csv', index_col=0)`

`CSV - Comma Separated Values`

### Pandas - 2

We need to make sure that the dataframe has the rows and columns with given appropriate labels. This is important to make accessing columns, rows and single elements in your DataFrame easy.

There are numerous ways in which you can index and select data from DataFrames, so we'll take this step by step.

**Index and Select Data** -

1. Square Brackets
2. Advanced Methods
   1. loc
   2. iloc

**Column Access** -

1. **Series Access** -

Suppose you want to select a column from a dataframe.

E.g - `brics["country"]` -> This is of the type `pandas.core.series.Series`.

Series is like a 1-D array that can be labelled, just like a dataframe. Otherwise put, if you put in a bunch of Series, you can create a DataFrame.

2. **DataFrame Access** -

If you want to select the country column but keep the data in a DataFrame, you'll need double square brackets, like this. E.g - `brics[["country"]]` -> This is of the type `pandas.core.frame.Dataframe`

## Types of Functions

1. `plt.index()` -
   1. index(), a list method.
   2. Return the index a element iss present in.
   3. E.g- `Ind_lib = countries.index('albania')` -> This will return the index of albania in countries array.
2. `europe.keys()` -
   1. This method returns all the keys present in the europe dictionary.
   2. Works on dictionary.
3. `del()` -
   1. We can delete the elements in the element inside the del function.
   2. E.g- `del(world['sealand]')` -> This will delete the sealand from the dictionary.
4. `*dataframe*.index` -
   1. It change the row labels which are set to 0 to ..., to the new value.
   2. E.g -
      ```python
        cars.index = row_labels
        # row_labels = ['US', 'AUS', 'JPN', 'IN', 'RU', 'MOR', 'EG']
        # Here the dataframe is cars, and we set the arr row_label as the default row.
      ```
5. `type()` -
   1. It returns the type of object present inside the parenthesis.
   2. E.g - `type(brics["country"])` will return `pandas.core.series.Series`
