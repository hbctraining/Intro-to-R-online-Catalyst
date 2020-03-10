# Introduction

Welcome to segment 7A. In this segment we will be learning a few new functions and using them to set up for learning the basics of plotting with ggplot.

## Setting up a data frame for visualization

We already have a metadata data frame with information about each of the samples. We want to add two more columns, the first one is the average gene expression in a sample, and the second one is the age of each of the mice that make up each of our samples.

[[[ADD IMAGE OF FINISHED DATA FRAME]]]

So, let's talk about getting the average expression for each sample. We can get this information from the counts data frame that we created using read.csv() in segment \_\_\_. Each column in the counts data frame has the gene expression for a sample in our experiment, and we can use the mean function to get the average expression. 

This is how we would get the average expression in sample1:
```r
mean(rpkm_ordered$sample1)
```

This method is great for a single sample, or a single column, but we need to get this information for all 12 samples. What is the best way to do this without having to run the mean function 12x times and accurately representing that information?

Programming languages typically have a way to loop through the same few lines of code multiple times. R has many ways to do this type of looping - one can write out a "for loop" or use functions belonging to either the `apply()` or the `map()` families to achieve looping. 

Here we are going to use the map family of functions from the purrr package (purr with 3 rs), which is part of the tidyverse suite of packages.

### The `map` family of functions

We have linked the [R for Data Science](http://r4ds.had.co.nz/iteration.html#the-map-functions) book in the "resources" (??), which goes into a detailed information about the map family of functions. 

Simply, this family includes several functions, each has a very specific input and output.

For example, we can use these functions to execute some task/function on every element in a vector, or every column in a dataframe, or every component of a list, and so on. 

[[[ADD IMAGE OF the list below]]]

- `map()` creates a list.
- `map_lgl()` creates a logical vector.
- `map_int()` creates an integer vector.
- `map_dbl()` creates a "double" or numeric vector.
- `map_chr()` creates a character vector.

[[[ADD IMAGE OF the code below]]]

these functions have 2 arguments, first is the input object and second is the name of the function you want to use to iteratively use on the input object.

```r
## DO NOT RUN
map(object, function_to_apply)
```

### Wrangling our data with `map_dbl()`

We need to get a vector of numeric values with the mean function, so we will be using the map_dbl() function. This function takes in a data frame or a matrix and performs the given function on each column. It is important to note that if you want to iterate over the rows, you might want to use the apply function.

First, we need to load the library.

```r
library(purrr)  # Load the purrr
```

Next, we will run the map_dbl function on the counts data, such that we get the average for each column.

```r
map_dbl(rpkm_ordered, mean) 
```

The output of this function is a vector of 12 values. This is a named vector, and this is why it looks a little different than other vectors we have encountered before.

Now, let's run it again and this time we can save the our output in an object called samplemeans.

```r
samplemeans <- map_dbl(rpkm_ordered, mean) 
```






We can add this 12 element containing vector as a column to our metadata data frame, thus combining the average expression with experimental metadata. The `cbind()` or "column bind" function allows us to do this very easily.
	
```r
new_metadata <- cbind(metadata, samplemeans)
```

Before we start to plot, we also want to add an additional metadata column to `new_metadata`, this new column lists the age of each of the mouse samples in days.

```r
age_in_days <- c(40, 32, 38, 35, 41, 32, 34, 26, 28, 28, 30, 32)    
# Create a numeric vector with ages. Note that there are 12 elements here.
	
new_metadata <- cbind(new_metadata, age_in_days)    
# add the new vector as the last column to the new_metadata dataframe
```

We are now ready for plotting and data visualization!
