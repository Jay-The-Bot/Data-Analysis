# Introduction to Data Science in Python

## Getting Started With Python

## Floats and Strings

Floats represent either integer or decimals.
`height = 24 weight = 75.5`.

String represent text; can contain numbers, spaces, and special characters
`name = 'Bayes' breed = "Golden Retriever"`.
We define a string by putting either single or double quotes around a text.

If you define a string without quotes Python will think that the string is a variable, and if the variable wasn't previously defined, then you will get a **_name error_**.

Alternatively, you might have started your string with one type of quote and finished with a different type. This will give you a **_syntax error_**.

If you mix single and double quotes you'll get a **_syntax error_**.

## Functions

A function is an action. It turns one or more input into output.
E.g -

```python
  import pandas as pd
  from matplotlib import pyplot as plt

  df = pd.read_csv('letter_frequency')

  plt.plot(df.letter_index, df.frequency, label='Ransom')
  plt.show()
```

The above code would read the file produce the graph.

## Types of Functions

1. `print()` -> Will print the variable inside the parenthesis.
2. `pd.read_csv()` -> turns a CSV file into a table in Python.
   1. This function takes one argument, the name of the file as a string.
3. `plt.plot()` -> Turns data into line plot.
   1. `plt.plot(x_values, y_values)` -> This is the default format of plot function.
      1. We begin with the name of the function - plt.plot(), like all function we will be putting arguments inside of parentheses.
      2. The first argument is the x-values we want to plot.
      3. We select the column by typing the name of the DataFrame, followed by a dot (.), followed by a column name.
      4. The second argument is the y-values we want to plot.
   2. `plt.plot(label='')` -> This will allow us to create a legend for our graph.
   3. `plt.plot(color='')` -> This will give the inputted color to the given line.
      1. The `color` keyword will accept a string corresponding to a [Web Color](https://en.wikipedia.org/wiki/Web_colors).
      2. The list of allowed colors is in the link above.
   4. `plt.plot(linewidth='')` -> This will change the line width for increasing the `linewidth` of a line.
      1. The default `linewidth` is 1.
4. `plt.show()` -> Displays the plot in a new window.
   1. If we only type `plt.plot()` nothing will showup. Thats because Python wants to give us the opportunity to enter other commands.
   2. When we want to display everything we've made, we use `plt.show()` function.
   3. This function takes no arguments

**`plt.plot`**

```python
plt.plot(df.letter_index, df.frequency, label='Ransom')
```

1. Here `df.letter_index` and `df.frequency` are positional arguments.
2. Here `label="Ransom"` is a Keyword argument.
3. `plt.plot()` plots the `df.letter_index` is on the **x-axis** and `df.frequency` is on the **y-axis**.
4. The function name has 2 parts -
   1. Function Module -
      - Starts with the module that the function lives in.
      - In this case it is plt, which is implemented from matplotlib.
   2. Function Name -
      - This part starts after the period symbol(.).
      - After this comes a set of parentheses.
      - The inputs to the functions will all come inside the parentheses.
5. Types of Arguments in Function -
   1. Positional Arguments -
      - These are input to the a function; they tell the function how to do it's job.
      - Positional Arguments must come in a specific order.
      - In this case the first argument is the `x-value` of each point, and the second argument is the `y-value` of each point.
      - Each argument is separated by a Comma(,). If you forget the comma we will get a **Syntax Error**.
   2. Keyword Arguments -
      - They come after the positional arguments.
      - There are **multiple** keyword arguments, they can come in **any order**.
      - Start with a name of the argument, then a equals sign, followed by the argument.
