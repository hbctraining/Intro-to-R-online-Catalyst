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

Now that we have the required aesthetics, let's add some extras like color to the plot. We can **`color` the points on the plot based on genotype**, by specifying the column header as the input to the color argument within the aes function. 

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype)) 
```

Colors are automatically assigned to each of the two genotypes and a **legend has been conveniently plotted for us.**

 ![ggscatter1.1](../img/ggscatter-2.png) 

Alternatively, we could color based on celltype or any other column that is a factor. We could have used a numerics or a character column as input too, but that will results in each row getting a distinct color. Which may or may not be good for vizualization.

 Let's try another argument in the aes function called shape, and give it the celltype column as input.  

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype, shape=celltype)) 
```

The data point for each celltype gets a differently shaped data point now and an additional legend representing that also appears. 


 ![ggscatter3](../img/ggscatter-3.png) 


This is a nice way to overlay the information in columns with categorical data onto the basic plot. Other arguments for the aes function can also accept continuous data and color the plot using a gradient. 


Next, let's talk about modifying the data points independent of the information in the input data frame. 

If we wanted to update the size of all the data points to the same size, we can use the size argument outside aes, but within the `geom_point()` function. 

```r
ggplot(new_metadata) +
  geom_point(aes(x = age_in_days, y= samplemeans, color = genotype,
  			shape=celltype), size=2.25) 
```

Here, we want size equal to 2.25; this number is not specifying a relative size, it is actually an arbitrary number that we came up with after testing several values. 

 ![ggscatter4](../img/ggscatter-4.png)
  
It is possible to specify size relative to default, this is done using the rel function. We will be using that function in Segment 7C.

## Conclusion

