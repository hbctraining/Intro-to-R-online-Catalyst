## Introduction

Welcome to segment 6B, Reordering and Matching Datasets. Oftentimes, we encounter different analysis tools that require multiple input datasets. It is not uncommon for these inputs to need to have the same row names, column names, or unique identifiers in the same order to perform the analysis. Therefore, knowing how to reorder datasets and determine whether the data matches is an important skill.

In segment 6A, we learned how to determine whether the same data is present in two datasets, in addition to, whether it is in the same order. In this segment, we will explore how to reorder the data such that the datasets are matching.

## Reordering data using indices

Indexing `[ ]` can be used to extract values from a dataset as discussed in segment 5, but we can also use it to rearrange our data values. Let's explore reordering with indices by creating a vector called teaching team that has the values Mary first, Meeta second, and Radhika third.

```r
teaching_team <- c("Mary", "Meeta", "Radhika")
```
![reordering](../img/teachin-team.png)

Remember that we can return values in a vector by specifying it's position or index. So, if wanted to return Meeta and Radhika, I could do so by typing teaching team, square brackets, and inside the combine function giving the indices for Meeta and Radhika. Meeta is in the second position, so the index is 2 while Radhika is in the third position, so the index is 3.

```r
teaching_team[c(2, 3)] # Extracting values from a vector
```

Note that we return Meeta and Radhika; however, if we look at the teaching team variable it hasn't changed. If we wanted to save or store the output, then we would need to reassign the output to teaching team or assign it to a different variable.

```r
teaching_team
```

We can also extract the values and reorder them. The order of the indices is the order in which the values are returned. So, if we extract Meeta and Radhika, but would like Radhika to be output first, then Meeta, we can give Radhika's index first, which is 3, then Meeta's, which is 2.

```r
teaching_team[c(3, 2)] # Extracting values and reordering them
```

Now we see in the output Radhika then Meeta.

Similarly, we can extract all of the values and reorder them. Let's say we would like Radhika to be output first, followed by Mary and Meeta. We could type teaching team, square brackets, then inside the combine function, 3, comma, 1, comma, 2.

```r
teaching_team[c(3, 1, 2)]
```

Let's save our results by assigning to a variable, we'll call it reorder teach:

```r
reorder_teach <- teaching_team[c(3, 1, 2)] # Saving the results to a variable
```

Now we can see our reordered teaching team vector is saved as this new variable.

```r
reorder_teach
```

## The `match` function

Now that we know how to reorder using indices, let's try to use it to reorder the contents of one vector to match the contents of another. Let's create vectors `first` and `second`.

```r
first <- c("A","B","C","D","E")
second <- c("B","D","E","A","C")  # same letters but different order
```
![matching4](../img/match1.png)

***How would you reorder `second` vector to match `first` using indices?***

We can start by giving the name of the vector to reorder, second, then square brackets. Inside the square brackets we can add the combine function to put the indices in the order we would like the values of second output. Since A comes first in the first vector, we need to give the index for A in the second vector as the first value, which is 4, since A is in the fourth position. Then we want B, which is 1, followed by C, which is 5, then D and E give 2 and 3.

```r
second[c(4, 1, 5, 2, 3)]
```

When we run this, we can see the output is the letters ordered in the same order as the first vector. If we had large datasets, it would be difficult to reorder them by searching for the indices of the matching elements, and it would be quite easy to make a typo or mistake. To help with matching datasets, there is a function called match(). 

We can use the `match()` function to match the values in two vectors. We'll be using it to evaluate which values are present in both vectors, then reorder the elements to make the values match. 

`match()` takes 2 arguments. The first argument is a vector of values in the order you want, while the second argument is the vector of values to be reordered such that it will match the first. 

1. a vector of values in the order you want
2. a vector of values to be reordered

The function returns the position of the matches (indices) with respect to the second vector, which can be used to re-order it so that it matches the order in the first vector.  

Let's use match() on the first and second vectors we created. We can type match, then inside the parentheses, we give the vector of values in the order we want, which is first, then the vector of values to be reordered, which is second.
	
```r
match(first, second)
[1] 4 1 5 2 3
```

The output is the indices for how to reorder the second vector to match the first. These indices match the indices that we derived manually before. 

The function should return a vector of size `length(first)`. Each number that is returned represents the index of the `second` vector where the matching value was observed. 

Now, we can just use the indices to reorder the `second` vector to be in the same positions as the matching elements in the `first` vector. Let's save the indices to a variable we'll call reorder idx. 

```r
reorder_idx <- match(first,second) # Saving indices for how to reorder `second` to match `first`
```

Then, use those indices to reorder the second vector by typing second, square brackets, reorder idx, similar to how we ordered with the manually derived indices.

```r
second[reorder_idx]  # Reordering the second vector to match the order of the first vector
```

Let's save this output to a variable called second reordered.

```r
second_reordered <- second[reorder_idx]  # Reordering and saving the output to a variable
```

![matching7](../img/match3-reordered.png)


Now that we know how `match()` works, let's change vector `second` so that only a subset are retained. 

```r	
first <- c("A","B","C","D","E")
second <- c("D","B","A")  # remove values
```

![matching5](../img/match2.png)

We are missing C and E in second. Let's explore how match() deals with the missing values.

```r
match(first, second)

[1]  3  2 NA  1 NA
```

We see that the match() function takes every element in the first vector and finds the position of that element in the second vector, and if that element is not present, will return a missing value of NA. The value NA represents missing data for any data type within R. In this case, we can see that the match function output represents the value at position 3 as first, which is A, then position 2 is next, which is B, the value coming next is supposed to be C, but it is not present in the second vector, so NA is returned, so on and so forth. 

If we rearrange second using these indices, then we should see that all the values present in both vectors are in the same positions and NAs are present for any missing values.

```r
second[match(first, second)]
```

### Reordering genomic data using `match()` function

Using the `match` function, we now would like to match the row names of our metadata to the column names of our expression data*, so these will be the arguments for `match`. Using these two arguments we will retrieve a vector of match indices. The resulting vector represents the re-ordering of the column names in our data matrix to be identical to the rows in metadata:
 
 ```r
rownames(metadata)
	
colnames(rpkm_data)
	
genomic_idx <- match(rownames(metadata), colnames(rpkm_data))
genomic_idx
```

Now we can create a new data matrix in which columns are re-ordered based on the match indices:

```r
rpkm_ordered  <- rpkm_data[,genomic_idx]
```

Check and see what happened by using `head`. You can also verify that column names of this new data matrix matches the metadata row names by using the `all` function:

```r
head(rpkm_ordered)
all(rownames(metadata) == colnames(rpkm_ordered))
```

Now that our samples are ordered the same in our metadata and counts data, **if these were raw counts** we could proceed to perform differential expression analysis with this dataset.


---
*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*
