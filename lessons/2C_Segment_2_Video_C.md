## Introduction

Welcome to segment 2C, Data Structures for Higher Dimensional Data (2D and beyond). In segment 2B, we got comfortable with the idea of using vectors and factors as variables for storing one-dimensional data, and we discussed how they can be used as building blocks for creating other, higher dimensional, data structures in R. In this lesson, we will explore the data structures for two-dimensional data, including matrices and data frames. In addition to the two-dimensional data structures, we will introduce a data structure called a list.

## Matrix

The first two-dimensional data structure we will introduce is the matrix. A `matrix` in R is essentially a vector divided into a certain number of rows and columns. 

![matrix](../img/matrix.png)

For instance, we could create a matrix using the `matrix()` function, and have a vector of values from number 1 to 6 be divided between 2 rows and 3 columns.

```r
# Create a vector to be turned into a matrix
top_num <- c(1,2,3,4,5,6)

# Turn vector into matrix
mx <- matrix(top_num, nrow = 2, ncol = 3)
mx
```

Once the matrix is created, each row and each column could be thought of as a vector of values. However, in a matrix, all of the columns and rows have the same data type. 

Matrices are used commonly as part of the mathematical machinery of statistics. They are usually of numeric or integer data type and used in computational algorithms to serve as a checkpoint. For example, if input data is not of identical data type (numeric, character, etc.), the `matrix()` function will throw an error and stop any downstream code execution.

While matrices are usually numeric, they can also be created using any of the other data types. You can have matrices with all character or all logical values, as well.

### Data Frame

The next two-dimensional data structure we will explore is the data frame. A `data.frame` is the _de facto_ data structure for most tabular data and what we use for statistics and plotting. A `data.frame` is similar to a matrix in that it's a collection of vectors of the **same length** and each vector represents a column. However, in a dataframe **each vector can be of a different data type** (e.g., characters, integers, factors). 

![dataframe](../img/dataframe.png)

A data frame is the most common way of storing data in R, and if used systematically makes data analysis easier. 

We can create a dataframe by bringing **vectors** together to **form the columns**. We do this using the `data.frame()` function, and giving the function the different vectors we would like to bind together. *This function will only work for vectors of the same length.*

Let's create a data frame called `df`. We can do this by typing `data.frame`, parentheses, and inside the parentheses adding the names of the vectors that we would like to turn into columns, in the order we would like them to appear. So we will type `species`, comma, `glengths`. Then we can use the assignment operator to create a variable called `df`. 

```r
df <- data.frame(species, glengths)
```

We can see that a new variable called `df` has been created in our environment within a new section called `Data`. In the environment, it specifies that `df` has 3 observations of 2 variables. What does that mean? In R, rows always come first, so it means that `df` has 3 rows and 2 columns. We can get additional information if we click on the blue circle with the white triangle in the middle next to `df`. It will display information about each of the columns in the data frame, giving information about what the data type is of each of the columns and the first few values of those columns.

Note that the species column is now a factor even though we added it as a character vector. It turns out that the `data.frame()` function will turn all **character vectors into factors** by default. There are ways that we can change the default behavior of the function as we will see in Segment 3A, but we will leave it as is for now. 

Another handy feature in RStudio is that if we hover the cursor over the variable name, `df`, it will turn into a pointing finger. If you click on `df`, it will open the data frame as it's own tab next to the script editor. We can explore the table interactively within this window. To close, just click on the X on the tab.

As with any variable, we can print the values stored inside to the console if we type it's name and run.

Type and run `df`.

```r
df
```

### Lists

Lists are a data structure in R that can be perhaps a bit daunting at first, but soon become amazingly useful. A list is a data structure that can hold any number of any types of other data structures.

![list](../img/list.png)


If you have variables of different data structures you wish to combine, you can put all of those into one list object by using the `list()` function and placing all the items you wish to combine within parentheses:

```r
list1 <- list(species, df, number)
```
Print out the list to screen to take a look at the components:

```r
list1
	
[[1]]
[1] "ecoli" "human" "corn" 

[[2]]
  species glengths
1   ecoli      4.6
2   human   3000.0
3    corn  50000.0

[[3]]
[1] 5

```

There are three components corresponding to the three different variables we passed in, and what you see is that structure of each is retained. Each component of a list is referenced based on the number position. We will talk more about how to inspect and manipulate components of lists in later lessons.

***
**Exercise**

Create a list called `list2` containing `species`, `glengths`, and `number`.

---

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*

* *The materials used in this lesson are adapted from work that is Copyright © Data Carpentry (http://datacarpentry.org/). 
All Data Carpentry instructional material is made available under the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0).*


