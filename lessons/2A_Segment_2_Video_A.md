## Introduction

Welcome to segment 2A, Introduction to R Variables. In this lesson we will explore what types of values are available in R and how to assign specific values to variables.

## Data Types

Different types of values can be specified within R. The six basic **data types** that R uses include: numeric, character,  integer, and logical, as shown in this table. The first data type shown is the `numeric` data type, which is for any numerical values, including whole numbers and decimals. This is the most common data type for performing mathematical operations. The next data type we'll discuss is `character`, which is for text values. The `character` data type can be specified by putting quotation marks ("") around the value. For instance, while 5 is a numeric value, if you were to put quotation marks around it, it would turn into a character value, and you could no longer use it for mathematical operations. Single or double quotes both work, as long as the same type is used at the beginning and end of the character value. The next data type is the `integer`, which is for whole numbers. It behaves very similarly to the `numeric` data type for most tasks or functions; however, it takes up less storage space than numeric data, so often tools will output integers if the data is known to be comprised of whole numbers. Just know that integers behave similarly to numeric values. If you wanted to create your own, you could do so by providing the whole number, followed by an upper-case L. The last data type we will discuss in much detail is the `logical` data type. This data type is for `TRUE` and `FALSE` values, and represents the Boolean data type. The `logical` data type can be specified using four values, `TRUE` in all capital letters, `FALSE` in all capital letters, a single capital `T` or a single capital `F`. There are two additional basic data types in R; the `complex` data type is for complex numbers with real and imaginary parts, but most of us do not need to use this data type unless we work with complex numbers. The last data type is `raw`, but we aren't going to go into details on this data type.

The table below provides examples of each of the commonly used data types:

| Data Type  | Examples|
| -----------:|:-------------------------------:|
| Numeric:  | 1, 1.5, 20.33333333|
| Character:  | “anytext”, “5”, “TRUE”|
| Integer:  | 2L, 500L, -17L|
| Logical:  | TRUE, FALSE, T, F|

The type of data will determine what you can do with it. For example, if you want to perform mathematical operations, then your data type cannot be character or logical. Whereas if you want to search for a word or pattern in your data, then you data should be of the character data type. The task or function being performed on the data will determine what type of data can be used.

## Assignment operator

Now that we know what type of values are available to use in R, let's explore how we can use them. To do useful and interesting things in R, we need to assign _values_ to _variables_ using the assignment operator, which is denoted by a 'less than sign', followed by a dash or minus sign.  For example, we can use the assignment operator to assign the numeric value `3` to `x` by typing x, assignment operator, then 3. The assignment operator (`<-`) assigns **values on the right** to **variables on the left**. After we finishing typing, we need to run the code. Remember, the shortcut to run a line of code is pressing the ‘command’ or ‘control’ key at the same time as the ‘enter’ key. 

```r
# Assign the value 3 to a variable named x
x <- 3
```

You should see that your environment is no longer empty. We have a variable, x, that contains the value 3. There is another shortcut to create the assignment operator, or arrow. If you type 'Alt' and minus at the same time, it will create the arrow in a single keystroke.


## Variables

So we have created the variable xA variable is a symbolic name for (or reference to) information. Variables in computer programming are analogous to "buckets", where information can be maintained and referenced. On the outside of the bucket is a name. When referring to the bucket, we use the name of the bucket, not the data stored in the bucket.

In the example above, we created a variable or a 'bucket' called `x`. Inside we put a value, `3`. 

Let's create another variable called `y` and give it a value of 5. 

```r
y <- 5
```
Note that you can create the assignment operator, or arrow, with a shortcut by pushing the `Alt`  and minus keys at the same time.

When assigning a value to an variable, R does not print anything to the console. You can force to print the value by using parentheses or by typing the variable name.

```
y
```

You can also view information on the variable by looking in your `Environment` window in the upper right-hand corner of the RStudio interface.

![Viewing your environment](../img/environment.png)

Now we can reference these buckets by name to perform mathematical operations on the values contained within. What do you get in the console for the following operation: 

```r
x + y
```

Try assigning the results of this operation to another variable called `number`. 

```r
number <- x + y
```

***
**Exercises**

1. Try changing the value of the variable `x` to 5. What happens to `number`?
2. Now try changing the value of variable `y` to contain the value 10. What do you need to do, to update the variable `number`?

***

### Tips on variable names
Variables can be given almost any name, such as `x`, `current_temperature`, or
`subject_id`. However, there are some rules / suggestions you should keep in mind:

- Make your names explicit and not too long.
- Avoid names starting with a number (`2x` is not valid but `x2` is)
- Avoid names of fundamental functions in R (e.g., `if`, `else`, `for`, see [here](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Reserved.html) for a complete list). In general, even if it's allowed, it's best to not use other function names (e.g., `c`, `T`, `mean`, `data`) as variable names. When in doubt
check the help to see if the name is already in use. 
- Avoid dots (`.`) within a variable name as in `my.dataset`. There are many functions
in R with dots in their names for historical reasons, but because dots have a
special meaning in R (for methods) and other programming languages, it's best to
avoid them. 
- Use nouns for object names and verbs for function names
- Keep in mind that **R is case sensitive** (e.g., `genome_length` is different from `Genome_length`)
- Be consistent with the styling of your code (where you put spaces, how you name variable, etc.). In R, two popular style guides are [Hadley Wickham's style guide](http://adv-r.had.co.nz/Style.html) and [Google's](http://web.stanford.edu/class/cs109l/unrestricted/resources/google-style.html).




