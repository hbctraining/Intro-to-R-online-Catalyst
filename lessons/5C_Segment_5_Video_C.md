## Introduction

In this segment we will extend on the lesson from segment 5B and talk about additional functionality in R to subset data from one-dimensional objects.

#### Selecting using indices with logical operators

R has a set of logical operators available that can be used to assess data within objects. E.g. if one is interested in extracting all the elements from age that were greater than or equal to a certain value, we can do that fairly easily. 

This is the full list of logical operators available in R. It includes "and" `&` and "or" `\|`, which are used to combine two or more of the operators together.

| Operator | Description |
| :-----------:|:----------------|
| > | greater than |
| >= | greater than or equal to|
| < | less than |
| <= | less than or equal to |
| == | equal to |
| != | not equal to |
| & | and |
| \| |or |


Let's use some of these with the `age` vector to get all the elements that are greater than 50.
	
```r
age

age > 50
```

Instead of returning the 3 elements that are actually greater than 50, we get a vector of TRUE and FALSE values. Let's take a closer look at this output.

* What is the data type of this output? It is logical
* What is the data structure of this output? It is a vector
* How many elements in the logical vector? 6
* Why are there 6 elements in this logical vector? Because the vector `age` has 6 elements

In conclusion, the output of `age > 50` is a logical vector of the same length as `age`. Every FALSE here corresponds to elements that are NOT greater than 50, and every TRUE corresponds to elements that are greater than 50.

```r
[1] FALSE FALSE FALSE  TRUE  TRUE  TRUE
```

Great, we can now use logical operators and understand the output. But we still need to extract the elements that are greater than 50 from the `age` vector. So how do we do this?

In addition to being able to place a vector of numeric values within the brackets to extract specific elements, we can also place a vector of logical values of the same length as the object being subsetted, within the brackets. Let's say we want to extract the values in the `age` vector that are either greater than 50 **or** less than 18.

We could write out the logical expression as follows with age greater than 50 separated from age less than 18 by a "pipe" which denotes "or" and save the logical vector output to a new object:

```r
logi_idx <- age > 50 | age < 18

logi_idx 
```
Then we can use this object to subset from the age vector

```r
age[logi_idx]
```

You could have also used nesting to do this with a single line of code

```r
age[age > 50 | age < 18]
```

##### Indexing with logical operators using the `which()` function

While logical expressions will return a vector of TRUE and FALSE  values of the same length, there is a function within base R called `which()` that takes a logical vector as input and returns the numeric index associated with each TRUE value.

```r
which(age > 50 | age < 18)
```

Since the output of which is a numeric vector of indices, it can also be used within the brackets.

```r
age[which(age > 50 | age < 18)]
```

`which()` stands for "which is true" and is useful when dealing with NA values.

## Conclusion

Using logical operators and operations is a commonly used method to subset and wrangle data structures in R, in segment 5D (or 5E) we will be using logical operators to subset data frames. Thanks for your attention. 

---

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*

* *The materials used in this lesson are adapted from work that is Copyright © Data Carpentry (http://datacarpentry.org/). 
All Data Carpentry instructional material is made available under the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0).*
