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

You can then use the assignment operator to assign value to it. The value will be the function that you define.

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


The last line of the code is the value that will be returned by the function. It is not necessary that a function return anything, for example a function that makes a plot might not return anything, whereas a function that does a mathematical operation might return a number, or a list of numbers. 

```r
name_of_function <- function(argument1, argument2, ...) {
    statements or code that does something
    statements or code that does something
    ...
    return(something)
}
```


Let's try creating a simple example function. This function will take in a numeric value as input, and return the squared value.

We will call the function `square_it`, and assign the value to be function() function. We will add the argument `x` inside the parentheses. `x` will be the numeric value required as input from the user.

```r
square_it <- function(x) {

}
```

Inside the curly brackets we will add a line of code. The something that we want to do here, is square the input value `x`. A variable called square is created to store the result of x times x:

```r
square_it <- function(x) {
square <- x * x
}
```

Finally, we add a return statement, returning the variable `square` to the user.

```r
square_it <- function(x) {
    square <- x * x
   return(square)
}
```

To be able to use this function, it needs first to be read into memory. This is just like loading a library, until you do it the functions contained within it cannot be called.

To do this, highlight the chunk of code and run it in the console. Now, if you look in your environment tab and scroll down, you should see a new section called "Functions". Here, you will see `square_it` listed there.

We can now use the `square_it` function as we would any other function. We type out the name of the function, and inside the parentheses provide a numeric value `x`:

```r
square_it(5)
```

The important idea behind functions is that objects that are created within the function are local to the environment of the function – they don’t exist outside of the function. Take a look at your environment. Even though inside the function a variable called `square` has been created, we do not observe that in our global environment. Only the value that is returned from the function, is being passed into the global environment.

Note that we could have also created this function without the return statement. However, if we do it that way we would also forgo creating the square variable:

```r
# Alternative way of defining the same function
square_it <- function(x) {
    x * x
}
```

If we highlight and run this code in the console, this will overwrite the function currently loaded in memory. Now try using it as we had done before. You should see teh same value being returned.

```r
square_it(5)
```

Let's try one more example to demonstrate the use of multiple arguments. This time we will create a function called `multiply_it` which takes into two arguments: a numeric value `x` and a numeric value `y`. The function will return the product of these two values.


```r
multiply_it <- function(x, y){
    x * y
}
```

Once you have run the function in your console, test it out with x = 4 and y =8. The number 32 should be returned in the console.

```r
multiply_it(4, 8)
```

Setting default options for arguments can be helpful at times. For example, if the user does not pass all the arguments required by function, then it will result in an error. Try this with `multiply_it`:

```r
multiply_it(4)
```

One reason to pass default arguments could be to avoid failure of the function. Values that serve as "good enough" are used and then they can always be changed by the user if required. However, it really depends upon the use case. Although a default does not make sense in this case, we will test it out to show how it works. Re-define the function setting the value of `y = 1` so that the user is only required to specify a value for x:

```r
multiply_it <- function(x, y = 1){
    x * y
}
```

Once you have run the function in your console, test it out first with a single value x = 4. The number 4 should be returned in the console.

```r
multiply_it(4)
```

What if we provided a y-value? The default gets overwritten by the value provided:

```r
multiply_it(4, 8)
```


Pretty simple, right? In this case, we only had one line of code that was run, but in theory you could have many lines of code to get obtain the final results that you want to "return" to the user. We have only scratched the surface here when it comes to creating functions! We will revisit this in later lessons, but if interested you can also find more detailed information on this [R-bloggers site](https://www.r-bloggers.com/how-to-write-and-debug-an-r-function/), which is where we adapted this example from.

