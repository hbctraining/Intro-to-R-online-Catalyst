# Exercise


## Boxplot

Now that we have all the required information for plotting with ggplot2, let's try plotting a boxplot. A boxplot provides a graphical view of the distribution of data based on a five number summary. The top and bottom of the box represent the (1) first and (2) third quartiles (25th and 75th percentiles, respectively). The line inside the box represents the (3) median (50th percentile). The whiskers extending above and below the box represent the (4) maximum, and (5) minimum of a data set. The whiskers of the plot reach the minimum and maximum values that are not outliers. 

Outliers are determined using the interquartile range (IQR), which is defined as: Q3 - Q1. Any values that exceeds 1.5 x IQR below Q1 or above Q3 are considered outliers and are represented as points above or below the whiskers. These outliers are useful to identify any unexpected observations.

1. Use the `geom_boxplot()` layer to plot the differences in sample means between the Wt and KO genotypes.
2. Use the `fill` aesthetic to look at differences in sample means between the celltypes within each genotype.
3. Add a title to your plot.
4. Add 'Genotype' as your x-axis label and 'Mean expression' as your y-axis labels.
5. Theme changes:
  * Use the `theme_bw()` function to make the background white.
  * Change the size of your axes labels to 1.5x larger than the default.
  * Change the size of your plot title to 1.5x larger than default.
  * Center the plot title.

**Our final figure should look something like that provided below.**

<p align="center">
<img src="../img/ggboxplot_new.png" width="600">
</p>