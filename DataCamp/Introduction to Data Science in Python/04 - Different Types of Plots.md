# Introduction to Data Science in Python

## Different Types of Plots

### Making a Scatter Plot

**Scatter Plot** -

1. A scatter plot allows us to show where each data point sits on a grid.
2. Line plots let us visualize ordered data points, but scatter plots are a great way of viewing un-ordered points.
3. Many of the same keyword arguments that we used in line plots will work in scatter plots. E.g - _color_, _linestyle_, _marker_.

**Alpha** -

1. Alpha is generally used for decreasing the transparency of the points in the plot.
2. If there are too many points in a plot, such as in a scatter plot.We can't see if we've plotted many layers of points or just a single layer.
3. We can make it easier to read by using `Alpha`.
4. Alpha accepts a number between 0 and 1 and makes each marker transparent.
5. The smaller the alpha parameter, the more transparent the dot.

**Creating a Scatter Plot** -

`plt.scatter(x_values, y_values)`

1. The first input parameter the x-data.
2. The second argument is the y-data.

### Making a Bar Chart

**Bar Chart** -

1. The best way to visualize a comparison of categorical data is by using a bar chart.
2. In a _Bar Chart_ the x-axis is already labelled for us.
3. So, we only need to label the y-axis.
4. We can also create a horizontal bar chart.

**Creating a Bar Chart** -

`plt.bar(x_values, y_values)`

1. Creating a _Bar Chart_ is simple we simply provide two arguments to the function `plt.bar()`.

**Creating a Horizontal Bar Chart** -

`plt.barh(x_values, y_values)`

1. When we have many bars, it can be easier to fit all of the labels in with a horizontal bar plot.

**Adding Error Bars** -

`plt.bar(x_values, y_values, yerr=error)`

1. Averages don't always tell the full story.
2. Often, we'll want to show some sort of error associate with our average, such as the `standard deviation` or `standard error of the mean`.
3. We can add error bars to our bar chart by using the keyword argument `yerr` after our the first two positional arguments in `plt.bar`.
4. Here `error` is column already present in the DataFrame.

**Stacked Bar Chart** -

1. A stacked bar chart is a chart that uses bars to show comparisons between categories of data, but with ability to break down and compare parts of a whole.
2. Each bar in the chart represents a whole, and segments in the bar represent different parts or categories of that whole.

**Creating a Stacked Bar Chart** -

```python
plt.bar(x_values, y1_values)
plt.bar(x_values, y2_values, bottom=y1_values)
```

1. To create a stacked bar chart we create a our basic bar chart as we normally would.
2. Next, we stack the y2_values bars on top of the y1_values bars by using the keyword "bottom".
3. Normally, a bar chart will start each bar at 0, but if we add the keyword `bottom` to `plt.bar()` and feed in the heights of our bottom bars (in this case y1_values), matplotlib will plot the second set of bars starting where the first set of bars ends.

### Making a Histogram

1. A histogram visualizes the distribution of values in a dataset.
2. To create a histogram, we place each piece of data into a bin.

**Creating a Histogram** -

```python
plt.hist(values)
plt.hist(values, bins = n_bin)
plt.hist(values, bins = n_bin, range=(xmin, xmax))
plt.hist(values, bins = n_bin, range=(xmin, xmax), density=True)
```

1. This function takes just one positional argument: our dataset.
2. By default, matplotlib will create a histogram with 10 bins of equal size spanning from the smallest sample to the largest sample in our dataset.
3. If we want to change the number of bins we can use the keyword argument "bins".
4. Bins accepts one integer.
5. Bins allows us to see more detail in our histogram.
6. If we want to zoom in on a specific piece of our dataset, we can use the keyword "range" to set the minimum and maximum value for our histogram.
7. Note that we give the minimum and maximum values inside of a second set of parenthesis, separated by a comma

**Normalizing** -

`plt.hist(values, density=True)`

1. For some reasons we are able to collect many more samples of category_a but not a lot of category_b.
2. Then, when we plot both histograms on the same axes, we can't actually see the difference in the distributions.
3. Instead, we care about what proportion of the dataset has that weight.
4. We can solve this problem with normalization.
5. Normalization reduces the height of each bar by a constant factor so that the sum of the areas of each bar adds to one.
6. This would make our two histograms comparable, even if the sample sizes are different.
7. We can normalize our histogram by using the keyword argument density equals True.
8. Now each bar represents a proportion of the entire dataset.
