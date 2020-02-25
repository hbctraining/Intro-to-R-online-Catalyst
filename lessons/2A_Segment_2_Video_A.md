## Introduction

Welcome to segment 2A, Introduction to R Variables. In this lesson we will explore what types of values are available in R and how to assign specific values to variables.

## Data Types

Different types of values can be specified within R. The six basic **data types** that R uses include: numeric, character,  integer, and logical, as shown in this table. The first data type shown is the `numeric` data type, which is for any numeric values, including whole numbers and decimals. This is the most common data type for performing mathematical operations. 

The next data type we'll discuss is `character`, which is for text values. The `character` data type can be specified by putting quotation marks ("") around the value. For instance, while 5 is a numeric value, if you were to put quotation marks around it, it would turn into a character value, and you could no longer use it for mathematical operations. Single or double quotes both work, as long as the same type is used at the beginning and end of the character value. 

The next data type is the `integer`, which is for whole numbers. It behaves very similarly to the `numeric` data type for most tasks or functions; however, it takes up less storage space than numeric data, so often tools will output integers if the data is known to be comprised of whole numbers. Just know that integers behave similarly to numeric values. If you wanted to create your own, you could do so by providing the whole number, followed by an upper-case L. 

The last data type we will discuss in much detail is the `logical` data type. This data type is for `TRUE` and `FALSE` values, and represents the Boolean data type. The `logical` data type can be specified using four values, `TRUE` in all capital letters, `FALSE` in all capital letters, a single capital `T` or a single capital `F`. 

There are two additional basic data types in R; the `complex` data type is for complex numbers with real and imaginary parts, but most of us do not need to use this data type unless we work with complex numbers. The last data type is `raw`, but we aren't going to go into details on this data type.

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

So far we have created the variable x that has the value 3, but what exactly is a variable? A variable is a symbolic name for information. You can think of variables in computer programming as being analogous to "buckets", where information can be maintained and referenced. On the outside of the bucket is a name, and when referring to the bucket, we use the name on the outside of the bucket, not the data stored inside.

Therefore, for the variable `x` we created previously, 'x' is the name on the outside of the bucket, and 3 is the value stored inside.

Let's create another variable called `y` and give it a value of 5. 

```r
# Assign the value 5 to a variable named y
y <- 5
```

We now see the variable `y` appear in our `Environment` window with the value 5. When assigning a value to an variable, R does not print anything to the console. However, you can force to print the value by using parentheses or by typing the variable name.

```
# Print to console contents of a variable by typing it's name
y
```


![Viewing your environment](../img/environment.png)

Now we can reference these buckets by name to perform mathematical operations on the values contained within. What do you get in the console when typing x + y? 

```r
# Adding contents of variables
x + y
```

Let's assign the output to another variable. We can call the variable just about anything we would like, but we are going to choose to call it `number`. To assign the output of x + y to number, we can type: number, arrow, x + y.

```r
number <- x + y
```

***

**Exercises**
1.	Try changing the value of the variable `x` to 5 and the value of variable `y` to 10. 
2.	Does anything happen to the variable `number`? If not, try to update `number`.

***

Let's go through the exercises together. To change the value of x to 5, we can type x, arrow, 5:

```
x <- 5
```

Similarly, to change the value of y to 10, we can type, y, arrow, 10:

```
y <- 10
```

Now let's look at `number` in our Environment. Has `number` updated? No. This is one feature of R to keep in mind when working through your analyses. If you update the dependencies for a variable, the variable will not automatically update. What do we need to do to update `number`? We need to reassign number to be x + y using the current values of x and y. So, we will type: number, arrow, x + y.

```
number <- x + y
```

### Tips on variable names

We mentioned earlier that you could name variables just about any name you would like; however, there are a few restrictions and a few suggestions for naming variables. Variables can be given almost any name, such as `x`, `current_temperature`, or
`subject_id`. However, there are some rules / suggestions you should keep in mind:

- Avoid names starting with a number (`2x` is not valid but `x2` is)
- Avoid names of fundamental functions in R (e.g., `if`, `else`, `for`, see [here](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Reserved.html) for a complete list). In general, even if it's allowed, it's best to not use other function names (e.g., `c`, `T`, `mean`, `data`) as variable names. When in doubt check the help to see if the name is already in use. 
- Make your names explicit and not too long.
- Keep in mind that **R is case sensitive** (e.g., `genome_length` is different from `Genome_length`)
- Avoid dots (`.`) within a variable name as in `my.dataset`. There are many functions in R with dots in their names for historical reasons, but because dots have a special meaning in R (for methods) and other programming languages, it's best to avoid them. 
- Use nouns for object names and verbs for function names
- Be consistent with the styling of your code (where you put spaces, how you name variable, etc.). In R, two popular style guides are [Hadley Wickham's style guide](http://adv-r.had.co.nz/Style.html) and [Google's](http://web.stanford.edu/class/cs109l/unrestricted/resources/google-style.html).

Names starting with numbers are not allowed in base R, nor should you use the names of fundamental functions. You won’t know these functions yet, but we have provided a link to them in the slides. A general rule of thumb is to not name a variable with a name of a function that you use in your analysis. Make your variable name explicit and not too long. Make the names intuitive, so that it is easy to figure out what the contents of the variable are. Keep in mind that R is case sensitive, so genome lengths in all lower case is not the same as genome lengths with a capital G.Try to avoid dots in variable names, like my.dataset, because dots have special meaning in R and in other programming languages, so even though it’s unlikely to cause you issues, it’s best to avoid them. Be consistent with the styling of your code, where you put spaces, how you name variables, ecetera. We have provided the links to two popular styling guides that we encourage you to look through to get an idea on how you may want to style your code for optimal readability and reproducibility.


