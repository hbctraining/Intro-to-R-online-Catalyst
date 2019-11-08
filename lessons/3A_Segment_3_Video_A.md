## Functions and their arguments

### Introduction

So far you have been introduced to R and RStudio, and you are now familiar with some basic syntax of the R programming language. We have also explored the different data types and data structures that you will encounter when working in R. Through all of this, we have used a few examples of basic functions yet we haven't really talked much about them - so now let's take the time to delve into functions in more detail.

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

For now, we will continue to use the base functions we have available in our current environment. Since R is used for statistical computing, many of the base functions involve mathematical operations. One example would be the function `sqrt()`. The input/argument must be a number, and the output is the square root of that number. Let's try finding the square root of 81:

```r
sqrt(81)
```

Now what would happen if we **called the function** (e.g. ran the function), on a *vector of values* instead of a single value? 

```r
sqrt(glengths)
```

In this case the task was performed on each individual value of the vector `glengths` and the respective results were displayed.


Let's try another function, this time using one that we can change some of the *options* (arguments that change the behavior of the function), for example `round`:

```r
round(3.14159)
```

We can see that we get `3`. That's because the default is to round to the nearest whole number. **What if we want a different number of significant digits?**


### Seeking help on arguments for functions

The best way of finding out this information is to use the `?` followed by the name of the function. Doing this will open up the help manual in the bottom right panel of RStudio that will provide a description of the function, usage, arguments, details, and examples: 

```r
?round
```	
Alternatively, if you are familiar with the function but just need to remind yourself of the names of the arguments, you can use:

```r
args(round)
```

Even more useful is the `example()` function. This will allow you to run the examples section from the Online Help to see exactly how it works when executing the commands. Let's try that for `round()`:

```r
example("round")
```

In our example, we can change the number of digits returned by **adding an argument**. We can type `digits=2` or however many we may want:


```r
round(3.14159, digits=2)
```

> *NOTE:* If you provide the arguments in the exact same order as they are defined (in the help manual) you don't have to name them:
>
	round(3.14159, 2)
>
>However, it's usually not recommended practice because it involves a lot of memorization. In addition, it makes your code difficult to read for your future self and others, especially if your code includes functions that are not commonly used. (It's however OK to not include the names of the arguments for basic functions like `mean`, `min`, etc...). Another advantage of naming arguments, is that the order doesn't matter. This is useful when a function has many arguments. 


***
**Exercise** 

1. Another commonly used base function is `mean()`. Use this function to calculate an average for the `glengths` vector.
2. Use the help manual to identify additional arguments for `mean()`.

***

> **Missing values**
> 
> By default, all **R functions operating on vectors that contains missing data will return NA**. It's a way to make sure that users know they have missing data, and make a conscious decision on how to deal with it. When dealing with simple statistics like the mean, the easiest way to ignore `NA` (the missing data) is to use `na.rm=TRUE` (`rm` stands for remove).
>
> In some cases, it might be useful to remove the missing data from the vector. For this purpose, R comes with the function `na.omit` to generate a vector that has NA's removed. For some applications, it's useful to keep all observations, for others, it might be best to remove all observations that contain missing data. The function `complete.cases()` returns a logical vector indicating which rows have no missing values. 

***
