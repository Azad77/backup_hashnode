---
title: "12- Scientific computation using NumPy library"
datePublished: Sun Jun 27 2021 22:26:39 GMT+0000 (Coordinated Universal Time)
cuid: ckqfrhvsz0p8fgss19ccaev5k
slug: 12-scientific-computation-using-numpy-library
tags: tutorial, python, programming-languages, numpy

---

In Python, NumPy (Numerical Python) is the essential package for scientific computation. It is used for working with arrays. An array in NumPy is very fast compared to traditional Python lists. It can also be used for computing Pearson’s correlation coefficient and generating random numbers.

## Installation of NumPy:

```python
pip install numpy
```

## Import NumPy

```python
import numpy as np
```

## Arrays in NumPy

### 0D array

```python
da = np.array(1977)
print(da)
# 1977
```

### 1D array

```python
da = np.array([3, 5, 7, 9, 12])
type(da)
# numpy.ndarray
da.max() # calculate max of array
# 12
da.min() # calculate min of array
# 3
da.mean() # calculate mean of array
#  7.2
da.sum() # calculate sum of array
# 36
np.median(da)
# 7.0
```

### 2D array

````python
da = np.array([[22, 15, 33], [24, 25, 16]])
da
# array([[22, 15, 33],
#           [24, 25, 16]])
```
````

### 3D array

```python
da = np.array([[[1, 3, 5], [2, 4, 6]], [[1, 3, 5], [2, 4, 6]]])
da
# array([[[1, 3, 5],
#          [2, 4, 6]],

#          [[1, 3, 5],
#          [2, 4, 6]]])
print('shape of array:', da.shape)
# shape of array: (3, 3)
```

## Data type of array

```python
da = np.array([1, 2, 3, 4])

print(da.dtype)
# int32
```

## Accessing and Slicing Arrays

```python
da = np.array([5, 9, 7, 11])
da[0] # first number
# 5
da[2] # third number
# 7
da = np.arange(50)
da[1:10]
# array([1, 2, 3, 4, 5, 6, 7, 8, 9])
```

## Operations

```python
da = np.array([1, 2, 3, 4])
da + 1
# array([2, 3, 4, 5])
da * da
# array([ 1,  4,  9, 16])
```

## Array manipulations

```python
da = np.arange(20).reshape(4, 5)
da
# array([[ 0,  1,  2,  3,  4],
#           [ 5,  6,  7,  8,  9],
#           [10, 11, 12, 13, 14],
#           [15, 16, 17, 18, 19]])
```

## Random numbers in NumPy

Random means that numbers cannot be anticipated logically.

```python
from numpy import random
rn = random.randint(100)
print(rn)
# 56
rn = random.randint(100)
print(rn)
# 43
rn = random.randint(100)
print(rn)
# 85
rn = random.rand(3) # float
print(rn)
# [0.75700426 0.97003262 0.16064961]
```

## NaN values

NaN means "Not a Number". If we multiply a NaN value by another value, we get NaN.

To calculate the sum, we can use np.nansum instead of np.sum in order to find the sum and avoid NaN:

```python
x = np.array([12,np.nan,31,56, 88, np.nan])
x
# array([12., nan, 31., 56., 88., nan])
np.nansum(x)
# 187.0
np.nanmean(x)
# 46.75
np.nanmax(x)
# 88.0
np.nanmin(x)
# 12.0
```

## Mask in NumPy

Download the data  [here](https://github.com/Azad77/py4researchers/blob/main/data/munich_temp_with_bad_data.TXT)

```python
t=np.loadtxt('D:\Python\Python_for_Researchers\munich_temp_with_bad_data.txt')
np.min(t)
# -99.0
keep = (t > -30) & (t < 50) # Mask with conditions temperature should lower than 50 and higher than -30
t1 = t[keep]
np.max(t1)
# 27.6667
np.mean(t1)
# 8.933222104668378
np.min(t1)
# -16.7778
```

## Calculate correlation coefficient in NumPy

```python
x = np.array([2, 4, 2, 8])
y = np.array([2, 3, 1, 8])
np.corrcoef(x, y)
# array([[1.        , 0.98552746],
#     [0.98552746, 1.        ]])

r = np.corrcoef(x, y)
r
r[0, 1]
# 0.9855274566525744
r[1, 0]
# 0.9855274566525744
r[0, 0]
# 1
r[1, 1]
# 1
```

If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.

If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)