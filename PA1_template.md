# Reproducible Research: Peer Assessment 1

---
author: "B. Spangehl"
date: "Saturday, July 19, 2014"
output: html_document
---




### Loading and preprocessing the data

```r
fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
fileZip <- "./activity.zip"

if (file.exists(fileZip) == F) {
  download.file(fileUrl, fileZip, mode = "wb")
  dateDownLoaded <- date()
}

df <- read.csv(unz(fileZip,"activity.csv")                
               ,colClasses=c("integer","Date","integer"),na.strings="NA")
```


### What is mean total number of steps taken per day?

```r
steps.date <- aggregate(steps ~ date, data = df, sum)
```

1. Make a histogram of the total number of steps taken each day

```r
ggplot(steps.date, aes(x=steps)) + xlab("No. of Steps") + ylab("Count") + 
      geom_histogram(binwidth = 1000)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

2. Calculate and report the **mean** and **median** total number of steps taken per day  
Mean of total number of steps taken per day: 1.0766 &times; 10<sup>4</sup>.  
Median of total number of steps taken per day: 10765.


### What is the average daily activity pattern?
1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
steps.interval <- aggregate(steps ~ interval, data = df, mean)
plot(steps.interval, type = "l", xlab("Interval"), ylab("Steps"))
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
steps.interval$interval[which.max(steps.interval$steps)]
```

```
## [1] 835
```

### Imputing missing values



### Are there differences in activity patterns between weekdays and weekends?
