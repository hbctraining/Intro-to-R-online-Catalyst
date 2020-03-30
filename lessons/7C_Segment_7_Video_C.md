# Introduction

Welcome to segment 7C. You will need to have worked through Segment 7A and Segment 7B prior to starting this segment.

In this segment we will continue working with the scatter plot we created in Segment 7B and update the plot's appearance by changing its background, giving the axes some titles and so on.

## Theme layers

Let's start by talking about theme layers. The ggplot2 `theme` system handles non-data plot elements such as:

* Axis label aesthetics
* Plot background
* Facet label backround
* Legend appearance

ggplot2 has preset theme functions, for example `theme_bw()`, `theme_classic()` and so on that can be added as layers to the existing ggplot code chunk. These functions are preset to change one or more of the non-data elements mentioned above. Usually, they are used to change the background/foreground colours. 

In addition, we can adjust specific elements of by adding the `theme()` layer to modify these non-data elements in the plot. 

Finally, it is possible to use both a preset theme and a theme function with any customized modifications. In fact, a ggplot code chunk can have multiple theme layers.

Let's add one of the preset layers, `theme_bw()` to the plot from segment 7B by adding a plus at the end of the geom later and typing theme underscore b w on the next line.

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() 
```

What happens when you run it? What changes? Do the axis labels or the tick labels change with this theme?

Let's change the size of the labels on the x- and y-axis. This time we will add a new theme layer that is the `theme()` function and specify arguments within it to change the sizes.

Since we are adding this layer on top (i.e later), any features we change will override what is set in the `theme_bw()`. Here we'll **increase the size of the axes labels to be 1.5 times the default size.** 

The argument we are specifying the theme() layer is `axis.title` - which updates anything to do with the titles of the 2 axes. We want to change something about the text element so we use the function `element_text()` as input to that argument. Specifically, we want to change the size of the text, so within the element_text function we specify the argument size and give it the output of the rel() or relative function as input. When modfying the size of text we often use the `rel()` function to specify a size that is relative to the default.


```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y = samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.title = element_text(size=rel(1.5)))			
```

Make sure you are closing any parenthesis you open!

You can specify multiple arguments within the same theme layer. For example, if you wanted to update the size of the tick labels to be a little smaller, you can add a comma within the theme function, and add another argument called axis.text() and give it a similar input as what we just did for axis.text.

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y = samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.title = element_text(size=rel(1.5)),
        axis.text = element_text(size=rel(0.75)))			
```
 
![ggscatter5](../img/ggscatter-5.png)
 

Pause this video and work on the following exercises. When you are done, restart the video and I will walk through the solution. 

***

**Exercise**

Update your plot with a few new layers by giving the axes some descriptive names and giving the plot a title!

1. The current axis label text defaults to what we gave as input to `geom_point` (i.e the column headers). We can change this by **adding additional layers** called `xlab()` and `ylab()` for the x- and y-axis, respectively. Add these layers to the current plot such that the x-axis is labeled "Age (days)" and the y-axis is labeled "Mean expression".
2. Use the `ggtitle` layer to add a title to your plot. 
3. Add the following layer to your code chunk `theme(plot.title=element_text(hjust=0.5))`. What does it do? How do you think `theme(plot.title=element_text(hjust=1))` might have changed the output?

***

So, the first thing we want to do is add a layer called xlab() with the argument "Age (days)" within quotations.

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y = samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.title = element_text(size=rel(1.5)),
        axis.text = element_text(size=rel(0.75)))	+
  xlab("Age (days)")
```

Next, let's add a layer called ylab() with the argument "Mean expression" within quotations

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y = samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.title = element_text(size=rel(1.5)),
        axis.text = element_text(size=rel(0.75)))	+
  xlab("Age (days)") +
  ylab("Mean expression")
```

Now let's add a title with the ggtitle() function and some text that describes the plot.

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y = samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.title = element_text(size=rel(1.5)),
        axis.text = element_text(size=rel(0.75)))	+
  xlab("Age (days)") +
  ylab("Mean expression") +
  ggtitle("First scatterplot in ggplot!")
```

Great! Now our plot looks a little better!

Let's work on question 3 of the exercise now and add the theme layer specified in the exercise.

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y = samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.title = element_text(size=rel(1.5)),
        axis.text = element_text(size=rel(0.75)))	+
  xlab("Age (days)") +
  ylab("Mean expression") +
  ggtitle("First scatterplot in ggplot!") +
  theme(plot.title=element_text(hjust=0.5))
```
What changed? Your title should now be centered! 
If instead of saying hjust = 0.5, you had instead said hjust = 1, the title would have been over to one side of the plot.

## Consistent formatting using custom functions

When publishing, it is helpful to ensure all plots have similar formatting. To do this we can create a custom function with our preferences for the theme. Remember the structure of a function is:

```r
name_of_function <- function(arguments){
    statements or code that does something
}
```

Now, let's suppose we always wanted our theme to include the following:

```r
theme_bw() +
theme(axis.title=element_text(size=rel(1.5)),
      axis.text=element_text(size=rel(0.75)),
      plot.title=element_text(hjust=0.5)) 
```

If there is nothing that we want to change when we run this, then we do not need to specify any arguments. Creating the function is simple; we can just put the code inside the `{}`:

```r
personal_theme <- function(){
  theme_bw() +
  theme(axis.title=element_text(size=rel(1.5)),
        axis.text=element_text(size=rel(0.75)),
        plot.title=element_text(hjust=0.5)) 
}
```

Now to run our personal theme with any plot, we can use this function in place of the `theme()` code:

```r
ggplot(new_metadata) +
  geom_point(aes(x=age_in_days, y=samplemeans, color=genotype, shape=celltype), size=rel(3.0)) +
  personal_theme() +
  xlab("Age (days)") +
  ylab("Mean expression") +
  ggtitle("Expression with Age")
```

### Customizing data point colors

The plot is looking better, but it is hard to distinguish differences in significance based on the colors used. There are cheatsheets available for specifying the base R colors by [name](https://greggilbertlab.sites.ucsc.edu/teaching/rtransition/) or [hexadecimal](http://www.r-graph-gallery.com/41-value-of-the-col-function/) code. We could specify other colors available or use pre-created color palettes from an external R package. 

To make additional color palettes available for plotting, we can load the RColorBrewer library, which contains color palettes designed specifically for the different types of data being compared.

```r
# Load the RColorBrewer library
library(RColorBrewer)

# Check the available color palettes
display.brewer.all()
```

![rcolorbrewer_palettes](../img/Rcolorbrewer_palettes.png)

The output is separated into three sections based on the suggested palettes for sequential, qualitative, and diverging data. 

- **Sequential palettes (top):** For sequential data, with lighter colors for low values and darker colors for high values.
- **Qualitative palettes (middle):** For categorical data, where the color does not denote differences in magnitude or value.
- **Diverging palettes (bottom):** For data with emphasis on mid-range values and extremes.

Since our adjusted p-values are sequential, we will choose from these palettes. Let's go with the "Yellow, orange, red" palette. We can choose how many colors from the palette to include, which may take some trial and error. We can test the colors included in a palette by using the `display.brewer.pal()` function, and changing if desired:

```r
# Testing the palette with six colors
display.brewer.pal(6, "YlOrRd")
```

The yellow might be a bit too light, and we might not need so many different colors. Let's test with three different colors:

```r
# Testing the palette with three colors
display.brewer.pal(3, "YlOrRd")

# Define a palette
mypalette <- brewer.pal(3, "YlOrRd")

# how are the colors represented in the mypalette vector?
mypalette
```

Those colors look okay, so let's test them in our plot. We can add a color scale layer, and most often one of the following two scales will work:

- **`scale_color_manual()`:** for categorical data or quantiles
- **`scale_color_gradient()` family:** for continuous data. 


## Conclusion


