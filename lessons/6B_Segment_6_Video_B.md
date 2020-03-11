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

While the input to the match() function is always going to be to vectors, often we need to use these vectors to reorder the rows or columns of a data frame to match the rows or columns of another dataframe. Let's explore how to do this with a common use case for RNA-seq data. To perform differential gene expression analysis, we have a data frame with the expression data or counts for every sample and another data frame with the information about to which condition each sample belongs. For the tools doing the analysis, the samples in the counts data, which are the column names, need to be the same and in the same order as the samples in the metadata data frame, which are the rownames.

We can take a look at these samples in each dataset by using the rownames() and colnames() functions.

 ```r
rownames(metadata)
	
colnames(rpkm_data)
```

We see the row names of the metadata are in a nice order starting at sample1 and ending at sample12, while the column names of the counts data look to be the same samples, but are randomly ordered. Therefore, we will reorder the columns of the counts data to match the order of the row names of the metadata.

To do so, we will use the `match` function to match the row names of our metadata with the column names of our counts data, so these will be the arguments for `match`. Within the match function, the rownames of the metadata is the vector in the order that we want, so this will be the first argument, while the colnames of the count or rpkm data is the vector to be reordered. We will save these indices for how to reorder the colnames of the count data such that it matches the rownames of the metadatato a variable called genomic idx.

```r
genomic_idx <- match(rownames(metadata), colnames(rpkm_data))
genomic_idx
```

The resulting vector represents how to re-order the column names in our counts data to be identical to the row names in metadata. Now we can create a new counts data frame in which the columns are re-ordered based on the match indices. Remember to reorder the rows or columns in a data frame we give the name of the data frame followed by square brackets, and then the indices for how to reorder the rows or columns. 

Our genomic idx represents how we would need to reorder the columns of our count data such that the column names would be in the same order as the row names of our metadata. Therefore, we need to add our genomic idx to the columns position. We are going to save the output of the reordering to a new data frame called rpkm ordered.

```r
rpkm_ordered  <- rpkm_data[, genomic_idx]
```

Let's take a quick check of the new data frame using View(). 

```r
View(rpkm_ordered)
```

We can see that it appears that the sample names are now in a nice order from Sample1 to 12, just like the metadata. One thing to note is that you would never want to rearrange just the column names without the rest of the column because that would dissociate the sample name from it's values.

You can also verify that column names of this new data frame matches the metadata row names by using the `all` function that we learned about in segment 6A:

```r
all(rownames(metadata) == colnames(rpkm_ordered))
```

We get TRUE, meaning that all of the elements in the row names of the metadata are the same and in the same order as the column names in the count data.

Now that our samples are ordered the same in our metadata and counts data, **if these were raw counts** we could proceed to perform differential expression analysis with this dataset.

## Conclusion

Understanding how to reorder and match datasets can be necessary for many different types of analyses and is a useful skill for even basic data wrangling.

To summarize, in this lesson, we explored the how to reorder data using indices and how to match data using the match() function. 


---
*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*
