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


The logical vector returned denotes which elements in `A` are also in `B` and which are not.  

We saw previously that we could use the output from a logical expression to subset data by returning only the values corresponding to `TRUE`. Therefore, we can use the output logical vector to subset our data, and return only those elements in `A`, which are also in `B` by returning only the TRUE values:

![matching1](../img/in-operator1.png)

```r
intersection <- A %in% B
intersection
```

![matching2](../img/in-operator2.png)

```r
A[intersection]
```

![matching3](../img/in-operator3.png)

In these previous examples, the vectors were small and so it's easy to count by eye; but when we work with large datasets this is not practical. A quick way to assess whether or not we had any matches would be to use the `any` function to see if **any of the values contained in vector A are also in vector B**:

```r
any(A %in% B)
```

The `all` function is also useful. Given a logical vector, it will tell you whether all values returned are `TRUE`. If there is at least one `FALSE` value, the `all` function will return a `FALSE` and you know that all of A are not contained in B.

```r
all(A %in% B)
```
***
[**Exercise 1**](https://github.com/hbctraining/Intro-to-R/blob/master/results/answer_keys/07_matching_answer_key.md)

1. Using the `A` and `B` vectors created above, evaluate each element in `B` to see if there is a match in `A`

2. Subset the `B` vector to only return those values that are also in `A`.

***
Suppose we had **two vectors that had the same values but just not in the same order**. We could also use `all` to test for that. Rather than using the `%in%` operator we would use `==` and compare each element to the same position in the other vector. Unlike the `%in%` operator, **for this to work you must have two vectors that are of equal length**.

```r
A <- c(10,20,30,40,50)
B <- c(50,40,30,20,10)  # same numbers but backwards 

# test to see if each element of A is in B
A %in% B

# test to see if each element of A is in the same position in B
A == B

# use all() to check if they are a perfect match
all(A == B)

```

Often when working with genomic data, we have a data file that corresponds with our metadata file. The data file contains measurements from the biological assay for each individual sample. In this case, the biological assay is gene expression and data was generated using RNA-Seq. 

Let's read in our expression data (RPKM matrix) that we downloaded previously:

```r
rpkm_data <- read.csv("data/counts.rpkm.csv")
```

Take a look at the first few lines of the data matrix to see what's in there.

```r
head(rpkm_data)
```

It looks as if the sample names (header) in our data matrix are similar to the row names of our metadata file, but it's hard to tell since they are not in the same order. We can do a quick check of the number of columns in the count data and the rows in the metadata and at least see if the numbers match up. 

```r
ncol(rpkm_data)
nrow(metadata)
```

What we want to know is, **do we have data for every sample that we have metadata?** 

Let's try this on our data and see whether we have metadata information for all samples in our expression data. We'll start by creating two vectors; one with the `rownames` of the metadata and `colnames` of the RPKM data. These are base functions in R which allow you to extract the row and column names as a vector:

```r
x <- rownames(metadata)
y <- colnames(rpkm_data)
```

Now check to see that all of `x` are in `y`:

```r
all(x %in% y)
```

*Note that we can use nested functions in place of `x` and `y`:*

```r
all(rownames(metadata) %in% colnames(rpkm_data))
```

We know that all samples are present, but are they in the same order:

```r
all(rownames(metadata) == colnames(rpkm_data))
```

**Looks like all of the samples are there, but will need to be reordered. To reorder our genomic samples, we need to first learn different ways to reorder data. Therefore, we will step away from our genomic data briefly to learn about reordering, then return to it at the end of this lesson.**

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
