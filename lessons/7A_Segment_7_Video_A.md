---
title: Plotting and data visualization in R
author: Mary Piper, Meeta Mistry, Radhika Khetani
date: "Wednesday, September 8, 2017"
---

Approximate time: 60 minutes

## Learning Objectives 

* Plot graphs using the external package "ggplot2".
* Use the "map" function for iterative tasks on data structures.
* Export plots for use outside of the R environment.

## Setting up a data frame for visualization

In this lesson we want to make various plots related to the average expression in each sample. When we make the plots, we also want to use all the metadata available to appropriately annotate the plots. 

Let's take a closer look at our counts data. Each column represents a sample in our experiment, and each sample has ~38K values corresponding to the expression of different transcripts. We want to compute **the average value of expression** for each sample eventually. Taking this one step at a time, what would we do if we just wanted the average expression for Sample 1 (across all transcripts)? We can use the R base package provided function called 'mean()`:

```r
mean(rpkm_ordered[,"sample1"])
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
