---
title: "4- Importing data to R Programming"
datePublished: Fri Jul 16 2021 15:23:31 GMT+0000 (Coordinated Universal Time)
cuid: ckr6hqx3z01fbuls1h169epl6
slug: 4-importing-data-to-r-programming
tags: tutorial, data-science, r, research, programming-languages

---

Mainly, researchers use .csv, .txt, .sav, and .xlsx format files.

R has several base functions for importing data, including read.table(), read.delim(), read.csv(), and read.csv2().

To follow along with this tutorial, you can download the data from this [**link**](https://github.com/Azad77/py4researchers/blob/main/data/columbus.csv).

#### Reading a local file

```r
# To read a CSV file from a local directory:
data <- read.csv("D:/R4Researchers/columbus.csv") 
data
View(data) # to view data as a table
# The "#" symbol in R is used to write a comment.

# To read a tab-delimited file:
data1<- read.delim(file.choose())

# To read comma-separated values:
data2<-read.csv(file.choose()) # to choose file from directory

# To read semicolon-separated values:
data3 <- read.csv2(file.choose())

# To read a table with a semicolon delimiter:
table<- read.table("D:/R4Researchers/columbus.csv", header=T, sep=";")
View(table)

# To read a delimited file with a semicolon delimiter:
delim = read.delim("D:/R4Researchers/columbus.csv", header=T, sep=";")
View(delim)
```

You can also call functions from libraries to read files:

```r
library(readr)  # for read_csv
library(knitr)  # for kable
library(curl)
```

#### Reading an online file

```r
# To read a table from an online source without headers:
df <- read.table("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.txt", header = FALSE)
df

# To read a CSV file from an online source with headers:
df1 <- read.table("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.csv", header = FALSE, sep = ",")
df1

# To read a CSV file from an online source without headers:
df2 <- read.csv("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.csv", header = FALSE)
df2

# To read a CSV file from an online source with a semicolon delimiter and no headers:
df3 <- read.csv2("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.csv",  header= FALSE)
df3
```

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).