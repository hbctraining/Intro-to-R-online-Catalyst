## Introduction

Welcome to segment 3B, **Creating Your Own Functions in R**. In this segment we will show you how to create your own custom functions, describe scenarios in which you may want to do so, and give you a few example functions.


**Slide Title?**

One of the great strengths of R is the user's ability to create their own functions. There are tons of functions built into R, which are available as part of the standard R installation. Even more functionality can be obtained by installing external packages.

However, sometimes there are tasks that are specific to your code and workflow, and you find yourself having to repeat it multiple times. In these types of situations it can be helpful to create your own custom function. 


Slide: **Structure of a Function**:

*Animate: Fade in different parts of the code with the bullets*

```r
name_of_function <- function(argument1, argument2) {
    statements or code that does something
    return(something)
}
```

To create your own function, you will want to start by giving your function a name. 

```r
name_of_function 
```

You can then use the assignment operator to assign value to it, where the value is the function.

```r
name_of_function <- 
```

On the right hand side of the assignment operator we place the function called function(). This is different from other functions in R, in that along with the parentheses after the function name, you also need a set of curly brackets. 

```r
name_of_function <- function() {

}
```

When **defining the function** you will want to provide the **list of arguments required**. These include any inputs required for the function to work and any options that user can provide to modify the default behaviour of the function.  The argument(s) can be any type of object (like a scalar, a matrix, a dataframe, a vector). Remember that a function can also be implemented without requiring any arguments.


```r
name_of_function <- function(argument1, argument2, ...) {

}
```

In between the curly brackets we place the tasks that are being executed, using the inputs if necessary. The code between the curly brackets is run every time the function is called. This code might be very long or very short. 


```r
name_of_function <- function(argument1, argument2, ...) {
    statements or code that does something
    statements or code that does something
    ...
}
```


The last line of the code is the value that will be returned by the function. It is not necessary that a function return anything, for example a function that makes a plot might not return anything, whereas a function that does a mathematical operation might return a number, or a list. The value that is returned, is being passed into the global environment. The important idea behind functions is that objects that are created within the function are local to the environment of the function – they don’t exist outside of the function. 

```r
name_of_function <- function(argument1, argument2, ...) {
    statements or code that does something
    statements or code that does something
    ...
    return(something)
}
```


Let's try creating a simple example function. This function will take in a numeric value as input, and return the squared value.

We will call the function `square_it`, and will assign to it the function() function. We will add the argument `x` inside the parentheses. `x` will be the numeric value required as input from the user.

```r
square_it <- function(x) {

}
```

Inside the curly brackets we will add a line of code. The something that we want to do is square the input value `x`.

```r
square_it <- function(x) {
x * x
}
```

Now, we can use the function as we would any other function. We type out the name of the function, and inside the parentheses  we provide a numeric value `x`:

```r
square_it(5)
```

Pretty simple, right? In this case, we only had one line of code that was run, but in theory you could have many lines of code to get obtain the final results that you want to "return" to the user. We have only scratched the surface here when it comes to creating functions! We will revisit this in later lessons, but if interested you can also find more detailed information on this [R-bloggers site](https://www.r-bloggers.com/how-to-write-and-debug-an-r-function/), which is where we adapted this example from.

