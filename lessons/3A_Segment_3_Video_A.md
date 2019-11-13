## Functions and their arguments

### Introduction

Welcome to segment 3A. In this segment, we will define what a function is in R and discuss how we use them through implementation of arguments. We will also discuss different ways in which you can find help on using functions in R. In other segments, we have used a few examples of basic functions yet we haven't really talked much about them - so now let's take the time to delve into functions in more detail.

### What are functions?

Functions are **"self contained" modules of code that accomplish a specific task**. The general usage for a function is the name of the function followed by parentheses:

```r
function_name(input)
```
Functions usually take in some sort of data structure (value, vector, dataframe etc.) as input. The input is then processed in some way and a result is returned to the user.

The input(s) are called **arguments**, which can include:

1. a physical object (any data structure) on which the function carries out a task 
2. specifications that alter the way the function operates (e.g. options)

Note that not all functions will necessarily take arguments, for example:

```r
# A function with no arguments required
getwd()
```
You can see that the parentheses are present, however there is no value provided inside them and a results is still returned to the user.

While there are many functions like `getwd()`, most functions will take atleast one argument as input and can typically accept up to several arguments. In many cases, a function will require one or two mandatory arguments that the user is required to provide and all other arguments for the function will fall back on using a *default*. 

The **default arguments** represent values that the author of the function has determined as being "good enough in standard cases". An example of a default would be what symbol to use for data points in a plot (i.e. a closed circle). However, if you wanted something specific, simply change the argument yourself with a value of your choice.

### Basic functions

 **All of the functions we will use here are available as part of R's built in capabilities**. However, you can also obtain added functionality to your R environment by downloading and installing external packages which will introduce you to other functions. Alternatively, you can create your own functions in R. Both of these are beyond the scope of this segment, but if you are interested we encourage you to refer to those segments. 

Since R is used for statistical computing, many of the base functions involve mathematical operations. One example would be the function `sqrt()`. The argument for this function is a numeric value, and the output is the square root of that number. Let's try finding the square root of 81:

```r
# Square root function
sqrt(81)
```

Now what would happen if we use a *vector of numeric values* as the argument instead of a single numeric value? We can test it out with the `glengths` vector.

```r
# Observe the contents of glengths
glengths

# Square root function using a numeric vector as an argument
sqrt(glengths)
```

Whaat happened? The square root of each individual value in the vector `glengths` was computed, and the respective results were displayed. Note that this will not always be the case with every function. One way of knowing what the function is expecting as an argument is to check the help documentation. 

### Seeking help on arguments for functions

In R, there are many ways in which you can find help on arguments for a function that you are using. The best and most common way of getting help on a function is to use the `?` followed by the name of the function. 

```r
?sqrt
```	

Doing this will open up the help documentation in the bottom right panel of RStudio. 

(Scroll through the documentation page and highlight each header). 

This documentation will provide a description of the function, some information on usage, details on the different arguments it can take, and some example code. 

(Scroll back to the Arguments section and highlight the text). 

Here, we see that `sqrt()` will take `x` as an argument, where `x` represents a numeric or complex vector or array.

Let's try another function, this time using one in which we can change some of the specifications (arguments that change the behavior of the function). We will use the `round()` function to round a decimal valued number:

```r
# Rounding numbers
round(3.14159)
```

The round function takes a numeric value as input and returns the user with a number rounded to the nearest whole number. **What if we want to retain a number of significant digits?** We can open up the help documentation and find out more:

```r
?round
```	

(Scroll through the documenatation until we reach the Usage/Arguments section).

Here, we see that in addition to a numeric vector, the `round()` function can also be given an argument called `digits` - an integer indicating the number of decimal places to be used. 

(Highlight `round`  usage). By default the `digits` argument is set to zero. 

Alternatively, if you are already familiar with the function but just need to remind yourself of the names of the arguments, you can use the `args()` function:

```r
# Finding the arguments of a function
args(round)
```

What you will see reported in the console is the different arguments the function `round()` will take, in addition what the defaults are set to - but no descriptions are provided here.


Finally, another method of obtaining help is by use of the `example()` function. This will allow you to run the examples section from the help documentation to see exactly how it works when executing the commands. Let's try that for `round()`:

```r
# Seeing how a function works
example("round")
```

This does not appear to be all that helpful in the case of the `round()` function, but it can be when working with functions for visualization. The `example()` function runs some example code and produces a plot. Knowing that you would like to draw a similar plot with your data, you now have the code you would require to do so.


Now that we have discussed the different methods for finding help, let's address the question at hand. **How do we round our number to only keep two significant digits?** Let's use the `digits` argument:

```r
# Rounding with an added argument
round(3.14159, digits=2)
```

Note that we could have also done this without the use of the word `digits`:

```r
round(3.14159, 2)
```

And this works just the same! If you provide the arguments in the exact same order as they are defined in the help manual you don't have to name them. However, **it's usually not recommended practice** because it involves a lot of memorization. In addition, it makes your code difficult to read for your future self and others, especially if your code includes functions that are not commonly used. if you are naming your arguments then the order doesn't matter.

### More functions and missing values

Another commonly used base function is `mean()`. Let's use this function to calculate the arithmetic mean for the `glengths` vector:

```r
# Compute the arithmetic mean
mean(glengths)
```

It works without any additional arguments, but let's see what other arguments we could provide to alter the way this function works.

```r
?mean
```

(Scroll through the help documentation to Arguments). 

We can see that the `trim` argument (which defaults to zero) can be set to a numeric value of 0 to 0.5 representing the fraction of observations to be trimmed from each end of x before the mean is computed. There is also a `na.rm` argument, this is an important feature of many functions in R that perform some statistical computation. The function accepts a logical value indicating whether NA values should be ignored before the computation proceeds.

By default, all **R functions operating on vectors that contains missing data will return NA**. It's a way to make sure that users know they have missing data, and make a conscious decision on how to deal with it. 

(Switch to slide)

When dealing with simple statistics like the mean, the easiest way to ignore `NA` (the missing data) is to use `na.rm=TRUE` (`rm` stands for remove). However, not all functions will have this argument. In some cases, it might be useful to remove the missing data from the vector rather than just ignoring it. For this purpose, R comes with the function `na.omit` to generate a vector that has NA's removed. For other applications, it's useful to keep all observations, fand just note where the missing values are ocurring. The function `complete.cases()` is another option, which returns a logical vector indicating which rows have no missing values. 


### Conclusion

In summary, we have defined for you what a function is in R and provided some instruction on using them by providing different types of arguments. We have presented some tips on finding help when using functions that your are not familiar with, and made special note of an especially useful argument (and additional functions) when you are working with data that has missing values.
