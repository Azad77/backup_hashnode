---
title: "10- The analysis of variance (ANOVA)"
datePublished: Tue Jul 20 2021 08:10:36 GMT+0000 (Coordinated Universal Time)
cuid: ckrbs1ltg0zjlz6s1h49m0155
slug: 10-the-analysis-of-variance-anova
tags: tutorial, r, research, coding, programming-languages

---

Create some data

```r
group <- rep(c('A1','A2', 'A3'), times=4)
value <- runif(12, 10, 20)
df1 <- data.frame(group, value)
df1

group <- rep(c('A1','A2', 'A3'), times=4)
value <- runif(12, 10, 20)
year <- as.factor(c(rep("2010",6), rep("2020",6)))
df2 <- data.frame(value,group,year) # dataframe
```

**Visualize data:**

```r
library(ggplot2)
ggplot(df1, aes(x = group, y = value)) +
  geom_boxplot()
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626778225836/USewmMMEW.png align="left")

#### One-way ANOVA

It is used to examine statistically significant differences between means of two or more groups.

```r
df1.anova <- aov(value ~ group, data=df1)
df1.anova
summary(df1.anova)

# extract the p-value and F value
summary(df1.anova)[[1]][1,4:5]
```

#### Interpretation of the result:

If the p-value is less than or equal to the chosen significance level (α), we reject the null hypothesis and conclude that there is a statistically significant difference between at least two group means.

If the p-value is greater than α, we fail to reject the null hypothesis and conclude that there is no statistically significant difference between group means.

The p-value of df1 is 0.9358, which is greater than 0.05. Therefore, we cannot reject the null hypothesis (means are equal) and conclude that the means are equal.

#### Two-way ANOVA

A two-way ANOVA has two independent variables. The syntax for a two-way ANOVA is:

```r
aov(dependent ~ as.factor(independent1) * as.factor(independent2), data=filename)
```

```r
df2.anova <- aov(value ~ group*year, data=df2)
summary(df2.anova)

# extract the p-value and F value:
summary(df2.anova)[[1]][1,4:5]
summary(df2.anova)[[1]][2,4:5]
summary(df2.anova)[[1]][3,4:5]
```

#### Analysis of Covariance

```r
df2.anova <- aov(value ~ group+year, data=df2)
summary(df2.anova)

# extract the p-value and F value:
summary(df2.anova)[[1]][1,4:5]
```

```r
TukeyHSD(df1.anova) #Tukey Honest Significant Differences
TukeyHSD(df2.anova)
```

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).