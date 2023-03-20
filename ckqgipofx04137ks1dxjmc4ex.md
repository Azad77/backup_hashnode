---
title: "13- SciPy library"
datePublished: Mon Jun 28 2021 11:08:32 GMT+0000 (Coordinated Universal Time)
cuid: ckqgipofx04137ks1dxjmc4ex
slug: 13-scipy-library
tags: tutorial, python, research, learning, programming-languages

---

"SciPy" stands for "Scientific Python" and it is valuable for scientific analysis.

#### SciPy installation:

```xml
pip install SciPy
```

Examples of the functions in SciPy:

* Integration: (`scipy.integrate`)
    
* Optimization/Fitting: (`scipy.optimize`)
    
* Interpolation: (`scipy.interpolate`)
    
* Signal Processing: (`scipy.signal`)
    
* Spatial data structures and algorithms: (`scipy.spatial`)
    
* Statistics: (`scipy.stats`)
    
* Multi-dimensional image processing: (`scipy.ndimage`)
    

#### Importing from SciPy

```xml
from scipy import optimize
from scipy import spatial
# first form
from scipy import stats
# second form
from scipy.stats import distributions
```

#### T-Test

```xml
from scipy.stats import ttest_ind
x = ([1, 3, 5, 7, 11])
y = ([2, 4, 6, 8, 4])
res = ttest_ind(x, y)
print(res)
```

#### Statistical Description of Data

```python
import numpy as np
from scipy.stats import describe

x = np.random.normal(size=50)
res = describe(x)

print(res)
# DescribeResult(nobs=50, minmax=(-2.5511668761037507, 1.7772593602939395), mean=0.02937722230632724, variance=0.9754504451804601, skewness=-0.12226936632001595, kurtosis=-0.39363575297869824)
```

#### Interpolation

```python
import numpy as np
from scipy.interpolate import interp1d

x = np.array([0., 1., 5., 8., 10.])
y = np.array([0., 4., 1., 6., 8.])
f = interp1d(x, y)
print(f(3))
# 2.5
```

#### Integration

```python
import scipy.integrate
import numpy as np

f = lambda x: np.exp(x**1)
# print results
i = scipy.integrate.quad(f, 1, 2) # quad -- General-purpose integration.
print(i)
# (4.670774270471606, 5.1856011379043454e-14)
```

#### Input and Output

The [`scipy.io`](http://scipy.io) package provides multiple methods to handle inputs and outputs of multiple formats such as:

* Matlab
    
* Netcdf
    
* IDL
    
* Arff
    
* Matrix Market
    
* Wave
    

```python
import scipy.io as syio
  
# Save the mat file
n = 14031977
syio.savemat('test.mat', {'test': n})
  
# Load the mat File
matf_contents = syio.loadmat('test.mat')
print(matf_contents)
  
# printing the contents of mat file.
matf_contents = syio.whosmat('test.mat')
print(matf_contents)

#{'__header__': b'MATLAB 5.0 MAT-file Platform: nt, Created on: Mon Jun 28 16:15:59 2021', '__version__': '1.0', '__globals__': [], 'test': array([[14031977]])}
[('test', (1, 1), 'int32')]
```

> If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.
> 
> If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)