## Introduction

Welcome to segment 1B, **Interacting with R**. In this segment we will begin by working in the console and interacting directly with R. We will then move to the script editor and demonstrate how you can 

## Interacting with R

Now that we have our interface and directory structure set up, let's start playing with R! There are **two main ways** of interacting with R in RStudio: using the **console** or by using **script editor** (plain text files that contain your code).

### Console window
The **console window** (in RStudio, the bottom left panel) is the place where R is waiting for you to tell it what to do, and where it will show the results of a command.  You can type commands directly into the console, but they will be forgotten when you close the session. 

Let's test it out:

```r
3 + 5
```

![Running in the console](../img/console.png)

### Script editor

Best practice is to enter the commands in the **script editor**, and save the script. You are encouraged to comment liberally to describe the commands you are running using `#`. This way, you have a complete record of what you did, you can easily show others how you did it and you can do it again later on if needed. 

**The Rstudio script editor allows you to 'send' the current line or the currently highlighted text to the R console by clicking on the `Run` button in the upper-right hand corner of the script editor**. Alternatively, you can run by simply pressing the `Ctrl` and `Enter` keys at the same time as a shortcut.

Now let's try entering commands to the **script editor** and using the comments character `#` to add descriptions and highlighting the text to run:
	
	# Intro to R Lesson
	# Feb 16th, 2016

	# Interacting with R
	
	## I am adding 3 and 5. R is fun!
	3+5

![Running in the script editor](../img/script_editor.png)

You should see the command run in the console and output the result.

![Script editor output](../img/script_editor_output.png)
	
What happens if we do that same command without the comment symbol `#`? Re-run the command after removing the # sign in the front:

```r
I am adding 3 and 5. R is fun!
3+5
```

Now R is trying to run that sentence as a command, and it 
doesn't work. We get an error in the console *"Error: unexpected symbol in "I am" means that the R interpreter did not know what to do with that command."*


### Console command prompt

Interpreting the command prompt can help understand when R is ready to accept commands. Below lists the different states of the command prompt and how you can exit a command:

**Console is ready to accept commands**: `>`.

If R is ready to accept commands, the R console shows a `>` prompt. 

When the console receives a command (by directly typing into the console or running from the script editor (`Ctrl-Enter`), R will try to execute it.

After running, the console will show the results and come back with a new `>` prompt to wait for new commands.


**Console is waiting for you to enter more data**: `+`.

If R is still waiting for you to enter more data because it isn't complete yet,
the console will show a `+` prompt. It means that you haven't finished entering
a complete command. Often this can be due to you having not 'closed' a parenthesis or quotation. 

**Escaping a command and getting a new prompt**: `esc`

If you're in Rstudio and you can't figure out why your command isn't running, you can click inside the console window and press `esc` to escape the command and bring back a new prompt `>`.


***
**Exercise**

1. Try highlighting only `3 +` from your script editor and running it. Find a way to bring back the command prompt `>` in the console.

***
R is commonly used for handling big data, and so it only makes sense that we learn about R in the context of some kind of relevant data. Let's take a few minutes to add files to the folders we created and familiarize ourselves with the data.

### Adding files to your working directory

You can access the files we need for this workshop using the links provided below. If you right click on the link, and "Save link as..". Choose `~/Desktop/Intro-to-R/data` as the destination of the file. You should now see the file appear in your working directory. **We will discuss these files a bit later in the lesson.**

* Download the **normalized counts file** by right clicking on [this link](https://raw.githubusercontent.com/hbc/NGS_Data_Analysis_Course/master/sessionII/data/counts.rpkm.csv)
* Download **metadata file** using [this link](https://github.com/hbc/NGS_Data_Analysis_Course/raw/master/sessionII/data/mouse_exp_design.csv)

> *NOTE:* If the files download automatically to some other location on your laptop, you can move them to the your working directory using your file explorer or finder (outside RStudio), or navigating to the files in the `Files` tab of the bottom right panel of RStudio

### The dataset

In this example dataset, we have collected whole brain samples from 12 mice and want to evaluate expression differences between them. The expression data represents normalized count data obtained from RNA-sequencing of the 12 brain samples. This data is stored in a comma separated values (CSV) file as a 2-dimensional matrix, with **each row corresponding to a gene and each column corresponding to a sample**.

<img src="../img/counts_view.png" width="900"> 

### The metadata
We have another file in which we identify **information about the data** or **metadata**. Our metadata is also stored in a CSV file. In this file, each row corresponds to a sample and each column contains some information about each sample. 

The first column contains the row names, and **note that these are identical to the column names in our expression data file above** (albeit, in a slightly different order). The next few columns contain information about our samples that allow us to categorize them. For example, the second column contains genotype information for each sample. Each sample is classified in one of two categories: Wt (wild type) or KO (knockout). *What types of categories do you observe in the remaining columns?*

<img src="../img/metadata_view.png" width="400"> 

R is particularly good at handling this type of **categorical data**. Rather than simply storing this information as text, the data is represented in a specific data structure which allows the user to sort and manipulate the data in a quick and efficient manner. We will discuss this in more detail as we go through the different lessons in R!  

## Best practices

Before we move on to more complex concepts and getting familiar with the language, we want to point out a few things about best practices when working with R which will help you stay organized in the long run:

* Code and workflow are more reproducible if we can document everything that we do. Our end goal is not just to "do stuff", but to do it in a way that anyone can easily and exactly replicate our workflow and results. **All code should be written in the script editor and saved to file, rather than working in the console.** 
* The **R console** should be mainly used to inspect objects, test a function or get help. 
* Use `#` signs to comment. **Comment liberally** in your R scripts. This will help future you and other collaborators know what each line of code (or code block) was meant to do. Anything to the right of a `#` is ignored by R. *A shortcut for this is `Ctrl + Shift + C` if you want to comment an entire chunk of text.*



## The R syntax
Now that we know how to talk with R via the script editor or the console, we want to use R for something more than adding numbers. To do this, we need to know more about the R syntax. 


Below is an example script highlighting the many different "parts of speech" for R (syntax):

  - the **comments** `#` and how they are used to document function and its content
  - **variables** and **functions**
  - the **assignment operator** `<-`
  - the `=` for **arguments** in functions

_NOTE: indentation and consistency in spacing is used to improve clarity and legibility_


### Example script

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


