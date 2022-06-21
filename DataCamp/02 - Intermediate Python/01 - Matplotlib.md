# Intermediate Python

## Matplotlib

### Basic plots with Matplotlib

1. Very Important in Data Analytics -
   1. Explore Data
   2. Report Insights
2. The `plt.plot()` function tells the Python what to plot and how to plot it.
3. `plt.show()` actually displays the plot.

**Putting a Axis on Logarithmic Scale** -

`plt.xscale('log')`

1. This will put the x-axis on the logarithmic scale.
2. This also works on the y-axis.
3. The logarithmic scale is useful for plotting data that includes very small numbers and very large numbers because the scale plots the data so you can see all the numbers easily, without the small numbers squeezed too closely.

### Histogram

1. The histogram is a type of visualization that's very useful to explore your data.
2. It can help you to get an idea about the distribution of your variables.
3. The height of the bar corresponds to the number of data points that fall in this bin.

### Customization

1. The first thing you always need to do is label your axes.
2. Make sure to call these functions before calling the show function, otherwise your customizations will not be displayed.
3. Add a title to a plot.
4. We can add points to the array using,

   ```python
      year = [1800, 1850, 1900] + year
      pop = [1.0, 1.262, 1.650] + pop
   ```

5. This will add these 3 data points in the graph.


## Types of Functions

1. `plt.clf()` -
   1. It is used to clear the current figure
2. `plt.yticks()` -
   1. We use this to change the y-label of the plot.
   2. The first input is a list.ind_li
   3. E.g- `plt.yticks([0, 2, 4, 6, 8, 10])`
   4. The second argument which is a list with the display names of the ticks.
   5. This list should have the same length as the first list.
   6. The tick 0 gets the name 0, the tick 2 gets the name 2B, the tick 4 gets the name 4B and so on.
   7. By the way, B stands for Billions here.
   8. E.g- `plt.yticks([0, 2, 4, 6, 8, 10], ['0', '2B', '4B', '6B', '8B', '10B'])`
3. `plt.grid()` -
   1. It has 2 arguments, `True` and `False`.
   2. If it is True it will show the grid lines while creating the plot.
   3. By default it is false.

