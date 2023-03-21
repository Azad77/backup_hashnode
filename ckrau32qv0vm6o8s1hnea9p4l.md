---
title: "9- Correlations in R programming"
datePublished: Mon Jul 19 2021 16:19:58 GMT+0000 (Coordinated Universal Time)
cuid: ckrau32qv0vm6o8s1hnea9p4l
slug: 9-correlations-in-r-programming
tags: tutorial, programming-blogs, r, research, programming-languages

---

Correlation measures the strength of the relationship between two variables.

*Tip: Correlation indicates association, not causation.*

Download the [**data**](https://github.com/Azad77/py4researchers/blob/main/data/LAI_factors.csv) used in this tutorial.

Load CSV data:

```r
df<- read.csv("D:\\R4Researchers\\LAI_factors.csv")
#View(df)
```

Using the cor() function:

```r
cor(df$LAI_India,df$LST_India, method="pearson") 
# -0.5035808 # inversely correlated
```

Using the cov() function:

```r
cov(df$LAI_India,df$LST_India) #Covariance
# -0.0080975
```

#### Pearson correlation coefficient (r)

```r
cor.test(df$LAI_India,df$LST_India, method="pearson")

#Pearson's product-moment correlation

#data:  df$LAI_India and df$LST_India
#t = -2.1809, df = 14, p-value = 0.04674
#alternative hypothesis: true correlation is not equal to 0
#95 percent confidence interval:
# -0.79966707 -0.01049536
#sample estimates:
#       cor 
#-0.5035808
```

**In the above output:**

* t is the t-test statistic value (t = -2.1809),
    
* df is the degrees of freedom (df = 14),
    
* p-value is the significance level of the t-test (p-value = 0.04674).
    
* [conf.int](http://conf.int) is the confidence interval of the correlation coefficient at 95% ([conf.int](http://conf.int) = \[-0.79966707, -0.01049536\]);
    
* sample estimates is the correlation coefficient (cor = -0.5035808).
    

#### Spearman's rank correlation coefficient (rho)

```r
cor.test(df$LAI_India,df$LST_India, method="spearman")  

#data:  df$LAI_India and df$LST_India
#S = 1074.7, p-value = 0.01842
#alternative hypothesis: true rho is not equal to 0
#sample estimates:
#       rho 
#-0.5803983 

#Warning message:
#In cor.test.default(df$LAI_India, df$LST_India, method = "spearman") :
#  Cannot compute exact p-value with ties
```

#### Kendall rank correlation coefficient (tau)

Kendall's tau is the same as Pearson's r and Spearman's rho

```r
cor.test(df$LAI_India,df$LST_India, method="kendall") 
#Kendall's rank correlation tau

#data:  df$LAI_India and df$LST_India
#z = -2.1475, p-value = 0.03175
#alternative hypothesis: true tau is not equal to 0
#sample estimates:
#       tau 
#-0.4109547 

#Warning message:
#In cor.test.default(df$LAI_India, df$LST_India, method = "kendall") :
#  Cannot compute exact p-value with ties
```

#### Extract correlation coefficient and p-value from correlation tests:

```r
pe<- cor.test(df$LAI_India,df$LST_India, method="pearson")
# Extract the p.value
pe$p.value
# 0.04673796

# Extract (r) correlation coefficient
pe$estimate
#cor 
#-0.5035808

spe<- cor.test(df$LAI_India,df$LST_India, method="spearman")
# Extract the p.value
spe$p.value
# 0.01841523

# Extract (rho) correlation coefficient
spe$estimate
# rho 
# -0.5803983

ken<- cor.test(df$LAI_India,df$LST_India, method="kendal")
# Extract the p.value
ken$p.value
# 0.0317547

# Extract (tau) correlation coefficient
ken$estimate
# tau 
# -0.4109547
```

#### Interpret correlation coefficient

* \-1 indicates a strong negative correlation.
    
* 0 means that there is no association between the two variables.
    
* 1 indicates a strong positive correlation.
    

Based on the previous tests, a significant negative relationship was found between land surface temperature and LAI vegetation index in India.

Create simple data and perform correlations between them:

```r
cor.test(c(1,3,5,7), c(1,3,5,7), method="pearson")
cor.test(c(1,3,5,7), c(1,3,5,7), method='spearman')
cor.test(c(1,3,5,7), c(1,3,5,7), method='kendal')
cor.test(c(1,3,5,7), c(1,3,5,1), method="pearson")
cor.test(c(1,3,5,7), c(1,3,5,1), method='spearman')
cor.test(c(1,3,5,7), c(1,3,5,1), method='kendal')
```

#### Matrix of correlations with significance levels

*Tip: Usually, statistically significant correlations should be considered.*

```r
library(Hmisc)
rcorr(as.matrix(df), type="pearson") # type can be pearson or spearman
rcorr(as.matrix(df), type='spearman') # data should be matrix
```

#### IQ score and weekly hours of watching TV

Create data:

```r
iq<- c(86, 97, 99, 100, 101, 103, 106, 110, 112, 113)
tv<- c(2, 20, 28, 27, 50, 29, 7, 17, 6, 12)
```

Correlation test:

```r
cor.test(iq, tv, method="pearson")
cor.test(iq, tv, method='spearman')
cor.test(iq, tv, method='kendal')
```

Based on all three tests, no significant correlation was found between IQ score and weekly hours of watching TV.

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).