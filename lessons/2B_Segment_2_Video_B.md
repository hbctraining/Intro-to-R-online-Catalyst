## Introduction

In this lesson, we will introduce the different formats available for storing data within R. 

So far we have learned that variables are like buckets where information is maintained and referenced, and we use the name on the outside of the bucket to refer to it. In the previous lesson, we only created variables or buckets filled with a single value, but **variables can store more than just a single value, they can store a multitude of values. These values can be stored in different formats or different data structures.** These include, but are not limited to, vectors, factors, matrices, data frames and lists. In this video, we will introduce the one-dimensional data structures, vectors and factors.

## Vectors

A vector is the most common and basic data structure in R, and is pretty much the workhorse of R. It's basically just a collection of values, and those values can be of any data type. For instance, we can see that this is a vector or collection of 4 values: 1, 50, 9, and 42.

![numeric vector](../img/vector2.png)


Vectors can, also, contain character values:

![character vector](../img/vector1.png)

or logical values:

![logical vector](../img/vector5-logical.png)

**Note that all values in a vector must be of the same data type.** If you try to create a vector with values of different data types, R will automatically try to coerce it into a single data type. 

For example, if you were to try to create the following vector, with values A, 9, C, and 52:

![mixed vector](../img/vector3.png)

R will coerce it into all character values:

<img src="../img/vector4.png" width="400">

The analogy for a vector is that your bucket now has different compartments; these compartments in a vector are called *elements*. 

Each **element** represents a single value, and there is no limit to how many elements you can have. A vector is assigned to a single variable, because regardless of how many elements it contains, in the end it is still just a single entity or bucket. 

Let's create a vector using the combine function. We will create a vector of genome lengths and assign it to a variable called `glengths`.

To create `glengths` we can type `glengths`, arrow, then c, for the combine function, followed by open parentheses. Within the parentheses we add the values we would like to combine into a vector separated by commas. So we type: 4.6, comma, 3000, comma, 50000, then close the parentheses.


```r
glengths <- c(4.6, 3000, 50000)
```

Each element of this vector contains a single numeric value, and the three values are combined together into a vector.

When we run this line of code, we should see a new variable or object appear in our Environment. It shows the `glengths` variable is a numeric vector that starts at element 1 and ends at element 3, meaning that `glengths` is comprised of 3 values. In addition, the Environment will show the first few values of any vector.

If we would like to print out the entire contents stored inside any variable, we can just type the name of the variable and run the code. Let's check out what's stored inside `glengths`. 

```r
glengths
```

Within the console you should see the contents printed.

A vector can also contain characters. Let's create another vector called `species` with three elements, where each element corresponds with the genome sizes in the `glengths` vector (in Mb).

To create the `species` vector, we type: `species`, arrow, then inside the `c` or combine function, we will add the values ecoli, human, and corn, separated by commas. Since these are character values, we need to ensure that each element is surrounded by quotation marks. Single or double quotes will work as long as you are consistent with which you use.

```r
species <- c("ecoli", "human", "corn")
```

After running, we should see the new variable pop up in our Environment as a character vector with 3 values. We can print out the contents of the variable by just typing `species`.

```r
species
```

What do you think would happen if we forgot to put quotations around one of the values? Let's test it out with corn:

```r
species <- c("ecoli", "human", corn)
```

Note that RStudio is quite helpful in color-coding the various data types. We can see that our numeric values are blue, the character values are green, and if we forget to surround corn with quotes, it's black. What does this mean? Let's try to run this code.

When we try to run this code we get an error specifying that object 'corn' is not found. What this means is that R is looking for an object or variable in my Environment called 'corn', and when it doesn't find it, it returns an error. If we had a character vector called 'corn' in our Environment, then it would combine the contents of the 'corn' vector with the values `"ecoli"` and `"human"`.

Since we only want to add the value "corn" to our vector, we need to re-run the code with the quotation marks surrounding `corn`. A quick way to add quotes to both ends of a word in RStudio is to highlight the word, then press the quote key.


```r
species <- c("ecoli", "human", "corn")
```

Now that you know how to create vectors, let's practice with a quick exercise. 

### Exercise

Now, let's go through the exercise together. First, we need to create a new vector by combining the values of our `glengths` and `species` vectors. We need to use the combine function denoted with a c, parentheses, and inside the parentheses we add our values. What are the values we should place inside the combine function? Would it be the names `glengths` and `species` surrounded by quotes?

```r
c("glengths", "species")
```

No, this would give us a vector of two values; one value is `glengths` and the other is `species`. This is not what we want. What we want is to combine the **values stored inside** these variables. Remember to access the contents stored inside a variable, we can just type that variable's name. Therefore, inside the combine function, we would want to type glengths and species without any quotation marks surrounding the words.

```r
c(glengths, species)
```

If we run this, then we get the vectors combined output to the console. For the next part of the exercise, we need to assign the output to a new variable called combined. We can do this using the assignment operator, or arrow. We type `combined`, followed by the arrow, then the combine function.

```r
combined <- c(glengths, species)
```
Now for the last part of the exercise, we need to output the contents of `combined` to the console and compare it to the original vectors. To do this, we just type the variable name, combined, and run.

```r
combined
```

Since vectors can only be of a single data type, R will automatically coerce the numeric values to character values. There is no warning or asking if this is what you want done, R will just automatically do it. This is a behavior of R that is important to be aware of as you start to code.

## Factors

The next data structure we'll explore is called a **factor**, which is really just a special type of vector used to **store categorical data**. We discussed in the introductory lessons, how R has powerful abilities for working with categorical data and this specialized data structure is the reason. Within a factor, each unique category is referred to as a **factor level**. Factors are built on top of integer vectors such that each **factor level** or category is assigned an **integer value**, creating value-label pairs. 

For instance, if we have four animals and the first animal is female, the second and third are male, and the fourth is female, we could create a factor that appears like a vector, but has integer values stored under-the-hood. The integer value assigned is a one for females and a two for males. The numbers are assigned in alphabetical order, so because the f- in females comes before the m- in males in the alphabet, females get assigned a one and males a two. In later lessons we will show you how you could change these assignments.

![factors](../img/factors_sm.png)

Let's create a factor and explore a bit more.  We'll start by creating a character vector describing three different levels of expression. 

We will use the combine function to combine together the values low, high, medium, high, low, medium, high into a vector, then assign it to a variable called `expression`. In the environment, we can see `expression` is a character vector of 7 values.

```r
expression <- c("low", "high", "medium", "high", "low", "medium", "high")
```

Let's print all values to the console by typing and running `expression`.

```r
expression
```

Now we can convert this character vector into a *factor* using the `factor()` function. Inside the parentheses we give the vector of values that we would like to turn into a factor. We could assign the output to a new variable; however, we aren't really interested in keeping a character vector called `expression`, so we can just overwrite it be re-assigning the output to `expression`. 

```r
expression <- factor(expression)
```

So, what exactly happened when we applied the `factor()` function? 

![factor_new](../img/factors_new.png)

The expression vector is categorical, in that all the values in the vector belong to a set of categories; in this case, the categories are `low`, `medium`, and `high`. By turning the expression vector into a factor, the **categories are assigned integers alphabetically**, with high equal to one, low equal to two, and medium equal to three. You can view the newly created factor variable in the **Environment** window or by typing and running `expression`. 

```r
expression
```

When you print the contents to the console, the factor levels are also output in order of the integers assigned. So we see high comes first because it recieves a 1, low second, and medium third.

So now that we have an idea of what factors are, when would you ever want to use them? 

Factors are extremely valuable for many operations often performed in R. For instance, factors can give order to values with no intrinsic order. In the previous `expression` vector, if I wanted the low category to be less than the medium category, then we could do this using factors. Also, factors are necessary for many statistical methods. For example, descriptive statistics can be obtained for character vectors if you have the categorical information stored as a factor. Also, if you want to denote which category is your base level for a statistical comparison, then you would need to have your category variable stored as a factor with the base level assigned to 1. Anytime that it is helpful to have the categories thought of as groups in an analysis, the factor function makes this possible. For instance, if you want to color your plots by treatment type, then you would need the treatment variable to be a factor.

Let's practice using factors for categorical data with an exercise.

### Exercise

For the exercise, we need to create a vector with three samples for each of the different sample groups. Remember that we can use the combine function or `c()` to create a vector. Inside the parentheses, we can write three of each of the values, CTL for control, KO for knock-out, and OE for overexpression. Don't forget that these are character values, so we need to surround each value with quotation marks.

```r
samplegroup <- c("CTL", "CTL", "CTL", "KO", "KO", "KO", "OE", "OE", "OE")
```

If we look at `samplegroup` in the Environment, we can see that it's a character vector with 9 values. If we would like to turn it into a factor, we can do so using the factor function and re-assigning to `samplegroup`.

```r
samplegroup <- factor(samplegroup)
```

If we print to console, we can see the level assignments:

```r
samplegroup
```

Which level received a 1? If we look at the levels in the output, we can see that control or CTL comes first, so that category received a one. That makes sense since C- in CTL comes in the alphabet before K- in KO and O- in OE. 

## Conclusion

Hopefully, you are starting to get a bit comfortable with the idea of using vectors and factors as variables for storing your data. Vectors really are the basic building blocks for creating other data structures in R, so understanding what they are and how to create them will be important in understanding later concepts.

To summarize, in this lesson, we explored the **vector** and **factor** data structures available to us in R for one-dimensional data. We learned how to create these data structures, as well as, explored when these data structures are useful. In the next lesson, we will learn about additional data structures for higher dimensional data.  
