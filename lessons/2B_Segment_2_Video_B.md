So far we have learned that variables are like buckets where information is maintained and referenced, and we use the name on the outside of the bucket to refer to it. In the previous lesson, we only created variables or buckets filled with a single value, but **variables can store more than just a single value, they can store a multitude of values. These values can be stored in different formats or different data structures.** These include, but are not limited to, vectors, factors, matrices, data frames and lists. In this video, we will introduce the one-dimensional data structures, vectors and factors.

A vector is the most common and basic data structure in R, and is pretty much the workhorse of R. It's basically just a collection of values, mainly either numbers:

![numeric vector](../img/vector2.png)

We can see that this is a vector or collection of 4 values: 1, 50, 9, and 42.

Vectors can, also, contain character values:

![character vector](../img/vector1.png)

or logical values:

![logical vector](../img/vector5-logical.png)

**Note that all values in a vector must be of the same data type.** If you try to create a vector with more than a single data type, R will automatically try to coerce it into a single data type. 

For example, if you were to try to create the following vector:

![mixed vector](../img/vector3.png)

R will coerce it into all character values:

<img src="../img/vector4.png" width="400">

The analogy for a vector is that your bucket now has different compartments; these compartments in a vector are called *elements*. 

Each **element** represents a single value, and there is no limit to how many elements you can have. A vector is assigned to a single variable, because regardless of how many elements it contains, in the end it is still a single entity (bucket). 

Let's create a vector of genome lengths and assign it to a variable called `glengths`. 

Each element of this vector contains a single numeric value, and the three values are combined together into a vector using the combine function, denoted using a `c` followed by parentheses. All of the values are put within the parentheses and separated with commas.

To create `glengths` we can type `glengths`, arrow, then c, for the combine function, followed by open parentheses. Within the parentheses we add the values we would like to combine into a vector, so we type: 4.6, comma, 3000, comma, 50000, then close the parentheses.

```r
glengths <- c(4.6, 3000, 50000)
```

When we run this line of code, we should see a new variable or object appear in our Environment. It shows the `glengths` variable is a numeric vector that starts at element 1 and ends at element 3, meaning that `glengths` is comprised of 3 values. In addition, the Environment will show the first few values of any vector.

If we would like to print out the entire contents stored inside any variable, we can just type the name of the variable and run the code. Within the console you should see the contents stored inside.

```r
glengths
```

A vector can also contain characters. Let's create another vector called `species` with three elements, where each element corresponds with the genome sizes in the `glengths` vector (in Mb).

To create the `species` vector, we type: `species`, arrow, then inside the `c` or combine function, we will add the values ecoli, human, and corn, separated by commas. Since these are character values, we need to ensure that each element is surrounded by quotation marks. Single or double quotes will work as long as you are consistent with which you use.

```r
species <- c("ecoli", "human", "corn")
```

We should see the new variable pop up in our Environment as a character vector with 3 values. We can print out the contents of the variable by just typing `species`.

```r
species
```

What do you think would happen if we forgot to put quotations around one of the values? Let's test it out with corn:

```r
species <- c("ecoli", "human", corn)
```

Note that RStudio is quite helpful in color-coding the various data types. We can see that our numeric values are blue, the character values are green, and if we forget to surround corn with quotes, it's black. What does this mean? Let's try to run this code.

When we try to run this code we get an error specifying that object 'corn' is not found. What this means is that R is looking for an object in my Environment called 'corn', and when it doesn't find it, it returns an error. If we had a character vector called 'corn' in our Environment, then it would combine the contents of the 'corn' vector with the values `"ecoli"` and `"human"`.

Since we only want to add the value "corn" to our vector, we need to re-run the code with the quotation marks surrounding `corn`. A quick way to add quotes to both ends of a word in RStudio is to highlight the word, then press the quote key.


```r
species <- c("ecoli", "human", "corn")
```

Now that you know how to create vectors, let's practice with a quick exercise. 

Let's go through the exercise. First we need to create a new vector by combining the values of our `glengths` and `species` vectors. We need to use the combine function with a c, parentheses, and inside the parentheses we add our values. What are the values we would place inside the combine functions? Would it be the names glengths and species surrounded by quotes?

```r
c("glengths", "species")
```

No, this would give us a vector of two values; one value is `glengths` and the other is `species`. This is not what I want. What I want is to combine the values stored inside these variables. Remember to access the contents stored inside a variable, we can just type that variable's name. Therefore, inside the combine function, we would want to type glengths and species without any quotation marks surrounding the words.

```r
c(glengths, species)
```

If we run this, then we get the vectors combined output to the console. For the next part of the exercise, we need to assign the output to a new variable called combined. We can do this using the assignment operator, or arrow. We type `combined`, followed by the arrow, then the combine function.

```r
combined <- c(glengths, species)
```
Now for the last part of the exercise, we need to output the contents of `combined` to the console and compare it with the original vectors. To do this, we just type the variable name, combined, and run.

```r
combined
```

Since vectors can only be of a single data type, R will automatically coerce the numeric values to character values. There is no warning or asking if this is what you want done, R will just  automatically do it. This is a behavior of R that is important to be aware of as you start to code.

### Factors

A **factor** is a special type of vector that is used to **store categorical data**. Each unique category is referred to as a **factor level** (i.e. category = level). Factors are built on top of integer vectors such that each **factor level** is assigned an **integer value**, creating value-label pairs. 

![factors](../img/factors_sm.png)

Let's create a factor vector and explore a bit more.  We'll start by creating a character vector describing three different levels of expression:

```r
expression <- c("low", "high", "medium", "high", "low", "medium", "high")
```

Now we can convert this character vector into a *factor* using the `factor()` function:

```r
expression <- factor(expression)
```

So, what exactly happened when we applied the `factor()` function? 

![factor_new](../img/factors_new.png)

The expression vector is categorical, in that all the values in the vector belong to a set of categories; in this case, the categories are `low`, `medium`, and `high`. By turning the expression vector into a factor, the **categories are assigned integers alphabetically**, with high=1, low=2, medium=3. This in effect assigns the different factor levels. You can view the newly created factor variable and the levels in the **Environment** window.

![Factor variables in environment](../img/factors.png)


***
**Exercises**

Let's say that in our experimental analyses, we are working with three different sets of cells: normal, cells knocked out for geneA (a very exciting gene), and cells overexpressing geneA. We have three replicates for each celltype.

1. Create a vector named `samplegroup` using the code below. This vector will contain nine elements: 3 control ("CTL") samples, 3 knock-out ("KO") samples, and 3 over-expressing ("OE") samples:

	```r
	samplegroup <- c("CTL", "CTL", "CTL", "KO", "KO", "KO", "OE", "OE", "OE")
	```

2. Turn `samplegroup` into a factor data structure.

***
