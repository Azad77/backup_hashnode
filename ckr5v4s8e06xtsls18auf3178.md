---
title: "3- Packages in R Programming"
datePublished: Fri Jul 16 2021 04:50:27 GMT+0000 (Coordinated Universal Time)
cuid: ckr5v4s8e06xtsls18auf3178
slug: 3-packages-in-r-programming
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707126065195/d21486c8-63e5-4b20-a732-d71b7344d6d6.gif
tags: tutorials, r, research, package, programming-languages

---

R packages are combinations of functions and datasets created as extensions to R. The `library` function in R is used to indicate the location where the package is stored.

#### Installing Packages

To install a package, use the `install.packages` function. For example, to install the `ggplot2` package, you can use the following code:

```r
install.packages('ggplot2') # ggplot2 is An implementation of the grammar of graphics in R
```

To install multiple packages at once, use the following code:

```r
install.packages(c("dplyr", "devtools", "foreign")) 
# dplyr is a package for grammar of data manipulation.
# devtools is a package containing package development tools.
# foreign is a package used to read data stored by other statistical software such as Minitab, S, SAS, SPSS, and Stata.
```

You can also install packages from the RGui by going to Packages &gt; Install package(s), and from RStudio by going to Tools &gt; Install Packages.

#### Loading Packages

Before using any packages, you have to load them using the `library` function. For example, to load functions from the `ggplot2` package, use the following code:

```r
library(ggplot2)
```

#### Removing Packages

To remove a package that you do not need, use the `remove.packages` function. For example, to remove the `ggplot2` package, use the following code:

```r
remove.packages("ggplot2")
```

#### Updating Packages

To check for outdated packages that need to be updated, use the `old.packages` function. To update all packages, use the `update.packages` function. For example:

```r
old.packages()

update.packages()
```

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).