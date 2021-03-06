Running data
================

This repository stores `RunningData.csv`, in which I record information
about each of my runs (e.g.┬ádistance, time, average pace).

``` r
# Read data, format dates and times
runningData <- read.csv("RunningData.csv")
runningData$Date <- as.Date(runningData$Date, format="%m/%d/%y")
runningData$Average_Pace <- as.POSIXct(runningData$Average_Pace, format="%M:%S")

# Plots 
library(ggplot2); library(ggpubr); library(scales); library(ggthemr); ggthemr('dust')
plotSettings <- list(geom_line(color="gray70"), geom_point(aes(color=Treadmill_Road)), scale_color_manual(values=c(alpha("orange3", 0.8), alpha("dodgerblue3",0.8))), theme(plot.title=element_text(hjust=0.5)), theme(legend.position="none"), scale_x_date(date_breaks="1 month", date_labels="%B-%y"), theme(axis.text.x=element_text(angle=45, vjust=1, hjust=1)))
p1 <- ggplot(runningData, aes(x=Date, y=Miles)) + geom_hline(yintercept=13.1, linetype="dotted", color = "mistyrose4") + geom_text(label="13.1 (half marathon)", x=as.Date("2021-12-18"), y=13.5, color="mistyrose4", size=2.5) + labs(y="Distance (miles)", title="How far I ran") + plotSettings + scale_y_continuous(breaks=seq(0,16,3))
p2 <- ggplot(runningData, aes(x=Date, y=Average_Pace)) + labs(y="Minutes:seconds", title="Average pace (time per mile)") + scale_y_datetime(date_labels="%M:%S") + labs(color="Where I ran") + plotSettings +  theme(legend.position=c(0.15, 0.18), legend.background=element_rect(size=0.1, linetype="solid", color="black"), legend.margin=margin(2,3,2,3), legend.title=element_text(size=9, face="bold"), legend.text=element_text(size=8)) + guides(color=guide_legend(override.aes=list(size=1)))
ggarrange(p1, p2, nrow=1)
```

![](Plots/README-Running-Plots-1.png)<!-- --> Total miles since
11/29/21:

``` r
sum(runningData$Miles)
```

    ## [1] 686.18

Average distance during the last 10 runs:

``` r
mean(tail(runningData$Miles, 10))
```

    ## [1] 11.517
