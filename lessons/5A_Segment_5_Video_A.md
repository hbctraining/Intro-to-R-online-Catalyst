## Introduction

In this segment we will be talking about functions for inspecting data structures. In other segments, we have discussed what functions are, as well as the different data types & data structures available in R; here we will discuss a few functions to enable you to get information from a data structure, including figuring out the exact data structure you may be working with.

## Inspecting data structures

There are a wide selection of base functions in R that are useful for inspecting your data and summarizing it. In this segment we will be utilizing some of the data objects we have created in segments 2B and importing-exporting-data; specifically `metadata`, `glenghts`, `expression`. If you do not have these objects, you can follow the instructions provided below the video. 

Basically, you will need to download [a `.csv` file](https://github.com/hbc/NGS_Data_Analysis_Course/raw/master/sessionII/data/mouse_exp_design.csv) to your working directory and run the following lines of code.

```r
metadata <- read.csv(file="mouse_exp_design.csv")

glengths <- c(4.6, 3000, 50000)

expression <- c("low", "high", "medium", "high", "low", "medium", "high")

expression <- factor(expression)
```

Let's start with the `metadata` object.

Take a look at the object by typing out the variable name `metadata` and pressing return; the variable contains information describing the samples in our study. 

```r
metadata

          genotype celltype replicate
sample1        Wt    typeA		1
sample2        Wt    typeA		2
sample3        Wt    typeA		3
sample4        KO    typeA		1
sample5        KO    typeA		2
sample6        KO    typeA		3
sample7        Wt    typeB		1
sample8        Wt    typeB		2
sample9        Wt    typeB		3
sample10       KO    typeB		1
sample11       KO    typeB		2
sample12       KO    typeB		3

```
Each row holds information for a single sample, and the columns contain categorical information about the sample `genotype`(WT or KO), `celltype` (typeA or typeB), and `replicate number` (1,2, or 3).

What is the data structure of this object? You should be able to tell based on the fact that each column represents distinct sets of information, which is typical of a data frame. How do we check that it is a data frame?

There is a function called `class()` that enables us to do this.

```r
class(metadata)

[1] "data.frame"
```

It is important to note that character values get converted to factors (data type) by default using `data.frame()` or the `read.csv()` functions. One way to assess if that is what happened with the `metadata` object would be to use the `str()` (structure) function. This function provides detailed information about each column:


```r
str(metadata)

'data.frame':	12 obs. of  3 variables:
 $ genotype : Factor w/ 2 levels "KO","Wt": 2 2 2 1 1 1 2 2 2 1 ...
 $ celltype : Factor w/ 2 levels "typeA","typeB": 1 1 1 1 1 1 2 2 2 2 ...
 $ replicate: num  1 2 3 1 2 3 1 2 3 1 ...
```

As you can see, the columns `genotype` and `celltype` are of the `factor` class, whereas the replicate column has been interpreted as integer data type.

__You can also get this information from the "Environment" tab in RStudio.__

For the `metadata` object we were able to just display all the contents of the data frame onto the console easily. Suppose we had a larger file with 100s of rows, we might not want to display all the contents in the console. In that case we can use the `head()` function to just display the first 6 rows/items from any object:

```r
head(metadata)

        genotype celltype replicate
sample1       Wt    typeA         1
sample2       Wt    typeA         2
sample3       Wt    typeA         3
sample4       KO    typeA         1
sample5       KO    typeA         2
sample6       KO    typeA         3
```

We could use the `head()` function on a factor or vector as well:

```r
head(expression)

[1] low    high   medium high   low    medium
Levels: high low medium
```

Similarly the `tail` function will display only the last 6 rows/items from a given object, try it out!


### List of functions for data inspection

In addition to the functions we discussed above, there are many other functions that allow you to get a sense of the content/structure of data. 

Some of these functions will work on **all data structures**, and we have already encountered most of these:
- **`str()`:** compact display of data contents (env.)
- **`class()`:** data type (e.g. character, numeric, etc.) of vectors and data structure of dataframes, matrices, and lists.
- **`summary()`:** detailed display, including descriptive statistics, frequencies
- **`head()`:** will print the beginning entries for the variable
- **`tail()`:** will print the end entries for the variable

Let's see what the `summary()` function returns for a vector and a data frame:

```r
summary(glengths)

   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    4.6  1502.3  3000.0 17668.2 26500.0 50000.0 


summary(metadata)

 genotype  celltype   replicate
 KO:6     typeA:6   Min.   :1  
 Wt:6     typeB:6   1st Qu.:1  
                    Median :2  
                    Mean   :2  
                    3rd Qu.:3  
                    Max.   :3  
```

As you can see the summary function is very useful not just for numeric/integer values, but also for factors.

Some functions, like `length()` will work on **one dimensional structures only**, i.e. vectors and factors:

```r
length(glengths)

[1] 3
```

And some others will work on **two dimensional structures** like data frames and matrices:

- **`dim()`:** returns dimensions of the dataset as a vector with two values
- **`nrow()`:** returns the number of rows in the dataset as a vector with a single value
- **`ncol()`:** returns the number of columns in the dataset as a vector with a single value
- **`rownames()`:** returns the row names in the dataset as a vector
- **`colnames()`:** returns the column names in the dataset as a vector

Let's try some of these out.

```r
dim(metadata)

[1] 12  3


ncol(metadata)

[1] 3


colnames(metadata)

[1] "genotype"  "celltype"  "replicate"
```

The list above is a non-comprehensive list of functions that can be used to inspect data structures. However, these are some of the more commonly used ones.
