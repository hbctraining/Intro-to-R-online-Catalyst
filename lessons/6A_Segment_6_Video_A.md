---
title: "Advanced R, matching and reordering shortened"
authors: Meeta Mistry, Mary Piper
date: "Friday, September 8, 2017"
---
Approximate time: 110 min


## Introduction

Welcome to segment 6A, “Finding overlap between vectors using the %in% operator. When working in R we are often dealing with vectors, whether it be individual vector variables, or as part of a dataframe. A common question that we encounter is then how can we compare one vector to another? In this segment, we introduce to you the %in% operator and show you how to evaluate overlapping content between two vectors. In addition, we will demonstrate how to check that the order of two vectors are the same. Finally, we apply these operations to a dataset to demonstrate a practical use case.

##  The `%in%` operator

To compare the values contained in one vector to another, we use the %in% operator in R. Although lacking in [documentation](http://dr-k-lo.blogspot.com/2013/11/) this operator is well-used and very convenient once you get the hang of it. The operator is used with the following syntax: 

SLIDE
```r
vector1_of_values %in% vector2_of_values
```

It will take a vector as input to the left and will **evaluate each element to see if there is a matching value in the vector that follows on the right of the operator.** This operation will return a logical vector of the same length as vector1, presenting a TRUE if the element value exists in vector2 and a FALSE if it does not.


RSTUDIO:

Let's go through an example to demonstrate how it works. We will create two vectors A and B. A will contain a set of 6 odd numbers and B will contain a set of 6 even numbers. *Note that the two vectors do not have to be the same length.*

```r
A <- c(1,3,5,7,9,11)   # odd numbers
B <- c(2,4,6,8,10,12)  # even numbers
```

To test and see if each of the elements in A is also in B we can type A %in% B:

```r
# test to see if each of the elements of A is in B	
A %in% B
```

The result is a logical vector of 6 FALSE values.Since vector A contains only odd numbers and vector B contains only even numbers, there is no overlap and so the vector returned contains a `FALSE` for each element. 

```r
## [1] FALSE FALSE FALSE FALSE FALSE FALSE
```

Let's change a couple of numbers inside vector B. Run the two lines of code so that we have a new vector B.


```r
A <- c(1,3,5,7,9,11)   # odd numbers
B <- c(2,4,6,8,1,5)  # add some odd numbers in 
```


To test and see which elements of vector A overlap with vector B we use the in operator:

```r
# test to see if each of the elements of A is in B
A %in% B
```

This time we get a different sequence of logical values.

```r
## [1]  TRUE FALSE  TRUE FALSE FALSE FALSE
```
SLIDE:

![matching1](../img/in-operator1.png)

In the first element of the logical vector we observe a TRUE value. This is because in the first element of vector A, we have the number one which also exists in vector B. It doesn't matter that the number one is in position 5 of vector B, it just matters that it exist somewhere in the vector B. The next value is FALSE because the number three does not exist in vector B. We then observe another TRUE vaue, corresponding to the number five which also exists in vector B. And the remainder of FALSE values indicate that none of the other values overlap with vector B. The logical vector that was returned is relative to the first vector used as input to the %in% operator - which is vector A.

In segment 5C, we demonstrated the use of output from a logical expression to subset data and return only the values corresponding to `TRUE`. In the same way, we can use the logical vector output from the %in% operator to subset the original vector A to keep only values that overlap with vector B.

RSTUDIO:

We can assign the output from the in operation to a variable called intersection.
```r
intersection <- A %in% B
intersection
```

Then we can use the square brackets to subset vector A using the interesection variable. Note how only the values 1 and 5 are returned.

```r
A[intersection]
```

***
[**Exercise 1**](https://github.com/hbctraining/Intro-to-R/blob/master/results/answer_keys/07_matching_answer_key.md)

1. Using the `A` and `B` vectors created above, evaluate each element in `B` to see if there is a match in `A`

2. Subset the `B` vector to only return those values that are also in `A`.

***

In our examples, the vectors A and B that we created were small and so it would be easy to evaluate the overlap by scanning the logicl values returned. However,  when we are working with large datasets this is not practical. We will introduce you to two new functions in R that are helpful when working logical vectors in R.

The first is the `any` function. This function will take as input a logical vector of any length and will return a single logical value to evaluate if any of the values are TRUE. Therefore , if a TRUE values is returned - this means that there is at least one TRUE value in the logical vector and a FALSE value indicates that there are none.

If we tried this with the logical vector output from the in operation A %in% B, we would get a TRUE value. This tells us that there is atleast one matching value between the two vectors.

```r
any(A %in% B)
```

The `all` function is also useful. Given a logical vector, it will tell you whether all values are `TRUE`. If there is at least one `FALSE` value, the `all` function will return a `FALSE`. If we tried this with the logical vector output from the in operation A %in% B, we would get a FALSE value, letting us know that all elements of A are not contained in B.

```r
all(A %in% B)
```

The `all` function can also be used with the double equal operator to evaluate the order of two vectors. We can test this out with an example. Let's create two new vectors C and D. They contain the same numbers, but one is just in the reverse order.

```r
C <- c(10,20,30,40,50)
D <- c(50,40,30,20,10)  # same numbers but backwards 
```

First we could check to see if each element of vector C is in vector D.

```r
# test to see if each element of C is in D
C %in% D
```

If we put that inside the all function we could quickly assess whether all values in vector C have a match somewhere in vector D.

```r
# test to see if all values are matching between vectors
all(C %in% D)
```

Great! Now we know that the two vectors contain all of the same values, but are they in the same order? To find out we can use the all function again, but this time using the double equals operator:

```r

# use all() to check if they are in the same order
all(C == D)

```

Note that evaluating order with all is only possible if the two vectors you are comparing are the exact same length.

# Use case

So now we know how to compare two vectors to one another, you might be wondering when would I need to do something like this? Well, one common example is when we are working with genomic data we often have a data file that corresponds with our metadata file. The data file contains measurements from the biological assay for each individual sample, while the metadata file contains information about each sample. For the data we are working with, the biological assay is gene expression and the data we are using was generated using RNA-Seq. 

Let's read in the count matrix that we downloaded previously. This is a csv file located in your data folder in yoru working directory. You can use the read.csv() function to read in the data and save it to a variable called `rpkm_data`.

```r
rpkm_data <- read.csv("data/counts.rpkm.csv")
```

Use the head() function to take a look at the first few lines of the dataframe to see what's in there.

```r
head(rpkm_data)
```

We have columns corresponding to samples and rows representing the different genes that were assayed. At a quick glance, it looks as if the sample names in our data are similar to the row names of our metadata file, but it's hard to tell since they are not in the same order. We can use some the functions we learned in segment 5A do a quick check of the number of columns in the count data and the rows in the metadata and at least see if the numbers match up. 

```r
ncol(rpkm_data)
nrow(metadata)
```
It looks like both files contain 12 samples. Now what we need to find out is, **do we have data for every sample that we have metadata?** 

We can answer this question by using the %in% operator. We need two vectors as input to the operator so we will create variables x and y.  x will be a vector of`rownames` from the metadata and y will be a vector of `colnames` of the RPKM data. In segement 5A, we discussed some base functions in R which allow you to extract the row and column names as a vector:

```r
x <- rownames(metadata)
y <- colnames(rpkm_data)
```

Now to check to see that all of `x` are in `y` we use:

```r
all(x %in% y)
```

We get a TRUE value which tells us that the same 12 samples in our metadata are contained in the data file. Note that we could have use nested functions and skipped the step of creating x and y:

```r
# Alternative 
all(rownames(metadata) %in% colnames(rpkm_data))
```

We know that all samples are present, but are they in the same order? We can use the `all()` function here:

```r
all(rownames(metadata) == colnames(rpkm_data))
```

We get a FALSE value! **Looks like all of the samples are there, but not in the same order.  To reorder our genomic samples, we need to first learn different ways to reorder data and this will be covered in segement 6B.**

***
[**Exercise 2**](https://github.com/hbctraining/Intro-to-R/blob/master/results/answer_keys/07_matching_answer_key.md)

We have a list of IDs for marker genes of particular interest. We want to extract count information associated with each of these genes, without having to scroll through our matrix of count data. We can do this using the `%in%` operator to extract the information for those genes from `rpkm_data`.

1. Create a vector for your important gene IDs, and use the `%in%`operator to determine whether these genes are contained in the row names of our `rpkm_data` dataset.

	```r
	important_genes <- c("ENSMUSG00000083700", "ENSMUSG00000080990", "ENSMUSG00000065619", "ENSMUSG00000047945", "ENSMUSG00000081010", 	"ENSMUSG00000030970")
	```
	
2. Extract the rows containing the important genes from your `rpkm_data` dataset using the `%in%` operator.

3. **Extra Credit:** Using the `important_genes` vector, extract the rows containing the important genes from your `rpkm_data` dataset without using the `%in%` operator.

***
