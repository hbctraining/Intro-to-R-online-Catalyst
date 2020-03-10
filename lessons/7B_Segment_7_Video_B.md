# Introduction

Welcome to segment 7B. You will need to have worked through Segment 7A prior to starting this segment. 

Here, we will be going through the fundamentals of using ggplot2 to create plots.

## Data Visualization with `ggplot2`

When we are working with large sets of numbers it can be useful to display that information graphically to gain more insight. Here are some plots drawn with ggplot2 that are very effectively communicating complex results or ideas.

[[[[ADD IMAGES OF PLOTS MADE WITH ggplot2]]]]


More recently, R users have moved away from graphing functions in base R towards `ggplot2`. This is because ggplot2 offers a lot more functionality and easier syntax. This syntax is what we will be covering in this segment. It uses functions, but differs from base R in how the functions are combined together.

Let's start by loading the `ggplot2` library.

```r
library(ggplot2)
```


The first plot we will draw is a simple X-Y scatterplot of `samplemeans` versus `age_in_days` from the `new_metadata` data frame you created in Segment 7A.

[[[SHOW IMAGE OF THE FINAL PLOT]]]

The `ggplot()` function is used to **initialize the basic graph structure**, then we add information and customizations by adding additional functions using the `+` operator. 

[[[SHOW IMAGE OF THE FINAL code for the plot]]]

Each function that is added is called a layer. So we will be building a chunk of code, with multiple layers for plotting with ggplot2.

It is important to note that ggplot2 will only accept data frames or tibbles as input. It does not work with other data structures such as matrices, lists or single dimensional objects.

Let's start by initializing the plot with the ggplot function and the new_metadata data frame as input: 

```r
ggplot(new_metadata)
```

You will get a blank plot, because you need to specify layers with information about what you want to plot.

One type of layer is called **geometric object**, or a geom layer in short. You need to specify at least one geom layer, since this is how you specify the kind of plot being drawn. i.e do you want to box plot? or an X-Y scatterplot? os do you want an histogram?

[[[Following list needs to be displayed on a slide]]]

* points (`geom_point`, `geom_jitter` for scatter plots, dot plots, etc)
* lines (`geom_line`, for time series, trend lines, etc)
* boxplot (`geom_boxplot`, for, well, boxplots!)

Listed are some examples of plots and geom functions that would create them.

For a more exhaustive list on all possible geometric objects and when to use them check out [Hadley Wickham's RPubs](http://rpubs.com/hadley/ggplot2-layers) or the [RStudio cheatsheet](https://www.rstudio.com/wp-content/uploads/2016/11/ggplot2-cheatsheet-2.1.pdf). Both these are linked ...

A plot **must have at least one `geom`**; there is no upper limit. You can add a `geom` to a plot using the `+` operator

Since we are plotting a simple scatterplot, we will be using the geom_point() function as our geom layer.

```r
ggplot(new_metadata) +
  geom_point() 
```

Running this code will give an error because we have not specified which column within new_metadata should be used as the X axis and which one should be used as the Y axis.

Anytime information from a column in the input dataframe is used, it has to be within a function called aes(). Aes stands for aesthetics or aesthetic mappings. 

[[[Following list needs to be displayed on a slide]]]

* position (i.e., on the x and y axes)
* color ("outside" color)
* fill ("inside" color) 
* shape (of points)
* linetype
* size

To start, we will add the position for the x- and y-axis within the aes function. And in turn place the aes function within `geom_point`. In this case x is age in days and y is samplemeans.

```r
ggplot(new_metadata) +
     geom_point(aes(x = age_in_days, y= samplemeans))
```







Now that we have the required aesthetics, let's add some extras like color to the plot. We can **`color` the points on the plot based on genotype**, by specifying the column header. You will notice that there are a default set of colors that will be used so we do not have to specify. Also, the **legend has been conveniently plotted for us!**


```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype)) 
```

 ![ggscatter1.1](../img/ggscatter-2.png) 

Alternatively, we could color based on celltype by changing it to `color =celltype`. Let's try something different and have both **celltype and genotype identified on the plot**. To do this we can assign the `shape` aesthetic the column header, so that each celltype is plotted with a different shaped data point. Add in `shape = celltype` to your aesthetic and see how it changes your plot:

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype,
  			shape=celltype)) 
```

 ![ggscatter3](../img/ggscatter-3.png) 


The **size of the data points** are quite small. We can adjust that within the `geom_point()` layer, but does **not** need to be **included in `aes()`** since we are specifying how large we want the data points, rather than mapping it to a variable. Add in the `size` argument by specifying a number for the size of the data point:

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype,
  			shape=celltype), size=3.0) 
```

 ![ggscatter4](../img/ggscatter-4.png)
  

The labels on the x- and y-axis are also quite small and hard to read. To change their size, we need to add an additional **theme layer**. The ggplot2 `theme` system handles non-data plot elements such as:

* Axis label aesthetics
* Plot background
* Facet label backround
* Legend appearance

There are built-in themes we can use (i.e. `theme_bw()`) that mostly change the background/foreground colours, by adding it as additional layer. Or we can adjust specific elements of the current default theme by adding the `theme()` layer and passing in arguments for the things we wish to change. Or we can use both.

Let's add a layer `theme_bw()`. Do the axis labels or the tick labels get any larger by changing themes?

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() 
```

Not in this case. But we can add arguments using `theme()` to change it ourselves. Since we are adding this layer on top (i.e later in sequence), any features we change will override what is set in the `theme_bw()`. Here we'll **increase the size of the axes labels and axes tick labels to be 1.5 times the default size.** When modfying the size of text we often use the `rel()` function. In this way the size we specify is relative to the default (similar to `cex` for base plotting). We can also provide the number vaue as we did with the data point size, but can be cumbersome if you don't know what the default font size is to begin with. 

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype,
  			shape=celltype), size=3.0) +
  theme_bw() +
  theme(axis.text = element_text(size=rel(1.5)),
  		axis.title = element_text(size=rel(1.5)))			
```
 
 ![ggscatter5](../img/ggscatter-5.png)
 

> *NOTE:* You can use the `example("geom_point")` function here to explore a multitude of different aesthetics and layers that can be added to your plot. As you scroll through the different plots, take note of how the code is modified. You can use this with any of the different geometric object layers available in ggplot2 to learn how you can easily modify your plots! 

> *NOTE:* RStudio provide this very [useful cheatsheet](https://www.rstudio.com/wp-content/uploads/2016/11/ggplot2-cheatsheet-2.1.pdf) for plotting using `ggplot2`. Different example plots are provided and the associated code (i.e which `geom` or `theme` to use in the appropriate situation.)


***

**Exercise**

1. The current axis label text defaults to what we gave as input to `geom_point` (i.e the column headers). We can change this by **adding additional layers** called `xlab()` and `ylab()` for the x- and y-axis, respectively. Add these layers to the current plot such that the x-axis is labeled "Age (days)" and the y-axis is labeled "Mean expression".
2. Use the `ggtitle` layer to add a title to your plot. *NOTE: Useful code to center your title over your plot can be done using `theme(plot.title=element_text(hjust=0.5))`.*

***

### Consistent formatting using custom functions

When publishing, it is helpful to ensure all plots have similar formatting. To do this we can create a custom function with our preferences for the theme. Remember the structure of a function is:

```r
name_of_function <- function(arguments) {
    statements or code that does something
}
```

Now, let's suppose we always wanted our theme to include the following:

```r
theme_bw() +
    theme(axis.text=element_text(size=rel(1.5)),
          axis.title=element_text(size=rel(1.5)),
          plot.title=element_text(hjust=0.5))
```

If there is nothing that we want to change when we run this, then we do not need to specify any arguments. Creating the function is simple; we can just put the code inside the `{}`:

```r
personal_theme <- function(){
  theme_bw() +
    theme(axis.text=element_text(size=rel(1.5)),
          axis.title=element_text(size=rel(1.5)),
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

## Boxplot

Now that we have all the required information for plotting with ggplot2 let's try plotting a boxplot. A boxplot provides a graphical view of the distribution of data based on a five number summary. The top and bottom of the box represent the (1) first and (2) third quartiles (25th and 75th percentiles, respectively). The line inside the box represents the (3) median (50th percentile). The whiskers extending above and below the box represent the (4) maximum, and (5) minimum of a data set. The whiskers of the plot reach the minimum and maximum values that are not outliers. 

Outliers are determined using the interquartile range (IQR), which is defined as: Q3 - Q1. Any values that exceeds 1.5 x IQR below Q1 or above Q3 are considered outliers and are represented as points above or below the whiskers. These outliers are useful to identify any unexpected observations.

1. Use the `geom_boxplot()` layer to plot the differences in sample means between the Wt and KO genotypes.
2. Add a title to your plot.
3. Add 'Genotype' as your x-axis label and 'Mean expression' as your y-axis labels.
4. Change the size of your axes labels to 1.5x larger than the default.
5. Change the size of your axes text (the labels on the tick marks) to 1.25x larger than the default.
6. Change the size of your plot title in the same way that you change the size of the axes text but use `plot.title`.

*BONUS: Use the `fill` aesthetic to look at differences in sample means between celltypes within each genotype.*


**Our final figure should look something like that provided below.**

 ![ggbox](../img/ggboxplot_new.png)

> *NOTE:* If you wanted to change the colors of these boxplots you would add another layer `scale_fill_manual()` to the code, and within the function specify which colors you want to use using the `values` argument.  For example, if the factor column you are coloring with has 2 levels, you will need to give 2 values as follows `scale_fill_manual(values=c("purple","orange"))`.
>
> *NOTE:* You are not restricted to colors specified as above, you have the choice of a lot of colors using their *hexadecimal code*, [click here for more information about color palettes in R](http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/).

