---
title: "5- Exporting data from R programming"
datePublished: Fri Jul 16 2021 16:24:31 GMT+0000 (Coordinated Universal Time)
cuid: ckr6jxdft02dhths1hijn7qd9
slug: 5-exporting-data-from-r-programming
tags: tutorial, r, research, programming-languages, learn-coding

---

#### Create data:

```r
data <- c(1977, 1979, 2013, 2014,'', 2015)
```

#### Save data as comma-separated CSV format:

```r
write.csv(data, 'created_data.csv')
```

#### Save as semicolon-separated CSV file:

```r
write.csv2(data, file='data_semicolon.csv')
```

#### Save data as text file:

```r
write.table(data, file= 'data.txt', sep = '\t', row.names=T) # \t is tab
```

#### Save as RData:

If we have objects a, b, c, d, and e, we can save them as RData and reload them in a new session:

```r
a<- c(5)
b<- c(-1)
c<- c(15)
d<- c(55)
e<- c('NA')
save(a, b, c, d, e, file='test.RData') # Rdata is used to save multiple R objects
load('C:\\Users\\Azad\\Documents\\test.RData')
```

#### Save an object to RDS file:

```r
saveRDS(data, 'firstData.rds')
# Restore it
rds_data <- readRDS("firstData.rds") # Rds is used to save a single R object
```

#### Save workspace:

The workspace is your current R working environment and includes any user-defined objects (vectors, matrices, data frames, lists, functions).

```r
save.image(file='workspace_2021.RData')
load('workspace_2021.RData')
```

#### Compressing and saving files:

```r
write.csv(data, file = bzfile('data_ziped.csv.bz2'))
```

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).