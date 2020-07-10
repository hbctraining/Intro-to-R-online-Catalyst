## Introduction

Welcome to segment 4B, "**Getting Help in R**". In this segment we will discuss different methods of finding help when working in R. Often, we get stuck while doing some analysis and while we know what it is we want to get done, we do not know the correct function to use. Other times we are using functions and find ourselves confronted with a cryptic error and we are unable to move forward. It is important for anyone who is new to R to know the right place to look for help. In this segment we will demonstrate various ways to access built-in help in R, and also provide some guidelines and helpful resources when asking for help.


## Finding functions but not knowing which package it is a part of

When starting out with an analysis in R, it can sometimes be overwhelming. You have the task you wish to execute, but are not aware of the function required to help you accomplish it. 

For example, suppose you would like to draw a scatter plot for your data. You have the x and y data points but how do you go about drawing it?

R has some functionality built-in for users to access help without leaving the RStudio interface. One example is the `apropos()` function. This function searches for objects, including functions, directly accessible in the current R session that have names matching the specified character string. The function searches the literal string or can take regular expressions as input. The function is case-insensitive.

Let's test this out using "scatter" as our search keyword:

```r
apropos("scatter")

[1] "scatter.smooth" "smoothScatter" 
```

The function returns two results. We can then use the help function, with the question mark, to open up documentation for each of these functions and find our more on what they do. Note that the result will be limited to the libraries that are loaded in your current R session.

```r
?scatter.smooth
```

Another built-in option is the function `RSiteSearch()`, however this does require an active internet connection. `RSiteSearch()` uses an internet search engine to search for information in function help pages and vignettes for all CRAN packages. Curly brackets can be used to specify multi-word terms. For example, 


```r
RSiteSearch("{generalized linear model}") 
```

This will open up a new window in your browser, returning information related to the term "generalized linear model" without matching the individual words "generalized", "linear", or "model". This is helpful because it searches for packages that you may not already have installed. However, it is limited to the CRAN repository.


## Finding functions specific to a package

Alternatively, you may know the package you need to use but need help finding out more on what functions to use. Suppose we are interested in using `ggplot2`, a package that was installed in the segment titled "Packages and Libraries". One way to get more information would be to use the `Package` tab in RStudio. If you click on the tab, you will see listed all packages that you have installed. For those *libraries that you have loaded*, you will see a blue checkmark in the box next to it. 

Type in "ggplot2" to the search box at the top of the tab. You should now see ggplot2 listed below.  Now, if you click on the hyperlinked `ggplot2` RStudio will open up the help documentation in the Help tab and you can scroll through it.

<img src="../img/ggplot_help.png" width="300">  

You will see all functions for this package listed alphabetically with a short description beside each. For some packages this might be helpful, but in other cases it would be nice to have a long form guide to the package. A vignette is a package guide that include comprehensive tutorials, sometimes with mock data that you can work through. You can access all of your libraries that you have installed and identify which have vignettes available using browseVignette(). Or alternatively, you can search for vignettes associated with the package you are interested in, for example `ggplot2`:

```r
browseVignettes("ggplot2")
```

A list of results will be displayed as an HTML page in a browser, and you can then click the hyperlinks to those that are of interest. For example, if we click on the "Aesthetics specifications", this takes us to an HTML page. This vignette summarises the various formats that grid drawing functions take, including things like color, fill and line types for plots. 


## Troubleshooting

Once you have familiarized yourself with the workings of R and start coding, you will no doubt encounter many error messages. Trying to decipher an error can be a time-consuming task, and often you can find yourself falling down the rabbit hole trying to fix it. This is common with R, but don't get discouraged! We have a few tips that can help when troubleshooting in R .

**Slide: Tips on Troublehooting**

*fade in bullets*

* Check your code for syntax errors
* Scan the error message for useful pointers
* Google cryptic error messages
* Ask for help


1. The most common error in RStudio is syntax errors. If something is not working check your code to make sure you haven't forgotten a comma, opened a bracket but haven’t closed it, or misspelled the name of a variable. The script editor in RStudio is good at picking up these types of errors and pointing it out to you with a little red x appearing next to that line of code.

2. R reports errors through messages in the console, which appear after you run code that is not quite right. Although the error messages look intimidating, they can sometimes be helpful. Take a quick look at the message to see if it is something that you can decipher. Error messages like "object not found" or "could not find function" and are pretty straightforward in telling you what the problem is and the solution is often an easy fix.

3. When dealing with more crytpic error messages, the solution is to Google it. R is backed by a large community of users and online resources for help. Chances are high that someone has already encountered the same or similar problem and you can use the answers given by R experts. 

4. Finally, if you have gotten to this point without a solution - you need to ask for help. 

**Slide: How to ask for help**

*fade in bullets*

* Be as precise as possible when describing your problem 
* Include the output of sessionInfo()
* Create a reproducible example


The key to getting help from someone is for them to grasp your problem rapidly. You should make it as easy as possible to pinpoint where the issue might be.

1. Try to use the correct words to describe your problem. The key point is to be as clear and precise as possible for people trying to help you. 

2. **Always include the output of `sessionInfo()`** as it provides critical information about your platform, the versions of R and the packages that you are using. All of this information can be very helpful to identify what might be causing your problem.	

3. If possible, **reproduce the problem using a very small `data.frame`**. Instead of your 50,000 rows and 10,000 columns one, create a small one with
the description of your problem. You can share an object containing the relevant R data structures that you have in your environment to an RData file. 

Please see the list of resources provided as links under this segment video. These are very helpful for when you are crafting your post for the first time.


**Slide: Where to ask for help?* 

* **Your friendly colleagues**: if you know someone with more experience than you, they might be able and willing to help you.

* **Stackoverflow**: Stack Overflow is a well organized and formatted site for help and discussions about programming.  Topics are tagged, and “r” is a very popular tag on the site. Search to see if you can find a post with a similar problem. If your question hasn't been answered before and is well crafted, chances are you will get an answer in less than 5 min.

* **The [R-help](https://stat.ethz.ch/mailman/listinfo/r-help)**: The R Project maintains a number of subscription-based email lists for posing and answering questions about R, including the general R-help email list. It is read by a lot of people (including most of the R core team), a lot of people post to it, but the tone can be pretty dry, and it is not always very welcoming to new users. 

* **The [Bioconductor support site](https://support.bioconductor.org/)**. The Bioconductor support site is very useful and if you tag your post with the package name, there is a high likelihood of getting an answer from the developer.

* If your question is about a specific package, see if there is a mailing list for it. Usually it's included in the DESCRIPTION file of the package that can
  be accessed using `packageDescription("name-of-package")`. You may also want to try to **email the author** of the package directly.

  
### More resources (for uner the video segment?)
* The [Posting Guide](http://www.r-project.org/posting-guide.html) for the R
  mailing lists.
* [How to ask for R help](http://blog.revolutionanalytics.com/2014/01/how-to-ask-for-r-help.html)
  useful guidelines
* The [Introduction to R](http://cran.r-project.org/doc/manuals/R-intro.pdf) can also be dense for people with little programming experience but it is a good place to understand the underpinnings of the R language.
* The [R FAQ](http://cran.r-project.org/doc/FAQ/R-FAQ.html) is dense and technical but it is full of useful information.


***

**Exercise - where does this go?**

The `ggplot2` package is part of the [`tidyverse` suite of integrated packages](https://www.tidyverse.org/packages/) which was designed to work together to make common data science operations more user-friendly. **We will be using the `tidyverse` suite in later lessons, and so let's install it**. _NOTE: This suite of packages is only available in CRAN._ 

***

---

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*

* *The materials used in this lesson are adapted from work that is Copyright © Data Carpentry (http://datacarpentry.org/). 
All Data Carpentry instructional material is made available under the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0).*

