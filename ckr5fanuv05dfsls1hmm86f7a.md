# 1- Data types in R

%%[adsense]
We recommend to you install and use the latest version of [R](https://cran.r-project.org/bin/windows/base/) and   [RStudio IDE](https://www.rstudio.com/products/rstudio/download/). 

The common R data types for research are numeric, factor, and character.

#### Numeric
```
a <- c(-1, -3, 0, 5, 7, 8, 4, 6.3, 10) 
```

- "<-" is assignment operator
- "c()" function combines values into a vector or list.
- We can get help about functions by using question mark and the name of the function, for example:
```
?c()
```
#### Factor
```
drink_vector <- (c('milk', 'water', 'juice'))
drink_vector
# [1] "milk"  "water" "juice"
drink_factor <- factor(drink_vector)
drink_factor
# [1] milk  water juice
# Levels: juice milk water
```
#### Character
```
d<-c('Hellow world', 'R is fun!')
d
# [1] "Hellow world" "R is fun!" 
```
#### Create dataframe:
```
a <- c(1, 3, 5, 7)
b <- c(2, 4, 6, 8)
df<-data.frame(a, b)
df
```
Add a column with $ operator
```
df$new_column <- c(1, 2, 3, 4)
df
```
Add a column with cbind function
```
df <- cbind(df, new_new_column = c('a', 'b', 'c', 'd'))
df
```
View df as table in RStudio
```
view(df)
```
Get names of dataframe
```
names(df)
```
Display the Structure of the dataframe
```
str(df)
```
Summary
```
summary(df)
```
<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>
To get full video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A


