### User-defined Functions

One of the great strengths of R is the user's ability to add functions. Sometimes there is a small task (or series of tasks) you need done and you find yourself having to repeat it multiple times. In these types of situations it can be helpful to create your own custom function. The **structure of a function is given below**:

```r
name_of_function <- function(argument1, argument2) {
    statements or code that does something
    return(something)
}
```

* First you give your function a name. 
* Then you assign value to it, where the value is the function. 

When **defining the function** you will want to provide the **list of arguments required** (inputs and/or options to modify behaviour of the function), and wrapped between curly brackets place the **tasks that are being executed on/using those arguments**.  The argument(s) can be any type of object (like a scalar, a matrix, a dataframe, a vector, a logical, etc), and it’s not necessary to define what it is in any way. 

Finally, you can **“return” the value of the object from the function**, meaning pass the value of it into the global environment. The important idea behind functions is that objects that are created within the function are local to the environment of the function – they don’t exist outside of the function. 

> **NOTE:** You can also have a function that doesn't require any arguments, nor will it return anything.

Let's try creating a simple example function. This function will take in a numeric value as input, and return the squared value.

```r
square_it <- function(x) {
    square <- x * x
    return(square)
}
```

Now, we can use the function as we would any other function. We type out the name of the function, and inside the parentheses  we provide a numeric value `x`:

```r
square_it(5)
```

Pretty simple, right? In this case, we only had one line of code that was run, but in theory you could have many lines of code to get obtain the final results that you want to "return" to the user. We have only scratched the surface here when it comes to creating functions! We will revisit this in later lessons, but if interested you can also find more detailed information on this [R-bloggers site](https://www.r-bloggers.com/how-to-write-and-debug-an-r-function/), which is where we adapted this example from.

