---
title: "1- Data types in R"
datePublished: Thu Jul 15 2021 21:27:07 GMT+0000 (Coordinated Universal Time)
cuid: ckr5fanuv05dfsls1hmm86f7a
slug: 1-data-types-in-r
tags: tutorial, programming-blogs, r, research, learn-coding

---

We recommend installing and using the latest versions of [R](https://cran.r-project.org/bin/windows/base/) and [RStudio IDE](https://www.rstudio.com/products/rstudio/download/).

The common R data types for research are numeric, factor, and character.

#### Numeric

```python
a <- c(-1, -3, 0, 5, 7, 8, 4, 6.3, 10)
```

* "&lt;-" is the assignment operator.
    
* "c()" function combines values into a vector or list.
    
* We can get help about functions by using the question mark followed by the name of the function, for example:
    

```python
?c()
```

#### Factor

```python
drink_vector <- (c('milk', 'water', 'juice'))
drink_vector
# [1] "milk"  "water" "juice"
drink_factor <- factor(drink_vector)
drink_factor
# [1] milk  water juice
# Levels: juice milk water
```

#### Character

```python
d<-c('Hellow world', 'R is fun!')
d
# [1] "Hellow world" "R is fun!"
```

#### Create a dataframe:

```python
a <- c(1, 3, 5, 7)
b <- c(2, 4, 6, 8)
df<-data.frame(a, b)
df
```

Add a column with the $ operator:

```python
df$new_column <- c(1, 2, 3, 4)
df
```

Add a column with the cbind function:

```python
df <- cbind(df, new_new_column = c('a', 'b', 'c', 'd'))
df
```

View the dataframe as a table in RStudio:

```python
view(df)
```

Get the names of the dataframe:

```python
names(df)
```

Display the structure of the dataframe:

```python
str(df)
```

Summary

```python
summary(df)
```

> If you enjoy the content, please consider subscribing to my [**YouTube channel**](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.
> 
> To access video tutorials and receive a certificate, enroll in my [**Udemy course**](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).