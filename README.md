An R package for visualizing changes in the subclonal architecture of tumors

This package is still in beta, and there may be minor changes to the parameters over the next few weeks.

## Installation instructions:

    #install devtools if you don't have it already for easy installation
    install.packages("devtools")
    library(devtools)
    install_github("chrisamiller/fishplot")

If you prefer to build the package by hand, follow these steps:

- Make sure that you have the dependencies from CRAN ("Hmisc","plotrix","png")

- Download and build from source:

        git clone git@github.com:chrisamiller/fishplot.git
        R CMD build fishplot
        R CMD INSTALL fishplot_0.1.tar.gz

## Usage
```R
    library(fishplot)

    #provide a list of timepoints to plot
    #You may need to add interpolated points to end up with the desired
    #visualization. Example here was actually sampled at days 0 and 150
    timepoints=c(0,30,75,150)      

    #provide a matrix with the fraction of each population
    #present at each timepoint
    frac.table = matrix(
      c(100, 45, 00, 00,
         02, 00, 00, 00,
         02, 00, 02, 01,
         98, 00, 95, 40),
      ncol=length(timepoints))

    #provide a vector listing each clone's parent
    #(0 indicates no parent)
    parents = c(0,1,1,3)

    #create a fish object
    fish = createFishObject(frac.table,parents,timepoints=timepoints)

    #calculate the layout of the drawing
    fish = layoutClones(fish)

    #draw the plot, using the splining method (recommended)
    #and providing both timepoints to label and a plot title
    fishPlot(fish,shape="spline",title.btm="Sample1",
             cex.title=0.5, vlines=c(0,150), 
             vlab=c("day 0","day 150"))
```

## Outputs
The tests/ directory contains several examples that explore many of the features in detail. Some example outputs are below.

### Simple plot with multiple subclones
![fishplot1](http://i.imgur.com/OECRqcD.png)

### More complex clonal structure
![fishplot1](http://i.imgur.com/gYO23si.png)

### Multiple independent clones, many timepoints
![fishplot1](http://i.imgur.com/uFPgudQ.png)

## FAQ

Q: Why "fishplot"?
A: The original visualization was put together by [Joshua McMichael](https://github.com/jmcmichael) for a paper on [relapsed AML](http://www.nature.com/nature/journal/v481/n7382/full/nature10738.html). Upon seeing the plots, someone remarked they looked like a tropical fish, and the name stuck.

## Notes
[Preprint currently posted at bioRxiv](http://biorxiv.org/content/early/2016/06/15/059055)
