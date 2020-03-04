## Selecting data using indices and sequences - Introduction

When analyzing data, we often want to **partition the data so that we are only working with selected columns or rows.** In this segment we will begin with how to subset a one-dimensional data structure, specifically vectors, using indices and sequences. This segment is a precursor to segment 5C and 5D.

### Indices

When we have displayed the contents of vectors previously, you may have noticed a notation to the left, the number one in a set of brackets. Let's take a look:

```r
glengths
```

This notation is called an **index**, and it is telling us that the first element in the `glengths` vector is 4.6, and the ones after are the 2nd and 3rd elements.

Let's create a new vector called `age` to learn more about indices:

```r
age <- c(15, 22, 45, 52, 73, 81)

age
```

If we look at this vector now, it will show that the first element in `age` is 15, and so on.

![vector indices](../img/vector-index.png)

The **index represents the element number within a vector** (or the compartment number, if you think of the bucket analogy). R indices start at 1.

If we want to extract one or several values from a vector, we can use this index notation along with the name of the vector. Suppose we only wanted the fifth value of this vector, we would say:

```r
age[5]
```

Note that there cannot be a space between the vector name and the open bracket.

We can even use this syntax to select more than one element. Say we were interested in extracting the 3rd, 5th and 6th elements from the vector `age`. Our intuition would be to list multiple values within the brackets, but this won't work:

```r
age[3,5,6]
```

`"Error in age[3, 5, 6] : incorrect number of dimensions"` 

It will give us an error message saying that we have listed the incorrect numebr of dimensions. 

This is because a vector is one-dimensional so R can only take one number or one *"thing"* as input within the brackets. 
This *"thing"* can be a vector of values, essentially the indices we are interested in, or a function that outputs a vector of values.

Let's first create a vector called `idx` that had the 3 indices we are interested in:
```r
idx <- c(3,5,6) # create vector of the elements of interest
```

To subset these out of the `age` vector we can now place that idx object inside the brackets
```
age[idx]
```

Voila! we have now successfully extracted the 3rd, 5th and 6th elements from `age`

We could have also done this with a single line of code, where the combine function that creates the vector with 3 values is within the brackets:

```r
age[c(3,5,6)]
```

This is called ***nesting***, i.e. we have nested a function within another syntactical component of R.

#### Subsetting with indices and sequence

In R, if you want to create a continuous sequence of numbers you can do so using the `:`. Say we wanted a vector with all the numbers from 6 to 23, we could say 6:23.

```r
6:23
```

We could also get them in reverse order with 23:6

```r
23:6
```

This is a handy functionality that can be used together with the index notation. For example, if we want to extract the first 4 elements from the `age` vector, we can say:

```r
age[1:4]
```

In addition to these using minus within the brackets works like you might expect; if we wanted all values except the fifth value, we could use -5 within the brackets instead of writing out the ones we want:

```r
age[-5]
```

## Conclusion
