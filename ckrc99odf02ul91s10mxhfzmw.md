---
title: "11- Student's t.test in R programming"
datePublished: Tue Jul 20 2021 16:12:46 GMT+0000 (Coordinated Universal Time)
cuid: ckrc99odf02ul91s10mxhfzmw
slug: 11-students-ttest-in-r-programming
tags: programming-blogs, r, research, coding, programming-languages

---

The t-test is used to examine the difference in means between two groups of data. By default, the t-test assumes unequal variance and applies the Welsh df modification.

To create data for the t-test in R, you can use the following code:

```r
group_a<- c(86, 97, 99, 100, 101, 103, 106, 110, 112, 113)
group_b<- c(50, 100, 98, 95, 90, 105, 110, 95, 100, 112)
```

#### One-sample t-test

You can perform a one-sample t-test using the following code:

```r
t.test(group_a)
```

#### Independent (unpaired) t-test

This test is used for an independent data set that is identically distributed, for example, when you randomly divide 200 samples of treatment cases into 100 as the treatment group and 100 as the control group. You can use the following code:

```r
tt<-t.test(group_a, group_b)
tt
t.test(x=c(2, 4, 6), y = c(2, 4, 6))
t.test(x=c(-2, -4, -6), y = c(2,4,6))
t.test(x=c(2, 4, 6), y = c(4, 8, 12))
```

#### Paired t-test

The paired t-test is used for equal pairs of similar units, or for one group of units that has been measured twice, for example, blood pressure before and after treatment. You can use the following code:

```r
df <- data.frame(Name = c("Jon", "Ali", "Aviar", "Didar", "Shilan", "Tom"),
                 first_exam = c(70, 41, 85, 58, 46, 90),
                 second_exam = c(45, 80, 55, 95, 85, 80)
)

t.test(df$first_exam, df$second_exam, paired=TRUE)
```

#### Extracting p-value and the value of the t-statistic

To extract the p-value and the value of the t-statistic, you can use the following code:

```r
names(tt)
t.test(group_a, group_b)$p.value 

tt$p.value
tt$statistic 
# or 
tt[['statistic']]
```

#### Interpreting the result

In the output:

* t is the t-test statistic value,
    
* df is the degrees of freedom,
    
* p-value is the significance level of the t-test,
    
* confidence interval is the confidence interval of the mean at 95%,
    
* sample estimates are the mean values of the sample.
    

If the p-value is greater than 0.05, it indicates that the means of the groups of data are not significantly different.

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).