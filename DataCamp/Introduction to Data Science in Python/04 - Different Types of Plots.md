# Introduction to Data Science in Python

## Different Types of Plots

### Making a Scatter Plot

**Scatter Plot** -

1. A scatter plot allows us to show where each data point sits on a grid.
2. Line plots let us visualize ordered data points, but scatter plots are a great way of viewing un-ordered points.
3. Many of the same keyword arguments that we used in line plots will work in scatter plots. E.g - _color_, _linestyle_.

**Alpha**

1. Alpha accepts a number between 0 and 1 and makes each marker transparent.
2. The smaller the alpha parameter, the more transparent the dot.

**Creating a Scatter Plot** -

`plt.scatter(df.age, df.height)`

1. The first input parameter the x-data.
2. The second argument is the y-data.
