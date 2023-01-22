# 11- Student's t.test in R programming

The t-test uses to examine the difference of means of two groups of data.

Default in t-test assumes unequal variance and applies the Welsh df modification

Create data:
```
group_a<- c(86, 97, 99, 100, 101, 103, 106, 110, 112, 113)
group_b<- c(50, 100, 98, 95, 90, 105, 110, 95, 100, 112)
```
#### One sample t-test
```
t.test(group_a) 
```
#### Independent (unpaired) t-test
Used for an independent data set that is distributed identically. For example, randomly divided 200 samples of treatment cases to 100 as treatment group and 100 as a control group.
```
tt<-t.test(group_a, group_b)
tt
t.test(x=c(2, 4, 6), y = c(2, 4, 6))
t.test(x=c(-2, -4, -6), y = c(2,4,6))
t.test(x=c(2, 4, 6), y = c(4, 8, 12))
```

#### Paired t-test
Used for equal pairs of similar units, or one group of units that has been measured twice, for example, blood pressure before and after treatment.
```
df <- data.frame(Name = c("Jon", "Ali", "Aviar", "Didar", "Shilan", "Tom"),
                 first_exam = c(70, 41, 85, 58, 46, 90),
                 second_exam = c(45, 80, 55, 95, 85, 80)
)

t.test(df$first_exam, df$second_exam, paired=TRUE)
```
#### Extract p-value and the value of the t-statistic
```
names(tt)
t.test(group_a, group_b)$p.value 

tt$p.value
tt$statistic 
# or 
tt[['statistic']]
```
#### Interpret the result
In the output:

- t is the t-test statistic value,
- df is the degrees of freedom 
- p-value is the significance level of the t-test 
- confidence interval is the confidence interval of the mean at 95% 
- sample estimates is the mean value of the sample

 
If p-value >0.05, indicates that means of groups of data are not significantly different.

<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>

To get full video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A