---
title: "2- Functions in R Programming"
datePublished: Thu Jul 15 2021 22:49:31 GMT+0000 (Coordinated Universal Time)
cuid: ckr5i8n3805m7sls1eszbdpoz
slug: 2-functions-in-r-programming
tags: tutorial, functions, r, research, programming-languages

---

A function is a collection of statements combined to perform a specific task.

The basic syntax of an R function is:

function\_name &lt;- function(arg\_1, arg\_2, ...) { Function body }

#### Built-in Functions:

For example, `max(x)` returns the maximum value of the elements in `x`, `min(x)` returns the minimum value of the elements in `x`, and `plot(x)` creates a plot of the values in `x`.

A list of built-in functions is available at: [**https://cran.r-project.org/doc/contrib/Short-refcard.pdf**](https://cran.r-project.org/doc/contrib/Short-refcard.pdf)

```r
max(20, 77, 85, 12)
# 85

min(20,77, 85, 12)
# 12

a <- c(-1, -3, 0, 5, 7, 8, 4, 6.3, 10)
plot(a, col='darkgreen')
```

If a function is not available in the list of built-in functions, you can use functions in packages or create your own.

#### User-defined Functions:

R users can create user-defined functions. For example, you can create a function to convert miles to kilometers:

```r
mile2km <- function(mile){
  km <- mile * 1.60934
  return(km)
}
mile2km(20)
# 32.1868
```

Define a `myMean` function:

```r
myMean <- function(n){
  mean = sum(n)/length(n)
  return(mean)
}

myMean(a)
# 4.033333

myMean(c(10, 50, 20))
# 26.6667
```

Create a function without an argument:

```r
multiply_function <- function(){
  for (i in -5:5){
    print(i*i)
  }
}
multiply_function()
'''
[1] 25
[1] 16
[1] 9
[1] 4
[1] 1
[1] 0
[1] 1
[1] 4
[1] 9
[1] 16
[1] 25
'''
```

If you enjoy the content, please consider subscribing to my [**YouTube channel**](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [**Udemy course**](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).