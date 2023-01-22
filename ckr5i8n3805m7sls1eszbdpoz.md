# 2- Functions in R Programming

A function is a collection of statements combined to do a specific task.

Basic syntax of an R function:

function_name <- function(arg_1, arg_2, ...) {
   Function body 
}

#### Built-in Function: 
For example: max(x) maximum of the elements of x, min(x) minimum of the elements of x, plot(x) plot of the values of x

The list of built-in functions is available at: https://cran.r-project.org/doc/contrib/Short-refcard.pdf
```
max(20, 77, 85, 12)
# 85

min(20,77, 85, 12)
# 12

a <- c(-1, -3, 0, 5, 7, 8, 4, 6.3, 10)
plot(a, col='darkgreen')
```
If a function is not available in the list of built-in functions you can use functions in packages or create it.

#### User-defined function
R user can create user-defined function.

For example: create a function to convert mile to km:
```
mile2km <- function(mile){
  km <- mile * 1.60934
  return(km)
}
mile2km(20)
# 32.1868
```
Define myMean function:
```
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
```
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
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>

To get video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A