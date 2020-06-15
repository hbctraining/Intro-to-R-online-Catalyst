* Creating project
* RStudio interface
* Organizing working directory
* Structuring your working directory

## Introduction

Welcome to segment 1A, Getting Started in RStudio. In this lesson we will walk through the steps for creating a project and  explore the various features of the RStudio interface. Within the project we will organize your working directory by setting up an appropriate directory structure and downloading the necessary files.

## Creating a new project in RStudio

When you're using RStudio, you have the option of creating a new R project. A project is simply a working directory designated with a `.RProj` file. We recommend creating a new R Project whenever you are starting a new research project. Once you’ve created a new R project, you should immediately create folders in the directory which will contain your R code, data files, notes, and other material relevant to your project.

Let's get started and create a new project directory for "Introduction to R": 

1. Start by opening up RStudio. 
2. Once it's open you can go to the `File` menu and select `New Project`. You can create an RStudio project:
* In a brand new directory
* In an existing directory where you already have R code and data
* Or by cloning a version control (Git or Subversion) repository
3. In the `New Project` window, choose `New Directory`. Then, choose `Empty Project`. You will be prompted to name your new directory. We will call our project `Intro-to-R`. Underneath you will see "Create the project as subdirectory of". Here, you have the opportunity to choose the location on your computer where you want this project to reside. Clicking on the "Browse" button will open up a File Explorer window and you can navigate to the appropriate folder.
4. Once you are done, click on `Create Project`. After your project is created, if it does not automatically open in RStudio, then go to the `File` menu, select `Open Project`, and choose `Intro-to-R.Rproj`.
5. When RStudio opens, you will see three panels in the window. Finally, go to the `File` menu and select `New File`, and select `R Script`. The RStudio interface should now have four panels

## RStudio Interface


Bullet points for slides:

**The RStudio Interface:**

1. **Console**: where you can type commands and see output. 
2. **Script editor**: where you can type out commands and save to file. Your code will not be evaluated until your "run" them in the console.
3. **Environment/History**: where you can see what objects are in your working space or environment or viw your command history.
4. **Files/Plots/Packages/Help** Here you can see file directories, view plots, see your packages and access R help documentation.

## Organizing your working directory & setting up

### Viewing your working directory

Before we organize our working directory, let's check to see where our current working directory is located by typing into the console:

```r
getwd()
```

Your working directory should be the `Intro-to-R` folder constructed when you created the project. The working directory is where RStudio will automatically look for any files you bring in and where it will automatically save any files you create, unless otherwise specified. 

You can visualize your working directory by selecting the `Files` tab from the **Files/Plots/Packages/Help** window. 

![Viewing your working directory](../img/getwd.png)

If you wanted to choose a different directory to be your working directory, you could navigate to a different folder in the `Files` tab, then, click on the `More` dropdown menu and select `Set As Working Directory`.
 
![Setting your working directory](../img/setwd.png)


### Structuring your working directory
To organize your working directory for a particular analysis, you should separate the original data (raw data) from intermediate datasets. For instance, you may want to create a `data/` directory within your working directory that stores the raw data, and have a `results/` directory for intermediate datasets and a `figures/` directory for the plots you will generate.

Let's create these three directories within your working directory by clicking on `New Folder` within the `Files` tab. 

![Structuring your working directory](../img/wd_setup.png)

When finished, your working directory should look like:

![Your organized working directory](../img/complete_wd_setup.png)

### Setting up 

This is more of a housekeeping task. We will be writing long lines of code in our script editor and want to make sure that the lines "wrap" and you don't have to scroll back and forth to look at your long line of code.

Click on "Tools" at the top of your RStudio screen and click on "Global Options" in the pull down menu.

![options](../img/tools_options.png)

On the left, select "Code" and put a check against "Soft-wrap R source files". Make sure you click the "Apply" button at the bottom of the Window before saying "OK".

![wrap_options](../img/wrap_option.png)

