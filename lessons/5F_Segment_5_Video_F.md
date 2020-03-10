## Introduction

Welcome to segment 5F, Extracting Data from Lists. In segments 5C and 5D, we explored how to select and extract data from one- and two-dimensional data structures. In this segment, we will explore how to extract the components from a list data structure.

## Extracting components from lists using indices

Selecting components from a list requires a slightly different notation than one- or two-dimensional data structures, even though in theory a list is a vector (that contains multiple data structures). To extract a specific component of a list, you need to use double bracket notation `[[]]`. Let's use the `list1` that we created in segment 2C and extract the second component. 

To get started, let's take a quick look at list1 by printing it to the console:

```r
list1
```

We see that it has three components. The first component is a vector, the second component is a data frame, and the third component is a single value. 

To extract the second component, we type the name of the variable we would like to extract from; in this case, it's list1. Then, we add the double square brackets, and inside we give the index for the component we would like to extract

```r
list1[[2]]
```

What do you see printed to the console? Using the double bracket notation is useful for **accessing the individual components while preserving the original data structure.** When creating this list we know we had originally stored a dataframe in the second component. We can extract the second component and save to a variable that we are going to call comp2. Then we can see the data structure of the component by using the `class` function:

```r
comp2 <- list1[[2]]

class(comp2)
```

You can also extract from inside the component by subsetting that data structure as you normally would. For example, in the first component we have a vector stored. 

```r
list1[[1]]
	
[1] "ecoli" "human" "corn" 
```

Since list1[[1]] is a vector, we can extract values from it as we would any vector. So, if we wanted to extract the first element of that vector we would add a single bracket one after the vector to extract the first element:

```r
list1[[1]][1]

[1] "ecoli"
```

You can also do the same for dataframes and matrices, although with these larger datasets it is not advisable. Instead, it is better to save the contents of a list component to a variable and further manipulate it. Also, it is important to note that when selecting components we can only **access one at a time**.

We just wanted to not that using the single bracket notation also works wth lists. The difference is the class of the information that is retrieved. Using single bracket notation i.e. `list1[1]` will return the contents in a list form and *not the original data structure*. The benefit of this notation is that it allows indexing by vectors so you can access multiple components of the list at once.

## Extracting components from lists using component names

Assigning names to the components in a list can help identify what each list component contains, as well as, facilitate the extraction of values from list components. 

Checking or adding names to the components of a list uses the function `names()`. Let's check and see if `list1` has names for the components:

```r
names(list1) 
```

Currently there are no names associated with the components. When we created the list in segment 2C we had combined the `species` vector with  a dataframe `df` and the `number` variable. Let's assign the original names to the components. To do this we can use the assignment operator in a new context. If we add names(list1) to the left side of the arrow to be assigned to, then anything on the right side of the arrow will be assigned. Since we have three components in list1, we need three names to assign. We can create a vector of names using the combine function, and inside the combine function we give the names to assign to the components in the order we would like. So the first name is assigned to the first component of the list.

```r
names(list1) <- c("species", "df", "number")
```

Now, we can check the names and we should see that our components now have names.

```r
names(list1)
```

We can print out list1, and instead of the double brackets, we now see the names. The dollar sign preceeding the names hints at a new way to extract the components of a list. We can extract components using the `$` similar to extracting columns from a dataframe. For example, to extract the `df` dataframe from the `list1` list, we would type list1, dollar sign, df:

```r
list1$df
```

Now we have multiple ways that we could extract a component from a list. Let's extract the `species` vector from `list1`:

```r
list1[[1]]
list1[["species"]]
list1$species
```

## Conclusion

To summarize, in this lesson, we explored how to extract components from the list data structure using either the index of the component or it's name.
