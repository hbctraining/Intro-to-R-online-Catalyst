# Introduction

Welcome to segment 7A. In this segment we will be learning a few new functions and using them to set up for learning the basics of plotting with ggplot.

## Setting up a data frame for visualization

We already have a metadata data frame with information about each of the samples. We want to add two more columns, the first one is the average gene expression in a sample, and the second one is the age of each of the mice that make up each of our samples.

So, let's talk about getting the average expression for each sample. We can get this information from the counts data frame that we created using read.csv() in segment \_\_\_. Each column in the counts data frame has the gene expression for a sample in our experiment, and we can use the mean function to get the average expression. 

This is how we would get the average expression in sample1:
```r
mean(rpkm_ordered$sample1)
```

That is great, if we only wanted the average from one of the samples (1 column in a data frame), but we need to get this information from all 12 samples, so all 12 columns. What is the best way to do this?

Programming languages typically have a way to allow the execution of a single line of code or several lines of code multiple times, or in a "loop". While "loops" are possible in R, there are functions that more directly achieve this purpose, such as the `apply()` family of functions and the `map()` family of functions. The `map()` family is a bit more intuitive to use than `apply()`, so we will explore this family in more detail. However, we have [similar materials available](https://hbctraining.github.io/Intro-to-R/lessons/apply_functions.html) using the `apply()` function if you would like to explore more on your own.

### The `map` family of functions

The `map()` family of functions is available from the **`purrr`** package, which is part of the tidyverse suite of packages. More detailed information is available in the [R for Data Science](http://r4ds.had.co.nz/iteration.html#the-map-functions) book. This family includes several functions, each taking a vector as input and outputting a vector of a specified type. For example, we can use these functions to execute some task/function on every element in a vector, or every column in a dataframe, or every component of a list, and so on. 

- `map()` creates a list.
- `map_lgl()` creates a logical vector.
- `map_int()` creates an integer vector.
- `map_dbl()` creates a "double" or numeric vector.
- `map_chr()` creates a character vector.

The syntax for the `map()` family of functions is: 

```r
## DO NOT RUN
map(object, function_to_apply)
```

If you would like to practice with the `map()` family of functions, we have [additional materials](https://hbctraining.github.io/Intro-to-R/lessons/map_purrr.html) available.
### Wrangling our data with `map_dbl()`

To obtain **mean values for all samples** we can use the `map_dbl()` function which generates a numeric vector. 

```r
library(purrr)  # Load the purrr

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
