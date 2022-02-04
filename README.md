Running data
================

This repository stores `RunningData.csv`, in which I record information
about each of my runs (e.g. distance, time, average pace).

``` r
# Read data, format dates and times
runningData <- read.csv("RunningData.csv")
runningData$Date <- as.Date(runningData$Date, format="%m/%d/%y")
runningData$Average_Pace <- as.POSIXct(runningData$Average_Pace, format="%M:%S")

# Plots
library(ggplot2); library(ggpubr)
plotSettings <- list(geom_line(color="lightsteelblue3"), geom_point(aes(color=Treadmill_Road)), scale_color_manual(values=c("orange3", "dodgerblue3")), theme_bw())
p1 <- ggplot(runningData, aes(x=Date, y=Miles)) + labs(y="Distance (miles)", title="How far I ran") + plotSettings
p2 <- ggplot(runningData, aes(x=Date, y=Time_Minutes)) + labs(y="Time (minutes)", title="Time I spent running") + plotSettings
p3 <- ggplot(runningData, aes(x=Date, y=Average_Pace)) + labs(y="Minutes:seconds", title="Average pace (time per mile)") + scale_y_datetime(date_labels="%M:%S") + plotSettings + theme(legend.background=element_rect(size=0.1, linetype="solid", color="black")) + labs(color="Where I ran") + guides(color=guide_legend(nrow=1))
ggarrange(p1, p2, p3, nrow=1, common.legend=T, legend.grob=get_legend(p3), legend="bottom")
```

![](Plots/README-Running-Plots-1.png)<!-- -->

Total miles since 11/29/21:

``` r
sum(runningData$Miles)
```

    ## [1] 142.64
