# 9- Correlations in R programming

Correlation measures the intensity of the relationship between the two variables.

*Tip: Correlation implies association, not causation.*

Download  [data](https://github.com/Azad77/py4researchers/blob/main/data/LAI_factors.csv)  used in this tutorial.

Load csv data:
```
df<- read.csv("D:\\R4Researchers\\LAI_factors.csv")
#View(df)
```
Using cor() function:
```
cor(df$LAI_India,df$LST_India, method="pearson") 
# -0.5035808 # inversely correlated
```
Using cov() function:
```
cov(df$LAI_India,df$LST_India) #Covariance
# -0.0080975
```
#### Pearson correlation coefficient (r)
```
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

- t is the t-test statistic value (t = -2.1809),
- df is the degrees of freedom (df= 14),
- p-value is the significance level of the t-test (p-value =0.04674).
- conf.int is the confidence interval of the correlation coefficient at 95% (conf.int = [-0.79966707, -0.01049536]);
- sample estimates is the correlation coefficient (cor = -0.5035808)

#### Spearman's rank correlation coefficient (rho)
```
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
#### Kendall rank correlation coefficient (tau). 

Kendall's tau is the same as for Pearson's r and Spearman's rho
```
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
#### Extract correlation coefficient and p.value from correlation tests:
```
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
- -1 indicates a strong negative correlation.
- 0 means that there is no association between the two variables.
- 1 indicates a strong positive correlation

Based on previous tests, a significant relationship was found between land surface temperature and lai vegetation index in India.

Create simple data and perform correlations between them:
```
cor.test(c(1,3,5,7), c(1,3,5,7), method="pearson")
cor.test(c(1,3,5,7), c(1,3,5,7), method='spearman')
cor.test(c(1,3,5,7), c(1,3,5,7), method='kendal')
cor.test(c(1,3,5,7), c(1,3,5,1), method="pearson")
cor.test(c(1,3,5,7), c(1,3,5,1), method='spearman')
cor.test(c(1,3,5,7), c(1,3,5,1), method='kendal')
```
#### Matrix of correlations with significance levels
*Tip: usually, correlations to be considered should be statistically significant.*
```
library(Hmisc)
rcorr(as.matrix(df), type="pearson") # type can be pearson or spearman
rcorr(as.matrix(df), type='spearman') # data should be matrix
```
#### IQ score and hours weekly watching tv 
Create data:
```
iq<- c(86, 97, 99, 100, 101, 103, 106, 110, 112, 113)
tv<- c(2, 20, 28, 27, 50, 29, 7, 17, 6, 12)
```
Correlation test:
```
cor.test(iq, tv, method="pearson")
cor.test(iq, tv, method='spearman')
cor.test(iq, tv, method='kendal')
```
Based on all three tests no significant correlation was found between IQ score and TV watching.

<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>

To get full video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A
