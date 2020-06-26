## Introduction

Welcome to segment 1B, **Interacting with R**. In this segment we will begin by working in the console and interacting directly with R. We will then move to the script editor and demonstrate it's use, while also introducing some R syntax. Finally, we will bring in data to our project and describe it. This data will be useful in future segments.


## The Console window

There are **two main ways** of interacting with R in RStudio; using the **console** or by using **script editor**. The **console window** in RStudio, here in the bottom left hand side of Rstudio screen, is where the code will be executed. You can type commands directly into the console and upon pressing return the code will be executed and the result will be displayed.

Let's test it out with a simple mathematical operation:

```r
3 + 5
```

After pressing return, you should see the number 8 returned in the console.

In the R console, you will find that the flashing cursor is placed immediately after the `>` symbol. The `>` symbol represents the command prompt, it's called this because it is “prompting” you to feed it with some R code. 

Bullet point slide:

* Console is ready to accept commands: `>`.
* Console is waiting for you to enter more data: `+`.
* Console is hanging: absence of `>` or `+`. Press ESC to quit


Interpreting the command prompt can help understand when R is ready to accept commands. If R is ready to accept commands, the R console shows a `>` as the command prompt. Once the code is finished running, the console will display the results and come back with a new `>` prompt, ready to accept another commad.

If you see a `+` as the prompt, this means that R is still waiting for you to enter additional code as it assumes the code is incomplete. This can happen if you have typos in your code, for example, if you have not 'closed' a parenthesis or quotation. 

If you have run your code, waiting for it finish but not see the `>` returned, nor do you see a `+`, you can press the ESC key. This will stop the command in progress and return to you the command prompt. You can troubleshoot the problem and try running the code again.


## Script editor

The second way to interact with R is through your script editor. When you type code into an R script, you’ll notice that, unlike typing code into the Console, nothing happens. In order for R to interpret the code, you need to send it from the script editor to the console. Let's try typing the same `3 + 5` as before but this time in our editor. There are three ways in which you can send code to the console:

1. You can simply copy the code from the editor and paste it into the console. This is the least efficient way of going about it.
2. You can highlight the code or place your cursor on the line, then press `Ctrl + Enter`
3. You can highlight the code or place your cursor on the line, then Click on the 'Run' button at the top of the editor

There are certainly many cases where it makes sense to type code directly into the console. For example, to open a help menu, or to take a quick look at some data, or to do simple calculations. However, the problem with writing all your code in the console is that nothing that you write will be saved. Best practice is to enter the commands in the **script editor**, and save the script as a physical file. 

### Parts of speech

**Slide Title: Parts of speech for R syntax**
- Have the code chunk on the slide and enter circles (animation) on the different parts, as I talk about them?

```r
# Load libraries
library(Biobase)
library(limma)
library(ggplot2)

# Setup directory variables
baseDir <- getwd()
dataDir <- file.path(baseDir, "data")
metaDir <- file.path(baseDir, "meta")
resultsDir <- file.path(baseDir, "results")

# Load data
meta <- read.delim(file.path(metaDir, '2015-1018_sample_key.csv'), header=T, sep="\t", row.names=1)
```
As you begin with your own scripts in R, you will start to encounter the different parts of speech for R syntax. Here, we have an example script to give you an idea of the different parts and how they appear. The details of each will be covered in other segments.

  - Where you see the hashtag is where there is a comment in the code. If R sees a `#` at the beginning of a line, it knows not to try and interpret it as code.
  - On several of the lines, you will see what looks like an arrow. This is the assignment operator, which means variables are being created.
  - There are also many instances of parentheses in the example code, these are lines in which functions are being used.
  - Inside the parentheses you will often see text, but also cases in which it is left empty. The text inside represents arguments for the function, and you will see the use of `=` to specify the value for a particular argument.

With R code you will also find indentation and consistency in spacing. While this is not a necessary practice, it is highly recommended it as it can improve clarity and legibility of your code.

### Comments

Let's play around a bit with the hashtag by adding comments to our script. First we will add a title and a subtitle:

```r
# Introduction to R

## Interacting with R 
```
Note that we have used differing numbers of the hashtag to comment. It doesn't matter how many you have, as long as R sees one it knows not to run that code. Also, you may have noticed a difference in the text coloring of our comments. This syntax highlighting is a feature of RStudio, and is very helpful when reading code.

Next we will use the hashtag to add descriptions to our code:

```r
## I am adding 3 and 5. R is fun!
3+5
```

Now we can highlight the whole chunk of text and send it to the console. You should see that although both lines were sent to the console only the one line without the hashtag was interpreted. Now try sending both lines without the comment symbol:

```r
I am adding 3 and 5. R is fun!
3+5
```

R is trying to run that sentence as a command, and it doesn't work. We get an error in the console *"Error: unexpected symbol in "I am" means that the R interpreter did not know what to do with that command."*

A shortcut for commenting is `Ctrl + Shift + C`. If you want to comment an entire chunk of text you could try this:

**Highlight code and use comment shortuct**
```r
# I am adding 3 and 5. R is fun!
# 3+5
```

When creating scripts for your own analyses, be sure to comment liberally. This will help future you and other collaborators know what each line of code (or code block) was meant to do. Your code and workflow are much more reproducible with documentation. Remember, our end goal is not just to "do stuff", but to do it in a way that anyone can easily and exactly replicate our workflow and results. 


## Interacting with data in R

Next, let's get some data setup in our project. R is commonly used for handling big data, and so it only makes sense that we learn about R in the context of some dataset. Let's take a few minutes to add files to our working directory and familiarize ourselves with the dataset.

You can access the files we need for this workshop using the links provided below the segment video. If you right click on the link, and "Save link as.." you should see a file explorer window open. Navigate to the location on your filesystem where you have created the `Intro-to-R` project, then click on the `data` folder. You will need to do this for each of the two files.

**Q: Do we just have the files in our data folder, already populated? We won't have a link to show as example** 

Once you have done so, you can go back to your RStudio window and take a look at your working directory. If you click on the `data` folder you should see the two files there: `counts.rpkm.csv` and `mouse_exp_design.csv`. If you find the files are in the data folder but do not have the extension `.csv`, rather they have `.txt`, you will want to change this. In the File tab, check the box next to the file. Then click on `Rename`. A dialog box will pop up asking you to enter the new name, here you can change the .txt to .csv

The counts.rpkm.csv file represents normalized count data obtained from RNA-sequencing of the 12 mouse brain samples. This data is stored in a comma separated values (CSV) file as a 2-dimensional matrix, with **each row corresponding to a gene and each column corresponding to a sample**.

**Slide with this data file image:**

<img src="../img/counts_view.png" width="900"> 


The mouse_exp_design file is the metadata file for this data. This file contains information about the normalized count data. In this file, each row corresponds to a sample. The first column contains the row names, and **note that these are identical to the column names in our expression data file above** (albeit, in a slightly different order). The next few columns contain information about our samples that allow us to categorize them. For example, the second column contains genotype information for each sample. Each sample is classified in one of two categories: Wt (wild type) or KO (knockout). 

<img src="../img/metadata_view.png" width="400"> 

R is particularly good at handling this type of **categorical data**. Rather than simply storing this information as text, the data is represented in a specific data structure which allows the user to sort and manipulate the data in a quick and efficient manner. This will be discussed in more detail in later segments.








