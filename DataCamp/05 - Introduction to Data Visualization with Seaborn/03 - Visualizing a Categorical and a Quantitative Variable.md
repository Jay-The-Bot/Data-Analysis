# Introduction to Data Visualization with Seaborn

## Visualizing a Categorical and a Quantitative Variable

### Count plots and bar plots

Visualizations that involve categorical variables.

**Count Plot** and **Bar Plot** are two types of visualizations that seaborn calls **Categorical Plots**.

Categorical plots involve a categorical variable, which is a variable that consists of a fixed, typically small number of possible values, or categories. These types of plots are commonly used when we want to make comparisons between different groups.

**Count Plot** displays the number of observations in each category.

In this chapter we will be using _catplot()_ to create different types of categorical plots.

### Box plots

A box plot shows the distribution of the quantitative data. The colored box represents the 25th to 75th percentile, and the line in the middle of the box is the median.

The whiskers give us sense if the spread of the distribution, and the floating points represent the outliers.

Box plots are commonly used as a way to compare the distribution of a quantitative variable across different groups of categorical variable.

The IQR is the 25th to 75th percentile of a distribution of data. The IQR can be added to the "whis" parameter by `whis=0.5` or `whis = [5, 95]`

### Point plots

Point plots show the mean of a quantitative variable for the observations in each category, plotted as single point.

| Point Plot                                                                                                | Line Plot                                                                          |
| --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Shows the mean of quantitative variable and 95 % confidence interval for the mean.                        | Shows the mean of quantitative variable and 95 % confidence interval for the mean. |
| In a point plot, one axis - usually the x-axis - is a categorical variable, making it a categorical plot. | Line plots are relational plots, so both x- and y-axis are quantitative variable.  |

## Types of Functions -

1. `sns.catplot(x='how_masculine', data=masculinity_data, kind='count', order=category_order)` -
   1. _catplot()_ offers the same flexibility as _relplot()_ does, which means it will be easy to create subplots if we need using the same _col_ and _row_ parameters.
   2. Sometimes there is a specific ordering of categories that makes sense for these kinds of plots. In this case, it make more sense for the categories to be in order from not_masculine to very_masculine.
   3. To change the order of the categories, create a list of category values in order that you want them to appear, and then use the _order_ parameter. This works for all types of categorical plots, not just categorical plots.
2. `sns.catplot(x='day', y='total_bill', data=tips, kind='bar', ci=None)` -
   1. Bar plots look similar to count plots, but instead of count of observations in each category, they show the mean of a quantitative variable.among variations in each category.
   2. Seaborn automatically shows 95% confidence intervals for these means.
   3. Just like the line plots, these confidence intervals show us the level of uncertainty we have about these estimates.
   4. Assuming out data is a random sample of some population, we can be 95% sure that the true population mean in each group lies within the confidence interval shown.
   5. If we want to turn off these confidence intervals, we can do this by setting the **ci** to _None_.
   6. Finally, you can also change the orientation of the bars in bar plots and count plots by switching the x and y parameters. However, it is fairly common practice to put the categorical variable on the x-axis.
