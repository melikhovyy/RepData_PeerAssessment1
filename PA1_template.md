# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
# create the folder that will contain data file
if (!file.exists("data")) { dir.create("data") }
# unzip the archive and store it in the <./data> folder
unzip("./activity.zip",exdir="./data")

# read the data
AMD_original <- read.csv("data/activity.csv",
                         header=1,
                         sep=",",
                         na.strings="NA"
)

# add extra column with the date in proper format
AMD_original$corDate <- as.POSIXct(AMD_original$date)
```

## Total Number of Steps taken each day

The Hystogram of the total number of steps taken each day is obtained using this code (note that mean and median are also added):


```r
# Total Number of Steps taken each day
TotalNumberOfStepsEachDay <- aggregate(steps~corDate, data=AMD_original, FUN=sum, na.rm=TRUE)

# Histogram of the Total Number of Steps taken each day
hist(TotalNumberOfStepsEachDay$steps,
     breaks=50,
     col="red", 
     xlab="Total Number Of Steps Taken Each Day", 
     ylab="Frequency", 
     main="Histogram of Total Number Of Steps Taken Each Day"
     )

# Mean and Median are added onto the plot
abline(v = median(TotalNumberOfStepsEachDay$steps), col = "blue", lwd = 1)
abline(v = mean(TotalNumberOfStepsEachDay$steps), col = "green", lwd = 1)
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)<!-- -->


## Mean and median numbers of steps taken each day

Mean and median numbers of steps taken each day can be found using this code:


```r
mean(TotalNumberOfStepsEachDay$steps)
```

```
## [1] 10766.19
```

```r
median(TotalNumberOfStepsEachDay$steps)
```

```
## [1] 10765
```

## Time series plot of the average number of steps taken

In order to construct the time series plot of the average number of steps taken, the data must be "aggregated" using the following code:


```r
# Average Number of Steps taken each day
AverageNumberOfStepsEachDay <- aggregate(steps~corDate, data=AMD_original, FUN=mean, na.rm=TRUE)
```

Time series plot of the average number of steps taken is constructed using this code:


```r
# Plot of Average Number of Steps taken each day
with(AverageNumberOfStepsEachDay,
     plot(steps~corDate, 
          type="l",
          col="black", 
          xlab="Date", 
          ylab="Average Number of Steps"
          )
     )
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->



## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
