
## Introduction

Welcome to segment 1A, **Getting Started in RStudio**. In this lesson we will walk through the steps for creating a project and explore the various features of the RStudio interface. Within the project we will organize your working directory by setting up an appropriate directory structure, and introduce some basic housekeeping tasks.

## Creating a new project in RStudio

When you're using RStudio, you have the option of creating a new R project. A project is simply a working directory designated with a `.RProj` file. We recommend creating a new R Project whenever you are starting a new research project.

Let's get started and create a new project directory for "Introduction to R": 

1. Start by opening up RStudio. 
2. Once it's open you can go to the `File` menu and select `New Project`. You can create an RStudio project:
* In a brand new directory
* In an existing directory where you already have R code and data
* Or by cloning a version control (Git or Subversion) repository
3. In the `New Project` window, choose `New Directory`. Then, choose `Empty Project`. You will be prompted to name your new directory. We will call our project `Intro-to-R`. Underneath you will see "Create the project as subdirectory of". Here, you have the opportunity to choose the location on your computer where you want this project to reside. Clicking on the "Browse" button will open up a File Explorer window and you can navigate to the appropriate folder.
4. Once you are done, click on `Create Project`. After your project is created, if it does not automatically open in RStudio, then go to the `File` menu, select `Open Project`, and choose `Intro-to-R.Rproj`.
5. When RStudio opens, you will see three panels in the window. Finally, go to the `File` menu and select `New File`, and select `R Script`. 

## RStudio Interface

Bullet points for slides:

* **Console**
* **Script editor**
* **Environment/History**
* **Files/Plots/Packages/Help**

The RStudio interface should now have four panels or windows. Let's take a moment to discuss what each window does in more detail. 

* On the bottom left corner we have the console window. This is where R actually evaluates code. Here, you can type out code and once you press the return key, you will get an immediate response as R executes the code. For example, if you type 1+1 into the console and press enter, you’ll see that R immediately gives an output of 2.
* Above the console, we have the script editor. You can think of this as notepad for your code. Here, you can type out commands and save to file. R scripts are just text files with the “.R” extension. Note that when you’re typing code in the script editor, R won’t actually evaluate the code as you type. To have R actually evaluate your code, you need to first ‘send’ the code to the Console (we’ll talk about this in another segment).
* In the upper right hand corner is the Environment and History window. The Environment tab of this window shows you the names of all the data objects that you’ve defined in your current R session. The History tab simply shows you a history of all the code you’ve previously evaluated in the console.
* The last window in the bottom right hand corner shows you a lot of heplful information. The files tab gives you access to the file directory on your hard drive. The plots tab allows you to see the plots and gives you options to save them to file. The packages tab shows a list of all the R packages installed on your hard drive and indicates whether or not they are currently loaded. Finally, the help tab opens up the R help documentation pages.


## Organizing your working directory

Now that we are familiarized with the RStudio interface, we can continue to organize our R project. Let's begin by checking to see where our current working directory is located. We can do this by typing into the console:

```r
getwd()
```

In the console, you should see a path returned. This path is the location on your computer where the `Intro-to-R` folder lives, which is also the directory chosen when creating this project. The working directory is where RStudio will automatically look for any files you bring in and where it will automatically save any files you create, unless otherwise specified. 


Your working directory can also be viewed by selecting the `Files` tab from the bottom right window. 

![Viewing your working directory](../img/getwd.png)

One nice feature of the files tab is that you can use it to set your working directory to a new folder. Once you navigate to a folder you want to read and save files to, click on the `More` dropdown menu and select `Set As Working Directory`.
 
![Setting your working directory](../img/setwd.png)

Once you’ve started a new R project, you should create folders in the directory which will contain your R code, data files, notes, and other material relevant to your project. For instance, you may want to create a `data/` directory within your working directory that stores the raw data, and have a `results/` directory for intermediate datasets and a `figures/` directory for the plots you will generate.

Let's create these three directories within your working directory by clicking on `New Folder` within the `Files` tab. 

![Structuring your working directory](../img/wd_setup.png)

When finished, your working directory should look like what we have here :

![Your organized working directory](../img/complete_wd_setup.png)

## User configuration settings

Finally, we would like to bring to your attention user configuration options for your Rstudio workspace. If you click on "Tools" at the top of your RStudio screen and click on "Global Options" in the pull down menu you will see a dialog box open. On left hand side you will see an array of categories listed. These are different aspects of Rstudio that can be changed by the user.

![options](../img/tools_options.png)

Since we will be writing long lines of code in our script editor, we want to make sure that the lines "wrap" and you don't have to scroll right and left just to read the code. To enable this feature, in your dialog box select "Code" from the left hand panel and put a check against "Soft-wrap R source files". Then you will want to you click the "Apply" button at the bottom of the Window before saying "OK".

![wrap_options](../img/wrap_option.png)


## Conclusion

In this segment we have dabbled with a few of the features that RStudio has to offer. Additionally, you should now be familiar with the RStudio interface and know how and when to navigate between the four different panes. Of course, we have only scratched the surface. There is so much more to Rstudio and as you go through additional segments we hope you will continue to build on the foundational concepts described here.
