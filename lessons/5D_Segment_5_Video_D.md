## Introduction

Welcome to segment 5D, Wrangling of Complex Data Structures. In segment 5C, we explored how to select and extract data from simple, one-dimensional data structures. In this segment, we will extend on what we learned to select and extract data from more complex data structures such as matrices, data frames and lists. Please see segment 2C for more detailed information about these data structures.

### Dataframes

Data frames (and matrices) have 2 dimensions (rows and columns), so if we want to extract from them specific data, we need to specify the "coordinates" for the data of interest. We use the same square bracket notation as for one-dimensional objects, but rather than providing a single index, there are *two indices required*. Within the square bracket, **row numbers come first, followed by column numbers and the two are separated by a comma**. Let's explore the `metadata` dataframe, with the image showing the first six samples:

![metadata](../img/metadata.png)

Let's say we wanted to extract the wild type value that is present in the first row and the first column. To extract it, just like with vectors, we give the name of the data frame that we want to extract from, followed by the square brackets. Now inside the square brackets we give the coordinates or indices for the rows in which the values are present, followed by a comma, then the coordinates or indices for the columns in which the values are present. So we will type `metadata`, square brackets, then we know the wild type value is in the first row if we count from the top, so we put a one, then a comma. The wild type value is also in the first column, counting from left to right, so we put a one in the columns space too. When we run the line of code, we should return the `Wt` value.

```r
# element from the first row in the first column of the data frame
metadata[1, 1] 
```

![metadata](../img/metadata.png)

Now let's try extracting the one value, which is also in the first row, but the third column. To do this, we would type metadata, square brackets, one in the rows space, for the value being in the first row, then a comma, and a three in the column space, for the value being in the third column. When we run it, we should return the value one.

```r  
# extract element in the first row in the 3rd column
metadata[1, 3]  
```

Now if you only wanted to select based on rows, you would provide the index for the rows and leave the columns index blank. The key here is to include the comma, to let R know that you are accessing a 2-dimensional data structure. So if we wanted to return only the third row, we would type: metadata, square brackets, 3, comma, then we would leave the column space blank to return all columns.

```r
# extract all elements in the 3rd row
metadata[3, ]    
```

What kind of data structure does the output appear to be? We see that it is two-dimensional with row names and column names, so we can surmise that it's a data frame.

If you were selecting specific columns from the data frame - the rows are left blank. For example, to return the entire third column we would type metadata, square brackets, leave the rows space blank, then add a comma, and a three in the columns space.

```r
# extract all elements in the 3rd column
metadata[ , 3]   
```

What kind of data structure does this output appear to be? It looks different from the data frame, and we really just see a series of values output, indicating a vector data structure. This happens be default if just selecting a single column. R will drop to the simplest data structure possible. Since a single column in a data frame is really just a vector, R will output a vector data structure as the simplest data structure. Oftentimes we would like to keep our single column as a data frame. To do this, there is an argument we can add called `drop`, meaning do we want to drop down to the simplest data structure. By default it is true, but we can change it's value to false in order to keep the output as a data frame. For instance if we wanted to keep the 3rd column as a data frame we could type: metadata, square brackets, rows space blank, comma, three, and after the three we could add the argment `drop = FALSE`.

```r
# extract all elements in the 3rd column, but keep as data frame
metadata[ , 3, drop = FALSE]
```

Just like with vectors, you can select multiple rows and columns at a time. Within the square brackets, you need to provide a vector of the desired values. For example, we can extract the first two columns of the metadata data frame. We can type: metadata, square brackets, rows space empty to return all rows, comma, then we can use the colon notation to extract the first two consecutive columns by typing: 1, colon, 2.	

```r
# dataframe containing first two columns
metadata[ , 1:2] 
```

We can also extract non-consecutive rows or columns. For instance, if we wanted to extract the first, third and sixth rows, we could type: metadata, square brackets, and we would create a vector of indices for the rows we would like to extract. Since we want the first, third and sixth, we would type c, for the combine function, and inside the parentheses we would type 1, 3, and 6. To return all of the columns, we leave the column space blank.

```r
# dataframe containing first, third and sixth rows
metadata[c(1,3,6), ] 
```

For larger datasets, it can be tricky to remember the column number that corresponds to a particular variable. A nice feature of R, is that we can also use the row names and column names to specify the rows or columns in which our values of interest are present. 

In some cases, the column number for a variable can change if the script you are using adds or removes columns. It's therefore often better to use column names to refer to a particular variable, and it makes your code easier to read and your intentions clearer.

If we want to return the first three rows of the cell type column, we could type: metadata, square brackets, 1, colon, 3, comma, and then in quotations we would add the name of the column we would like to extract the values from. In this case we would like the cell type column, so we type: quotation marks, celltype. It's important to type the names of the columns in the exact way that they are typed in the data frame; for instance if I had spelled celltype with a capital C, it would not have worked.

```r
# elements of the celltype column corresponding to the first three samples
metadata[1:3 , "celltype"] 
```

We could have used row names for the row values instead of the indices, for instance in the rows position, we could use the combine function and type the row names for the rows: in quotes, Sample1, Sample2, Sample3. This would have been correct, as well, and returned the same values.

```r
# elements of the celltype column corresponding to the first three samples
metadata[c("Sample1", "Sample2", "Sample3") , "celltype"] 
```


You can do operations on a particular column, by selecting it using the `$` sign. In this case, the entire column is a vector. For instance, to extract all the genotypes from our dataset, we can use: 

```r
metadata$genotype 
```
You can use `colnames(metadata)` or `names(metadata)` to remind yourself of the column names. We can then supply index values to select specific values from that vector. For example, if we wanted the genotype information for the first five samples in `metadata`:

```r
colnames(metadata)

metadata$genotype[1:5]
```

The `$` allows you to select a single column by name. To select multiple columns by name, you need to  concatenate a vector of strings that correspond to column names: 

```r
metadata[, c("genotype", "celltype")]
```

```r
          genotype celltype
sample1        Wt    typeA
sample2        Wt    typeA
sample3        Wt    typeA
sample4        KO    typeA
sample5        KO    typeA
sample6        KO    typeA
sample7        Wt    typeB
sample8        Wt    typeB
sample9        Wt    typeB
sample10       KO    typeB
sample11       KO    typeB
sample12       KO    typeB
```

While there is no equivalent `$` syntax to select a row by name, you can select specific rows using the row names. To remember the names of the rows, you can use the `rownames()` function:

```r
rownames(metadata)

metadata[c("sample10", "sample12"),]
```

#### Selecting using indices with logical operators

With dataframes, similar to vectors, we can use logical vectors for specific columns in the dataframe to select only the rows in a dataframe with TRUE values at the same position or index as in the logical vector. We can then use the logical vector to return all of the rows in a dataframe where those values are TRUE.

```r
idx <- metadata$celltype == "typeA"
	
metadata[idx, ]
```

##### Selecting indices with logical operators using the `which()` function
As you might have guessed, we can also use the `which()` function to return the indices for which the logical expression is TRUE. For example, we can find the indices where the `celltype` is `typeA` within the `metadata` dataframe:

```r
idx <- which(metadata$celltype == "typeA")
	
metadata[idx, ]
```

Or we could find the indices for the metadata replicates 2 and 3:

```r
idx <- which(metadata$replicate > 1)
	
metadata[idx, ]
```

Let's save this output to a variable:

```r
sub_meta <- metadata[idx, ]
```

***

**Exercise**  

Subset the `metadata` dataframe to return only the rows of data with a genotype of `KO`.
	
***

> **NOTE:** There are easier methods for subsetting **dataframes** using logical expressions, including the `filter()` and the `subset()` functions. These functions will return the rows of the dataframe for which the logical expression is TRUE, allowing us to subset the data in a single step. We will explore the `filter()` function in more detail in a later lesson.

