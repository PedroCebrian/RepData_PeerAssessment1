# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

The data is located inside a compressed file "activity.zip". The first task is to open a connection with the file in order to access the compressed data and read this data into an R data frame.


```r
fname <- "activity.zip"
con <- unz(fname, "activity.csv")
data <- read.csv(con, colClasses = c("numeric", "character", "character"))
```


After loading the data we transform the interval column into a factor and the date column into R dates objects. This is the best option to perform subsequent analyses.


```r
data$interval <- as.factor(data$interval)
data$date <- as.Date(data$date)
```




## What is mean total number of steps taken per day?

In order to calculate the mean number of steps per day we will first create a new data frame with the total number of steps per day


```r
library(reshape2)
mdata <- melt(data, id = c("interval", "date"))
totalSteps <- dcast(mdata, date ~ variable, sum, na.rm = T)
```


It is important to note that the missing values are deleted in order to perform the calculations.

Histogram of the total number of steps taken per day.


```r
hist(totalSteps$steps, breaks = 20, col = "blue", main = "Histogram of total number of steps per day", 
    xlab = "Number of steps")
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 


The following code calculates the mean and median of the total number of steps per day.


```r
mean <- round(mean(totalSteps$steps))
median <- median(totalSteps$steps)
```

The average number of steps taken per day is 9354 and the median number of step is 1.0395 &times; 10<sup>4</sup>.




## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
