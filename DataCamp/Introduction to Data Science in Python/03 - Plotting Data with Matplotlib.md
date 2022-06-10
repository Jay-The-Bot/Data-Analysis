# Introduction to Data Science in Python

## Plotting Data with Matplotlib

### Creating Line Plots

1. A **Line Plot** uses a coordinate grid to plot a series of points and then connect each point using a line.
2. In order to create a line plot, we'll need to import the module matplotlib.
3. To load load only the sub module pyplot we use this statement ->
   E.g- `from matplotlib import pyplot as plt`.
4. Once we have loaded the modules we can use the functions ->
   E.g- `plt.plot(x_values, y_values) and plt.show()`

**Multiple Lines** -

1. If we want to add multiple lines on the same axis, we can just add a second `plt.plot()` command before adding `plt.show()`.
2. **Matplotlib** will automatically give these 2 lines different colors.

## Adding Text to Plots

1. When we share our graphs with an audience, we must add labels to make it clear what we've plotted and why it's important.
2. If we have multiple lines in a single plot we want to add legends.

### Legends

There are 2 steps for adding a legend -

1. First we must add the keyword argument label to each instance of `plt.plot()`. The label would be the string that we want in our legend. By adding a label to each `plt.plot()` function, we make our code easier to read.
2. In order to add a legend to a plot we must add a final function - `plt.legend()`.

### Axes Labels

1. We can label the horizontal (or _x_) axis using the command `plt.xlabel()`.
2. We can label the vertical (or _y_) axis using the command `plt.ylabel()`.
3. We can add these labels in any place in our code as long as they come before `plt.show()`.

### Arbitrary Text

1. Sometimes, we just want to add a quick note directly to our plot.
2. We can do this by using `plt.text()`.

### Modifying Text

1. Whether we are adding labels, legends, or arbitrary text, we might want to modify the letters in some way.
2. There are 2 easy keyword arguments that we can add to any of our functions to change the text is displayed.
3. If we want to change the **Size** of font, we can use the keyword argument `fontsize` and pass in a float.
   E.g- `plt.title("Plot Title", fontsize=20)`
4. If we want to change the **Color** of the font, we can use the keyword argument color and pass in string.
   E.g- `plt.legend(color="green")`

## Styling Graph

### Changing Line Color

1. We can do this by adding the keyword `color` to the `plt.plot()` command.
   E.g- `plt.plot(x, y, color="orange")`.

### Changing Line Width

1. The default line is 1, but you can increase it using the keyword argument `linewidth`.
   E.g- `plt.plot(x, y, linewidth=3)`

### Changing Line Style

1. We can create different types of dashed lines using the keyword argument `linestyle`.
2. `Linestyle` accepts several strings which correspond to different types of dashing.
3. Types of Linestyle -
   1. `plt.plot(x, y, linestyle='-')` -> Normal Line.
   2. `plt.plot(x, y, linestyle='--')` -> Dashed Line.
   3. `plt.plot(x, y, linestyle='-.')` -> Dot/Dash Line.
   4. `plt.plot(x, y, linestyle=':')` -> Dotted Line.

### Adding Markers

1. Adding markers is a great way to distinguish between different lines or to emphasize the location of a data point.
2. Types of Markers -
   1. `plt.plot(x, y, marker='x')` -> X.
   2. `plt.plot(x, y, marker='s')` -> Square.
   3. `plt.plot(x, y, marker='o')` -> Circle.
   4. `plt.plot(x, y, marker='d')` -> Thin Diamond or Diamond.
   5. `plt.plot(x, y, marker='*')` -> Star.
   6. `plt.plot(x, y, marker='h')` -> Hexagon.

### Setting a Style

1. We can change the background, colors, and fonts of our entire graph by setting a style.
2. E.g of Types of Styles -
   1. `plt.style.use('fivethirtyeight')`
   2. `plt.style.use('ggplot')`
   3. `plt.style.use('seaborn')`
   4. `plt.style.use('default')` -> This plot style is selected from default.

## Types of Functions

1. `plt.xlabel()` - Used for labelling the horizontal or _x - axis_.
   1. This function takes one argument - a string value that represents what we want the label to read.
2. `plt.ylabel()` - Similarly we can label the vertical (or _y_) axis.
   1. Argument must be a string.
3. `plt.title()` - We can give our plot a title.
   1. Argument must be a string.
4. `plt.legend()` - Used to add legends in the plots.
   1. Like `plt.show()`, `plt.legend()` does not take any arguments.
   2. It just tells **Matplotlib** to use the _labels_ from our `plt.plot()` functions to create a legend.
5. `plt.text()` - Add text to our graph.
   1. This function takes 3 inputs.
   2. The x - coordinate.
   3. The y - coordinate.
   4. The text to be displayed as a string.
   5. `plt.text(xcoord, ycoord, "Text Message")`
