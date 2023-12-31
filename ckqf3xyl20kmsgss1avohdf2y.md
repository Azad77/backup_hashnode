---
title: "9- Modules in Python"
datePublished: Sun Jun 27 2021 11:27:18 GMT+0000 (Coordinated Universal Time)
cuid: ckqf3xyl20kmsgss1avohdf2y
slug: 9-modules-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704016074398/13c314d3-c733-4ef0-b6c0-938173783828.png
tags: tutorial, python, research, learning, programming-languages

---

In Python, modules allow us to use a set of functions without the need to redefine them. We can group related modules to create a package. Here is an example of a simple module:

```python
def hi(name):
    print("Hello, " + name)
```

Save this module as "module1" in your directory.

To use the module, simply import it as follows:

```python
import module1
module1.hi("Ali")
# Hello, Ali
```

#### Built-in module

Python comes with several built-in modules that we can import and use in our programs. For instance, we can use the "platform" module to get information about the operating system:

```python
import platform
print(platform.system())
# Windows
```

We can also import modules from a package:

```python
import matplotlib.pyplot as plt
```

If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.

If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)