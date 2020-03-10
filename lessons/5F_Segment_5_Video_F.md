## Introduction

### Lists

Selecting components from a list requires a slightly different notation, even though in theory a list is a vector (that contains multiple data structures). To select a specific component of a list, you need to use double bracket notation `[[]]`. Let's use the `list1` that we created previously, and index the second component:

```r
list1[[2]]
```

What do you see printed to the console? Using the double bracket notation is useful for **accessing the individual components whilst preserving the original data structure.** When creating this list we know we had originally stored a dataframe in the second component. With the `class` function we can check if that is what we retrieve:

```r
comp2 <- list1[[2]]
class(comp2)
```

You can also reference what is inside the component by adding an additional bracket. For example, in the first component we have a vector stored. 

```r
list1[[1]]
	
[1] "ecoli" "human" "corn" 
```

Now, if we wanted to reference the first element of that vector we would use:

```r
list1[[1]][1]

[1] "ecoli"
```

You can also do the same for dataframes and matrices, although with larger datasets it is not advisable. Instead, it is better to save the contents of a list component to a variable (as we did above) and further manipulate it. Also, it is important to note that when selecting components we can only **access one at a time**. To access multiple components of a list, see the note below. 

> **NOTE:** Using the single bracket notation also works wth lists. The difference is the class of the information that is retrieved. Using single bracket notation i.e. `list1[1]` will return the contents in a list form and *not the original data structure*. The benefit of this notation is that it allows indexing by vectors so you can access multiple components of the list at once.


***

**Exercises**  

Let's practice inspecting lists. Create a list named `random` with the following components: `metadata`, `age`, `list1`, `samplegroup`, and `number`.

1. Print out the values stored in the `samplegroup` component.
	
2. From the `metadata` component of the list, extract the `celltype` column. From the celltype values select only the last 5 values.
	
***

Assigning names to the components in a list can help identify what each list component contains, as well as, facilitating the extraction of values from list components. 

Adding names to components of a list uses the same function as adding names to the columns of a dataframe, `names()`.
	
Let's check and see if the `list1` has names for the components:

```r
names(list1) 
```

When we created the list we had combined the `species` vector with  a dataframe `df` and the `number` variable. Let's assign the original names to the components:

```r
names(list1) <- c("species", "df", "number")
	
names(list1)
```

Now that we have named our list components, we can extract components using the `$` similar to extracting columns from a dataframe. To obtain a component of a list using the component name, use `list_name$component_name`:

To extract the `df` dataframe from the `list1` list:

```r
list1$df
```

Now we have three ways that we could extract a component from a list. Let's extract the `species` vector from `list1`:

```r
list1[[1]]
list1[["species"]]
list1$species
```

***

**Exercise**

Let's practice combining ways to extract data from the data structures we have covered so far:

1. Set names for the `random` list you created in the last exercise.
2. Extract the third component of the `age` vector from the `random` list.
3. Extract the genotype information from the `metadata` dataframe from the `random` list.

***

