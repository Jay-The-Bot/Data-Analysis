# Introduction to Data Visualization with Seaborn

## Visualizing Two Quantitative Variables

### Introduction to relational plots and subplots

Many questions in data science are centered around describing the relationship between two quantitative variables.

Seaborn calls plots that visualize this relationship as **Relational Plots**. So far we've seen several examples of questions about the relationships between two quantitative variables, and we answered them with **Scatter** plots.

Because they look at the relationship between two quantitative variables, these scatter plots are all considered as relational plots.

While looking at a relationship between two variables at a high level is often informative, sometimes we suspect that the relationship may be different within certain subgroups.

In this lesson, we'll try out a different method: creating a separate plot per subgroup. To do this, we're going to introduce new seaborn function: _relplot()_

**relplot()** -

1. stands for relational plot and enables you to visualize the relationship between two quantitative variables using scatter plot or line plot.
2. Using _relplot_ gives us a big advantage to create subplots in a single figure.

### Customizing scatter plots

Scatter plot are a great tool for visualizing the relationship between two quantitative variables. We've seen a few ways to add more information to them as well, by creating subplots with different colored points.

In addition to these, Seaborn allows to add more information to scatter plots by varying the size, and the transparency of the points.

All of the options can be used in both _scatterplot()_ and _relplot()_.

### Introduction to line plots

In Seaborn, we have two types of relational plots: scatter plots and line plots.

While each point in the scatter plot is assumed to be an independent observation, line plots are the visualization fo choice when we need to track same thing over time.

A common example is tracking the value of a company stock over time.

By specifying _kind_ to _line_ we can create a line plot an more easily see how the average nitrogen dioxide level fluctuates throughout the day.

We can also track subgroups over time with line plots.

## Types of Functions -

1. `sns.relplot(x='total_bill', y='tip', data=tips, kind='scatter', col='smoker', row='time', col_wrap=2, size='size', style='smoker')` -
   1. To make a **relplot()**, we change the function name to relplot() use the _kind_ parameter to specify what kind of relational plot to use - _scatter plot or line plot_.
   2. In this case, we'll set kind equal to word _scatter_.
   3. By setting the col to _smoker_, we get a separate scatter plot for smokers and non-smokers, arranged horizontally in columns.
   4. If you want to arrange these in rows instead of columns, we can use the **row** parameter instead of **col**.
   5. E.g - `sns.relplot(x='total_bill', y='tip', data=tips, kind='scatter', row='smoker')`.
   6. It is possible to use both **row** and **col** together at the same time.
   7. Now we have subplot for each combination of these two categorical variables.
   8. If there are many subplots in a single row, to address this, you can use the **col_wrap** parameter to specify how many subplots you want per row.
   9. Here, we set _col_wrap_ equal to two plots per row.
   10. We can also change the order of the plots using the **col_order** and **row_order** parameters and giving it a list of ordered values.
   11. E.g - `sns.relplot(x='total_bill', y='tip', data=tips, kind='scatter', col='smoker', row='time', col_wrap=2, col_order=["Thur", "Fri", "Sat", "Sun"])`.
   12. We want each point on the scatter plot to be sized based on the number if the people in the group, with larger groups having bigger points on the plot.
   13. To do this, we'll set the _size_ parameter qual to variable name _size_ from our dataset.
   14. Varying point size is is best used if the variable is either quantitative or a categorical variable that represents different levels of something, like _small_, _medium_, _large_.
   15. This plot is a bit hard to read because all of the points are of the same color. We can make it easier to see by using the _size_ parameter with the _hue_ parameter.
   16. Since, size is a quantitative variable, Seaborn will automatically color the points different shades of same color instead of different colors per category like we saw in the previous plots.
   17. Setting the _style_ parameter to a variable name will use different point styles for each value of the variable.
   18. Setting the alpha parameter to a value between 0 and 1 will wary the transparency of the points in the plot, with 0 being completely transparent and 1 being completely non-transparent.
   19. This customization can be useful when you have many overlapping points on the scatter plots, so you can see which areas of the plot have more or less observations.
2. `sns.relplot(x='hour', y='NO_2_mean', data=air_df_loc_mean, kind='line', style='location', hue='location', marker=True, ci='sd')` -
   1. By specifying _kind_ to _line_ we can create a line plot an more easily see how the average nitrogen dioxide level fluctuates throughout the day.
   2. We can also track subgroups over time with line plots.
   3. Setting the _style_ and _hue_ parameters equal to the variable name _location_ creates different lines for each region that vary both line styles and colors.
   4. Setting the _marker_ parameter to true will display a marker for each data point. The marker will vary based on the subgroup you've set using the _style_ parameter.
   5. If you don't want the line styles by subgroup, set the _dashes_ parameter equal to _False_.
   6. Line Plots can also be used when you have more than one observation per x-value.
   7. If the line plot is given multiple observations per x-value, it will aggregate them into a single summary measure. By default, it will display _mean_.
   8. Seaborn will automatically calculate the confidence interval for the mean, displayed in a shaded region.
   9. This confidence interval tells us that based on our sample, we can be 95% confident that the average mean is within this interval.
   10. Confidence interval indicate the uncertainty we have about what the true mean is for the whole city.
   11. Instead of visualizing a confidence interval, we may want to see how varied the measurements of nitrogen dioxide are across the different collection stations at a given point in time.
   12. To visualize this, set the **ci** parameter equal to the string _sd_ to make the shaded area represent the standard deviation, which shows the spread of the distribution of observations at each x value.
   13. We can also turn off the confidence interval by setting the _ci_ parameter equal to _None_ (Not in a string).
