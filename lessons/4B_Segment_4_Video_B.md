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


### Finding functions specific to a package

Alternatively, you may know the package you need to use but need help finding out more on what functions to use. Suppose we are interested in using `ggplot2`, a package that was installed in the segment titled "Packages and Libraries". One way to get more information would be to use the `Package` tab in RStudio. If you click on the tab, you will see listed all packages that you have installed. For those *libraries that you have loaded*, you will see a blue checkmark in the box next to it. 

Type in "ggplot2" to the search box at the top of the tab. You should now see ggplot2 listed below.  Now, if you click on the hyperlinked `ggplot2` RStudio will open up the help documentation in the Help tab and you can scroll through it.

<img src="../img/ggplot_help.png" width="300">  

You will see all functions for this package listed alphabetically with a short description beside each. For some packages this might be helpful, but in other cases it would be nice to have a long form guide to the package. A vignette is a package guide that include comprehensive tutorials, sometimes with mock data that you can work through. You can access all of your libraries that you have installed and identify which have vignettes available using browseVignette(). Or alternatively, you can search for vignettes associated with the package you are interested in, for example `ggplot2`:

```r
browseVignettes("ggplot2")
```

A list of results will be displayed as an HTML page in a browser, and you can then click the hyperlinks to those that are of interest. For example, if we click on the "Aesthetics specifications", this takes us to an HTML page. This vignette summarises the various formats that grid drawing functions take, including things like color, fill and line types for plots. 


## Asking for help

The key to getting help from someone is for them to grasp your problem rapidly. You
should make it as easy as possible to pinpoint where the issue might be.

1. Try to **use the correct words** to describe your problem. For instance, a package
is not the same thing as a library. Most people will understand what you meant,
but others have really strong feelings about the difference in meaning. The key
point is that it can make things confusing for people trying to help you. **Be as
precise as possible when describing your problem.**

2. **Always include the output of `sessionInfo()`** as it provides critical information about your platform, the versions of R and the packages that you are using, and other information that can be very helpful to understand your problem.

	```r
	sessionInfo()  #This time it is not interchangeable with search()
	```

3. If possible, **reproduce the problem using a very small `data.frame`**
instead of your 50,000 rows and 10,000 columns one, provide the small one with
the description of your problem. When appropriate, try to generalize what you
are doing so even people who are not in your field can understand the question. 
	- To share an object with someone else, you can provide either the raw file (i.e., your CSV file) with
your script up to the point of the error (and after removing everything that is
not relevant to your issue). Alternatively, in particular if your questions is
not related to a `data.frame`, you can save any other R data structure that you have in your environment to a file:

		```r
		# DO NOT RUN THIS!

		save(iris, file="/tmp/iris.RData")
		```

		The content of this `.RData` file is not human readable and cannot be posted directly on stackoverflow. It can, however, be emailed to someone who can read it with this command:

		```r
		# DO NOT RUN THIS!

		some_data <- load(file="~/Downloads/iris.RData")
		```

### Where to ask for help?

* **Google** is often your best friend for finding answers to specific questions regarding R. 
	- Cryptic error messages are very common in R - it is very likely that someone else has encountered this problem already! Start by googling the error message.  However, this doesn't always work because often, package developers rely on the error catching provided by R. You end up with general error messages that might not be very helpful to diagnose a problem (e.g. "subscript out of bounds").
* **Stackoverflow**: Search using the `[r]` tag. Most questions have already been answered, but the challenge is to use the right words in the search to find the answers: [http://stackoverflow.com/questions/tagged/r](http://stackoverflow.com/questions/tagged/r). If your question hasn't been answered before and is well crafted, chances are you will get an answer in less than 5 min.
* **Your friendly colleagues**: if you know someone with more experience than you,
  they might be able and willing to help you.
* **The [R-help](https://stat.ethz.ch/mailman/listinfo/r-help)**: it is read by a
  lot of people (including most of the R core team), a lot of people post to it,
  but the tone can be pretty dry, and it is not always very welcoming to new
  users. If your question is valid, you are likely to get an answer very fast
  but don't expect that it will come with smiley faces. Also, here more than
  everywhere else, be sure to use correct vocabulary (otherwise you might get an
  answer pointing to the misuse of your words rather than answering your
  question). You will also have more success if your question is about a base
  function rather than a specific package.
* **The [Bioconductor support site](https://support.bioconductor.org/)**. This is very useful and if you tag your post, there is a high likelihood of getting an answer from the developer.
* If your question is about a specific package, see if there is a mailing list
  for it. Usually it's included in the DESCRIPTION file of the package that can
  be accessed using `packageDescription("name-of-package")`. You may also want
  to try to **email the author** of the package directly.
* There are also some **topic-specific mailing lists** (GIS, phylogenetics, etc...),
  the complete list is [here](http://www.r-project.org/mail.html).
  
### More resources
* The [Posting Guide](http://www.r-project.org/posting-guide.html) for the R
  mailing lists.
* [How to ask for R help](http://blog.revolutionanalytics.com/2014/01/how-to-ask-for-r-help.html)
  useful guidelines
* The [Introduction to R](http://cran.r-project.org/doc/manuals/R-intro.pdf) can also be dense for people with little programming experience but it is a good place to understand the underpinnings of the R language.
* The [R FAQ](http://cran.r-project.org/doc/FAQ/R-FAQ.html) is dense and technical but it is full of useful information.


***

**Exercise**

The `ggplot2` package is part of the [`tidyverse` suite of integrated packages](https://www.tidyverse.org/packages/) which was designed to work together to make common data science operations more user-friendly. **We will be using the `tidyverse` suite in later lessons, and so let's install it**. _NOTE: This suite of packages is only available in CRAN._ 

***

---

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*

* *The materials used in this lesson are adapted from work that is Copyright © Data Carpentry (http://datacarpentry.org/). 
All Data Carpentry instructional material is made available under the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0).*

