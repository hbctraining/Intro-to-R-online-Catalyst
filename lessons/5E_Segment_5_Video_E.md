Description
This repository has teaching materials for a 3 hour, hands-on workshop led at a relaxed pace.

Learning Objectives
Understanding Tidyverse syntax: Tidyverse syntax is a bit different from base R with pipes, tibbles, and heavy opinions about row names
Wrangling data for use with analysis or plotting: Explore the functions available from the dplyr package to turn your data into the format you need it
Describe and utilize the ggplot2 grammar of graphics syntax: Create elaborate custom plots by learning the functions and structure for plotting with ggplot2
These materials are developed for a trainer-led workshop, but also amenable to self-guided learning.

Contents
Lessons	Estimated Duration
Setting up	15 min
Data wrangling with Tidyverse	75 min
Data visualization with ggplot2	90 min
Dataset
All the files used for the above lessons are linked within, but can also be accessed here.

Installation Requirements
Download the most recent versions of R and RStudio for your laptop:

R (Version 3.4 or higher)
RStudio
Install the required R packages by running the following code in RStudio:

# Install CRAN packages
install.packages("tidyverse")
install.packages("RColorBrewer")
Load the libraries to make sure the packages installed properly:

library(tidyverse)
library(RColorBrewer)
NOTE: The library used for the annotations associated with genes (here we are using org.Hs.eg.db) will change based on organism (e.g. if studying mouse, would need to install and load org.Mm.eg.db). The list of different organism packages are given here.

These materials have been developed by members of the teaching team at the Harvard Chan Bioinformatics Core (HBC). These are open access materials distributed under the terms of the Creative Commons Attribution license (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.

Training-modules is maintained by hbctraining.
This page was generated by GitHub Pages.
