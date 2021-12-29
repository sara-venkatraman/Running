Sara’s running data
================

This repository stores `RunningData.csv`, in which I record information
about each of my runs (e.g. distance, time, location, average pace). If
you think of anything interesting to do with this data, please let me
know!

``` r
# Read data, format dates and times
runningData <- read.csv("RunningData.csv")
runningData$Date <- as.Date(runningData$Date, format="%m/%d/%y")
runningData$Average_Pace <- as.POSIXct(runningData$Average_Pace, format="%M:%S")

# Plots
library(ggplot2); library(gridExtra); library(MetBrewer)
plotColors <- met.brewer("Gauguin", 3)
p1 <- ggplot(runningData, aes(x=Date, y=Miles)) + geom_point(color=plotColors[1]) + geom_line(color=plotColors[1]) + labs(y="Distance (miles)", title="How far I ran") + theme_bw()
p2 <- ggplot(runningData, aes(x=Date, y=Time_Minutes)) + geom_point(color=plotColors[2]) + geom_line(color=plotColors[2]) + labs(y="Time (minutes)", title="Time I spent running") + theme_bw()
p3 <- ggplot(runningData, aes(x=Date, y=Average_Pace)) + geom_point(color=plotColors[3]) + geom_line(color=plotColors[3]) + labs(y="Minutes:seconds", title="Average pace (time per mile)") + scale_y_datetime(date_labels="%M:%S") + theme_bw()
grid.arrange(p1, p2, p3, nrow=1)
```

![](Plots/README-Running-Plots-1.png)<!-- -->

Total miles since 11/29/21:

``` r
sum(runningData$Miles)
```

    ## [1] 70.45
