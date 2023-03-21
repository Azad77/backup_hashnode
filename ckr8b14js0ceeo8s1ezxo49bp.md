---
title: "7- Data manipulation in R programming"
datePublished: Sat Jul 17 2021 21:51:02 GMT+0000 (Coordinated Universal Time)
cuid: ckr8b14js0ceeo8s1ezxo49bp
slug: 7-data-manipulation-in-r-programming
tags: tutorial, programming-blogs, r, research, programming-languages

---

Download the [data](https://github.com/Azad77/py4researchers/blob/main/data/columbus.csv) used in this tutorial.

Then, install and load libraries:

```r
# install.packages(c('tidyverse', 'dplyr', 'furniture'))
library(tidyverse) # for tidy up the data
```

#### Open csv data:

```r
dt <- read.csv('columbus.csv')
View(dt)
```

#### Change name of columns from capital letter to small letter

```r
names(dt) <- tolower(names(dt)) 
View(dt)
```

#### Piping, grouping and summarizing

```r
dt %>% head(5) # View fist five columns

dt %>%
  group_by(ew) %>%
  summarize(mean_crime = mean(crime, na.rm=T))
# A tibble: 2 x 2
# ew           mean_crime
# <int>      <dbl>
#   0          303.
#   1          295.
```

#### Selecting variables

```r
selected_dt <- dt %>%
  select(neig, evi, al, crime)
View(selected_dt)
```

#### Filter: Only choose observations that we need

```r
filtered_dt<-dt %>%
  filter(ew ==0) # only choose 'ew' equal to 0
View(filtered_dt)

filtered_dt1 <- dt %>%
  filter(ew==0 & open<2) # only choose 'ew' equal to 0 and 'open' smaller than 2
View(filtered_dt1)

filtered_dt2<-dt %>%
  filter(ew==0 | open<2) # "&" and "|" mean both condition
```

#### Select and filter

```r
selected_filtered_dt <- dt%>%
  select(neig, evi, al,ew,  crime)%>%
  filter(ew==1 & evi >0.3)
View(selected_filtered_dt)
```

#### Mutate

The `mutate()` function is used to add new variables.

```r
library(dplyr)
df <- tibble(x = c(1,3,5), y =c(2, 4, 6))
df %>% mutate(z = y / x)
df %>% mutate(z = x * y, .after = x)

df %>%
  select(x, y) %>%
  mutate(
    z = y * 2,
    z_squared = z * z
  )
```

#### Reshaping

```r
library(furniture)
```

Create a wide data frame:

```r
df_wide <- data.frame('ID'=c('a', 'b', 'c', 'd'),
                      'time1'=c(1:4),
                      'time2'=c(3,5,6,9)) # create wide data frame

df_wide
#  ID time1 time2
#1  a     1     3
#2  b     2     5
#3  c     3     6
#4  d     4     9
```

Convert wide to long:

```r
df_long<-long(df_wide,
              c('time1', 'time2'),
              v.names='value')
df_long
#    ID time value
#a.1  a    1     1
#b.1  b    1     2
#c.1  c    1     3
#d.1  d    1     4
#a.2  a    2     3
#b.2  b    2     5
#c.2  c    2     6
#d.2  d    2     9
```

Convert long to wide:

```r
df_wide<-wide(df_long,
               v.names=c('value'),
               timevar='time') # convert long to wide data frame

df_wide
#    ID value.1 value.2
#a.1  a       1       3
#b.1  b       2       5
#c.1  c       3       6
#d.1  d       4       9
```

#### Joining (merging)

Create data:

```r
df1 <- data.frame(ID=1:3,
                  x1=c('a1', 'a2', 'a3'),
                  stringsAsFactors = F)

df2<- data.frame(ID=2:4,
                 x2 = c('z1', 'z2', 'z3'),
                 stringsAsFactors = F)
df3<- data.frame(ID=3:5,
                 x2=c('a1', 'a2', 'a3'),
                 x3=c('z1', 'z2', 'z3'),
                 stringsAsFactors = F)
```

`inner_join()` merges the variables of both data frames, but retains only rows with a shared ID.

```r
inner_join(df1, df2, by='ID')
```

`left_join()` retains all rows of the data table, which is inserted first into the function.

```r
left_join(df1, df2, by='ID')
```

`right_join()` function retains all rows of the data on the right

```r
right_join(df1, df2, by='ID')

full_join(df1, df2, by='ID') #retains the most data of all the join functions.
semi_join(df1, df2, by='ID') #return all rows from x where there are matching values in y, keeping just columns from x
anti_join(df1, df2, by='ID')#return all rows from x where there are not matching values in y, keeping just columns from x.
```

Join multiple data frames

```r
full_join(df1, df2, by='ID') %>%
  full_join(.,df3, by='ID') 

# join by multiple columns:
full_join(df2, df3, by=c('ID', 'x2'))
```

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).