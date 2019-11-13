## Functions and their arguments

### Introduction

In this segment, we will define what a function is in R and hwo we use them with the use of arguments. We will also discuss ways in which you can find help on using functions in R. In previous segments, we have used a few examples of basic functions yet we haven't really talked much about them - so now let's take the time to delve into functions in more detail.

### What are functions?

A key feature of R is functions. Functions are **"self contained" modules of code that accomplish a specific task**. Functions usually take in some sort of data structure (value, vector, dataframe etc.), it will process it in some way, and return a result.

The general usage for a function is the name of the function followed by parentheses:

```r
function_name(input)
```
The input(s) are called **arguments**, which can include:

1. the physical object (any data structure) on which the function carries out a task 
2. specifications that alter the way the function operates (e.g. options)

Note that not all functions will necessarily take arguments, for example:

```r
getwd()
```

You can see that the parentheses are present, however there is no value provided inside them.

While there are many functions like `getwd()`, most functions will take atleast one argument as input and can typically accept several arguments. In many cases, a function will require one or two mandatory arguments that the user is required to provide and all other arguments for the function will fall back on using a *default*. 

The **default arguments** represent values that the author of the function has determined as being "good enough in standard cases". An example of a default would be what symbol to use for data points in a plot (i.e. a closed circle). However, if you wanted something specific, simply change the argument yourself with a value of your choice.

### Basic functions

As mentioned, we have already used a few examples of basic functions in the previous lessons i.e `getwd()`, `c()`, and  `factor()`. **All of the functions we have used are available as part of R's built in capabilities**. However, you can also obtain added functionality to your R environment by downloading and installing external packages which will introduce you to other functions. Alternatively, you can create your own functions in R. Both of these are beyond the scope of this segment, but if you are interested we encourage you to refer to those lessons (cite them here?). 

For now, we will continue to use the base functions we have available in our current environment. Since R is used for statistical computing, many of the base functions involve mathematical operations. One example would be the function `sqrt()`. The argument for this function is a numeric value, and the output is the square root of that number. Let's try finding the square root of 81:

```r
sqrt(81)
```

Now what would happen if we **called the function** (e.g. ran the function), on a *vector of numeric values* instead of a single value? 

```r
sqrt(glengths)
```

In this case, the task was executed on each individual value of the vector `glengths` and the respective results were displayed. Note that this will not always be the case with every function.


Let's try another function, this time using one in which we can change some of the *options* (arguments that change the behavior of the function), for example `round()`:

```r
round(3.14159)
```

The round function takes a numeric value as input and returns the user with a number rounded to the nearest whole number. **What if we want to retain a number of significant digits?**


### Seeking help on arguments for functions

In R, there are many ways in which you can find help on arguments for a function that you are using. The best and most common way of getting help on a function is to use the `?` followed by the name of the function. 

```r
?round
```	

Doing this will open up the help documentation in the bottom right panel of RStudio. (Scroll through the documentation page). This documentation will provide a description of the function, some information on usage, details on the arguments it can take, and example code. 

Alternatively, if you are already familiar with the function but just need to remind yourself of the names of the arguments, you can use the `args()` function:

```r
args(round)
```
Here, what you will see reported in the console is the different arguments the function `round()` will take, in addition what the defaults are set to.


Another method of obtaining help is by use of the `example()` function. This will allow you to run the examples section from the help documentation to see exactly how it works when executing the commands. Let's try that for `round()`:

```r
example("round")
```

This does not appear to be all that helpful in the case of the `round()` function, but it can be super helpful when working with functions for visualization. The `example()` function runs some example code and produces a plot. Knowing that you would like to draw a similar plot with your data, you now have the code you would require to do so.


Now that we have discussed the different methods for finding help, let's address the question at hand. **How do we round our number to only keep two significant digits?** The help documentation tells us that we can provide a `digits` argument, which should be an integer indicating the number of decimal places or significant digits:

```r
round(3.14159, digits=2)
```

Note that we could have also done this without the use of the word `digits`:

```r
round(3.14159, 2)
```

And this works just the same! If you provide the arguments in the exact same order as they are defined in the help manual you don't have to name them. However, **it's usually not recommended practice** because it involves a lot of memorization. In addition, it makes your code difficult to read for your future self and others, especially if your code includes functions that are not commonly used. if you are naming your arguments then the order doesn't matter.

### More functions and missing values

Another commonly used base function is `mean()`. Let's use this function to calculate an average for the `glengths` vector:

```r
mean(glengths)
```

Seeing as this is the first time we are using this function, let's see what other arguments we could provide to alter the way this function works.

```r
?mean
```

(Scroll through the help documentation). We can see that at minimum the function requires a numeric vector `x`. We can also set the `trim` argument which would be a numeric value of 0 to 0.5 representing the fraction of observations to be trimmed from each end of x before the mean is computed. And finally there is a `na.rm` argument, this is an important feature of many functions in R that perform some statistical computation. The function accepts a logical value indicating whether NA values should be stripped before the computation proceeds.

By default, all **R functions operating on vectors that contains missing data will return NA**. It's a way to make sure that users know they have missing data, and make a conscious decision on how to deal with it. When dealing with simple statistics like the mean, the easiest way to ignore `NA` (the missing data) is to use `na.rm=TRUE` (`rm` stands for remove).

In some cases, it might be useful to remove the missing data from the vector. For this purpose, R comes with the function `na.omit` to generate a vector that has NA's removed. For some applications, it's useful to keep all observations, for others, it might be best to remove all observations that contain missing data. The function `complete.cases()` is another option, which returns a logical vector indicating which rows have no missing values. 


### Conclusion

In summary, we have defined for you what a function is in R and provided some instruction on using them by providing different types of arguments. We have presented some helpful tips on finding help when using functions that your are not familiar with, and made special note of an especially useful argument (and additional functions) when you are working with data that has missing values.
