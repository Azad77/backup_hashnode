# 3- Packages in R Programming

R packages are combinations of functions and data sets created as extensions to R. While, library in R indicates the place where the package is held.

#### Install packages
```
install.packages('ggplot2') # ggplot2 is An implementation of the grammar of graphics in R
```
To install more than one packages together
```
install.packages(c("dplyr", "devtools", "foreign")) 
#dplyr package is a grammar of data manipulation
#devtools package is a combination of package development tools
#foreign package used for read data stored by other statistical software such as Minitab, S, SAS, SPSS, and Stata.
```
You can also install packages from RGui: Packages> Install package(s)
 
and from RStudio from: Tools>Install Packages

#### Call packages
Before using any packages you have to load them using library function.
```
library(ggplot2) # to load functions from the package we have to call it.
```
#### Remove packages
You can remove any packages that you do not need:
```
remove.packages("ggplot2") # for remove a package
```

#### Update packages
Check old packages that need an update
```
old.packages()

# for update all packages
update.packages()
```
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>

To get full video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A



