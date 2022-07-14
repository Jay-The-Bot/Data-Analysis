# Introduction to Data Visualization with Seaborn

## Introduction to Seaborn

### Introduction to Seaborn - 1

Q. What is Seaborn ?
-> Seaborn is a powerful python library for creating data visualizations. It was developed to make it easy to create the most common types of plots.

Typical Data Analysis Workflow -
![Workflow](Images/Img%20-%2001.png)

Data Visualization is often a huge component of both the data exploration phase and the communication of result, so Seaborn is very useful here.

There are several tools that can be used for visualization, but seaborn offers several advantages.

1. Seaborn's main purpose is to make visualization easy. It was built to automatically handle a lot of complexity behind scenes.
2. Works extremely well with pandas data structures. Pandas is a library that is widely used for data analysis.
3. It is built on top of matplotlib, which is another Python Visualization Library. Matplotlib is extremely flexible. Seaborn allows you to take advantage of this flexibility when you need it, while avoiding the complexity that Matplotlib's can introduce.

**Importing Seaborn** -
`import seaborn as sns`

We also need to `import matplotlib.pyplot as plt` for showing the diagram.

**Count Plot** - Count Plots take in a categorical list and return bars that represent the number of list entries per category.

### Using pandas with Seaborn

Data Scientists commonly use pandas to perform data analysis, so it's a huge advantage that Seaborn works extremely well with pandas data structure (DataFrame).

Pandas is a python library for data analysis. It can easily read datasets from many types of files including csv and txt files, and other types of text files.

**Making DataFrame with countplot()** -

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv('masculinity.csv')
sns.countplot(x='how_masculine', data=df)
plt.show()
```

Because we are using a named column in the dataframe, Seaborn automatically adds the name of the column as the x-axis label is at the bottom.

> Seaborn works great with pandas DataFrame only if the DataFrame is _tidy_.

**Tidy data** - means each observation has it own row and each variable has it's own column.

### Adding a third variable with hue

We'll see another big advantage that Seaborn offers: the ability to quickly add a third variable to your plots by adding color.

The ability to quickly add a third variable to your plots by adding colors.

## Types of Functions -

1. `sns.scatter(x=height, y=weight, data=df, hue='smoker',palette=hue_colors, hue_order=['No', 'Yes'])` -

   1. It takes the x and y argument as input.
   2. If x and y are variables then no problem, but if a column of a DataFrame. We need to provide an additional argument that is data which is the name of the dataframe.
   3. The data argument takes the DataFrame on which the plot is being plotted.
   4. The hue argument takes in a column that it adds the color on.
   5. Hue also allows you to assert more control over the ordering and coloring of each value.
   6. The **hue order** parameter takes in a list of values and will set the order of the values in the plot accordingly. Notice how the legend for smoker now lists "yes" before "no".
   7. You can set the "hue" parameter equal to the DataFrame column name "smoker" and then Seaborn will automatically color each point by whether they are a smoker
   8. Plus, it will add a legend to the plot automatically! If you don't want to use pandas, you can set it equal to a list of values instead of a column name.

      ```python
      import matplotlib.pyplot as plt
      import seaborn as sns
      hue_colors = {
         "Yes":"Black",
         "No":"Red"
      }
      hue_colors1 = {
         "Yes":"#808080",
         "No":"#00FF00"
      }
      sns.scatterplot(x='total_bill', y='tip', hue='smoker', palette=hue_colors)
      sns.scatterplot(x='total_bill', y='tip', hue='smoker', palette=hue_colors1)
      plt.show()
      ```

   9. You can also control the colors assigned to each value using the "palette" parameter.
   10. This parameter takes in a dictionary, which is a data structure that has key-value pairs.
   11. This dictionary should map the variable values to the colors you want to represent the value.
   12. Here, we create a dictionary called "hue colors" that maps the value "Yes" to the color black and the value "No" to the color red. When we set hue equal to "smoker" and the palette parameter equal to this dictionary, we have a scatter plot where smokers are represented with black dots and non-smokers are represented with red dots.
   13. In the last example, we used the words 'black' and 'red' to define what the hue colors should be.
   14. This only works for a small set of colors names that are defined by Matplotlib.
   15. Here is the list of Matplotlib colors and their names.
   16. E.g - ![Colors Available](Images/Img%20-%2002.png)
   17. Note that you can use a single letter Matplotlib Abbreviation instead of full name.
   18. You can also use an HTML color hex code instead of Matplotlib color names, which allow you to choose any color you want.
   19. The hue_orders argument decides the order of the legend appearing in the plot. We can set the hue_order as we want and the legend order would change that way.

2. `sns.countplot(x=gender)` -
   1. Count Plots take in a categorical list and return bars that represent the number of list entries per category.
   2. Here we gave the gender to x for creating a Vertical Graph.
   3. For horizontal graph we can assign gender to y instead of x.
   4. All the parameters of the scatter plot can also be used on Count Plot.
