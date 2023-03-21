---
title: "14- Basic plotting in R Programming"
datePublished: Wed Jul 21 2021 17:28:19 GMT+0000 (Coordinated Universal Time)
cuid: ckrdreooz0ffe91s17fqeb8x8
slug: 14-basic-plotting-in-r-programming
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1626888480187/u1ldsq4e0.png
tags: tutorial, r, research, coding, programming-languages

---

#### Load trees data from datasets library

```r
library(datasets)
tr<-trees 
head(tr)
```

#### Histogram

```r
hist(tr$Volume, col = 'darkred',main="Your title", xlab="Volume")
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626887999000/qdl5TFPgcZ.png align="left")

#### Barplot

```r
barplot(tr$Height, names.arg=c(1:31), col='darkgreen')
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626888032088/T9brNjEyJ.png align="left")

#### Boxplot

```r
boxplot(tr$Height, col = 'darkblue', xlab='Height',ylab='Height (m)')
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626887961279/EWM6UO86M.png align="left")

```r
boxplot(tr, col='darkorange')
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626888068385/T4awiiEPo.png align="left")

#### Scatter plot

```r
plot(tr$Height, tr$Volume, col='#FDAE61', pch=19, xlab='Height', ylab=
      'Volume', main='Your title')
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626888159715/66XB0iIrVp.png align="left")

```r
plot(tr$Volume,tr$Height, col = factor(tr$Girth[1:6]), pch=19,
     xlab='Volume', ylab='Height', main='Your title')

# Legend
legend("topleft",
       legend = levels(factor(tr$Girth[1:6])),
       pch = 19,
       col = factor(levels(factor(tr$Girth[1:6]))))
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626888210328/2TWwBjZP1s.png align="left")

#### Line graph

```r
plot(tr$Height,type = "o",col = "darkgreen", xlab = "Day", ylab = "Value", 
     main = "Your title", ylim = c(0, 85), pch=18, lty=6)
lines(tr$Volume, type = "o", col = "darkblue", pch=19, lty=2)
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626888247633/DzgMIEO3r.png align="left")

#### Pie chart

```r
piedata <-c(79.814, 0.023, 16.21, 1.636, 2.318)
class <- c("Barren Land", "Water", "Built-up Area", "Tree", "Grass")
pct <- round(piedata/sum(piedata)*100, 2)
class <- paste(class, pct)
class <- paste(class,"%",sep="")
pie(piedata,labels = class, col=rainbow(5), main="LULC Types in 2013")
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640421243150/5ce2NPhW-.png align="left")

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).