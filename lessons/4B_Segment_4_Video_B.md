## Introduction

Welcome to segment 4B, "**Getting Help in R**". In this segment we will discuss different methods of finding help when working in R. Often, we get stuck while doing some analysis and while we know what it is we want to get done, we do not know the correct function to use. Other times we are using functions and find ourselves confronted with a cryptic error and we are unable to move forward. It is important for anyone who is new to R to know the right place to look for help. In this segment we will demonstrate various ways to access built-in help in R, and also provide some guidelines and helpful resources when asking for help.


### Finding functions but not knowing which package it is a part of

When starting out with an analysis in R, it can sometimes be overwhelming. You have the task you wish to execute, but are not aware of the function required to help you accomplish it. 

For example, suppose you would like to draw a scatter plot for your data. You have the x and y data points but how do you go about drawing it?

R has some functionality built-in for users to access help without leaving the RStudio interface. One example is the 

you can use `help.search()` (*but only looks through the installed packages*):

```r
help.search("scatter")
```

If you can't find what you are looking for, you can use the [rdocumention.org](https://www.rdocumentation.org/) website that search through the help files across all packages available.



### Finding functions specific to a package

Alternatively, you may know the package you need to use but need help finding out more on what packages are involved. And finally, you may be running through your analysis but run hit a wall because of an error that you just can't get past. In this segment we provide solutions on the best ways to find help when you run into problems such as these.


This is your first time using `ggplot2`, how do you know where to start and what functions are available to you? One way to do this, is by using the `Package` tab in RStudio. If you click on the tab, you will see listed all packages that you have installed. For those *libraries that you have loaded*, you will see a blue checkmark in the box next to it. Scroll down to `ggplot2` in your list:

<img src="../img/ggplot_help.png" width="300">  


If your library is successfully loaded you will see the box checked, as in the screenshot above. Now, if you click on `ggplot2` RStudio will open up the help pages and you can scroll through.

An alternative is to find the help manual online, which can be less technical and sometimes easier to follow. For example, [this website](http://docs.ggplot2.org/current/) is much more comprehensive for ggplot2 and is the result of a Google search. Many of the Bioconductor packages also have very helpful vignettes that include comprehensive tutorials with mock data that you can work with.


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

