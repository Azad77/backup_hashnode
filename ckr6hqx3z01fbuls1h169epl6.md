# 4- Importing data to R Programming

Mainly researchers use .csv, .txt, .sav, and .xlxs format files.

R base functions for importing data: read.table(), read.delim(), read.csv(), read.csv2()

Download  [data](https://github.com/Azad77/py4researchers/blob/main/data/columbus.csv)  used in this tutorial.
#### Reading a local file
```
data <- read.csv("D:/R4Researchers/columbus.csv") 
data
View(data) # to view data as table
# symbol in R used to write comment.

# For reading delimited tab separated file:
data1<- read.delim(file.choose())

# Read comma (",") separated values:
data2<-read.csv(file.choose()) # to choose file from directory

# Read semicolon (";") separated values:
data3 <- read.csv2(file.choose())

table<- read.table("D:/R4Researchers/columbus.csv", header=T, sep=";")
View(table)

delim = read.delim("D:/R4Researchers/columbus.csv", header=T, sep=";")
View(delim)
```

Call function from libraries to read files:

```
library(readr)  # for read_csv
library(knitr)  # for kable
library(curl)
```
#### Reading an online file 
```
df <- read.table("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.txt", header = FALSE)
df

df1 <- read.table("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.csv", header = FALSE, sep = ",")
df1

df2 <- read.csv("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.csv", header = FALSE)
df2

df3 <- read.csv2("https://s3.amazonaws.com/assets.datacamp.com/blog_assets/test.csv",  header= FALSE)
df3
```
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>

To get full video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A