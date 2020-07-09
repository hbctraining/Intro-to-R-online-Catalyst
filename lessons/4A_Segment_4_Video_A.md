## Introduction

Welcome to segment 4A, "Packages and Libraries in R". In this segment we will discuss what a package is in R and demonstrate the different ways in which you can install them. Once installed, we will go through the steps required to ensure it was a successful installation. We will also describe the process of utilizing packages in R by loading libraries.

## Packages and Libraries

**Slide: Packages **

*fade in bullets*

A **Package** in R is a collection of R functions, data, and compiled code in a well-defined format. As part of your R installation, you have access to a set of **standard (or base) packages**. These base packages are considered part of the R source code and contain **basic functions** that allow R to work, and enable standard statistical and graphical functions on datasets. Functions that have been used in any of the previous segments are part of these base packages.

The more you work with R, you will come to realize that there is a cornucopia of R packages that offer a wide variety of functionality. There are currently over 16,000 user contributed packages and this number continues to increase exponentially. To use additional packages you will be required to install it, which simply means downloading the package code onto your personal computer. 

**Slide: Libraries**

*fade in bullets*

A **Library** in R, refers to the directory or folder on your computer where the packages are stored. After a package is installed on your computer, you need to load the library into your R session. Loading the library allows the user to access any functions or datasets that are part of the package.

**Slide: Packages vs. Libraries 

<img src="../img/install_vs_library.jpeg" width="600">

*Analogy and image credit to [Dianne Cook](https://twitter.com/visnut/status/1248087845589274624) of [Monash University](https://www.monash.edu/).* 

The terms *package* and *library* are sometimes used synonymously and there has been [discussion](http://www.r-bloggers.com/packages-v-libraries-in-r/) amongst the community to resolve this. An analogy used to help differentiate between packages and libraries, is if you think of the package installation as installing a lightbulb into your light fixture. You do this once and you're all set for awhile. When we want to use the light, we use the switch to turn it on or off. Similarly, when we want to use a package we need to load the library every time we start a new RStudio environment.


To check what libraries are loaded in your current R session, we use a function called `sessionInfo()`. This is a function that does not require any arguments. 

```r
sessionInfo() #Print version information about R, the OS and attached or loaded packages

```
In the console, you will see text returned describing your R session. This includes the version of R you are using, details on your computer and operating system. Further down you will see listed the libraries that have been loaded. Note that right now you should only see the base packages listed.

Another function that is helpful in identifying the libraries loaded in your R session is `search()`. Similar to `sessionInfo()` there are no arguments required as input. The output of this function is less detailed, reporting only the list of loaded libraries.

```r
search() # Gives a list of attached packages
```

## Repositories

R packages are stored in repositories, typically they are online and accessible to everyone. Three of the most popular repositories for R packages are CRAN, Bioconductor and GitHub. We will discuss each repository briefly and then introduce you to the functions used for installing packages from each. 

**Slide for each; including code**
- Don't run the code now; just show each clip on the slides
- Can we open a browser for each repository live? or do we do screenshots?

### CRAN 

The first, and most common repository is CRAN, which stands for the Comprehensive R Archive Network. This is where the latest downloads of R (and legacy versions) are found in addition to source code for thousands of different user contributed R packages. The R foundation coordinates it, and for a package to be published here, it needs to pass several tests that ensure it is following CRAN policies.

<img src="../img/cran_packages.png" width="600">

Packages for R can be installed from the [CRAN](http://cran.r-project.org/) repository using the `install.packages` function. This function will download the source code from CRAN and install the package (and any dependencies) locally on your computer. 

An example is given below for the `ggplot2` package:

```r
install.packages("ggplot2")
```

### Bioconductor

Bioconductor is a topic specific repository, intended for open source software for bioinformatics. The packages provide tools for the analysis and comprehension of high-throughput **genomic data**. These packages include (but is not limited to) tools for performing statistical analysis, annotation packages, and accessing public datasets. Similar to CRAN, it has its own submission and review processes, and its community is very active having several conferences and meetings per year. There are many packages that are available in CRAN and Bioconductor, but there are also packages that are specific to one repository. 

<img src="../img/bioconductor_logo.png" width="300">


To install a package from Bioconductor, you will first need to install BiocManager. *This only needs to be done once ever for your R installation.* Then you can use the `install()` function to install a package by providing the name in quotations. Note the syntax with the double colon is used to indicate that the `install()` function should be used from the BiocManager package.

```r
install.packages("BiocManager")
BiocManager::install("ggplot2")
```

### Github

Github is probably the most popular repository for open source projects, although it is not R specific. Its popularity comes from the unlimited space for open source, the integration with a version control software, and its ease to share and collaborate with others. Many popular R packages reside in GitHub and are commonly used by many in the R community. However, be aware that sometimes these packages can be the development version. Additionally, there is no review process associated with R packages in GitHub.

To install a package from GitHub, you will first need to install a package called devtools. The devtools package contains specific functions for each repository, and the function for GitHub is install_github. In quotations, you will need to provide the 	repository address in the format username/repo:

```r
install.packages("devtools")
devtools::install_github("tidyverse/ggplot2")
```

## Package installation from source

Finally, R packages can also be installed from source. This is useful when you do not have an internet connection (and have the source files locally), since the other methods we described are retrieving the source files from remote sites. 

To install from source, we use the same `install.packages` function but we have additional arguments that provide *specifications* to *change from defaults*. Instead of the package name, we provide the path on your personal computer to where the source files reside. We also set type = "source" and specify that we are not accessing a repository by setting repos = NULL. 

```r
# DO NOT RUN THIS!

install.packages("~/Downloads/ggplot2_1.0.1.tar.gz", type="source", repos=NULL)
```

## Installing `ggplot2`

Let's test out a package installation! We will install ggplot2, a popular package for data visualization which will be used in later segments. As we noted, there is more than one repository from which we can install this package. Here, we will use the CRAN method `install.packages()`:

```r
install.packages("ggplot2")
```



Once you have the package installed, you can **load the library** into your R session for use. Any of the functions that are specific to that package will be available for you to use by simply calling the function as you would for any of the base functions. *Note that quotations are not required here.*


```r
library(ggplot2)
```

You can also check what is loaded in your current environment by using `sessionInfo()` or `search()` and you should see your package listed as:

```r
other attached packages:
[1] ggplot2_2.0.0
```

In this case there are several other packages that were also loaded along with `ggplot2`. Talk more about these!

