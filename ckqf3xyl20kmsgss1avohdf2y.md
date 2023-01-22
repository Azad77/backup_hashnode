# 9- Modules in Python

In the modules, we can use a set of functions without being required to redefine them. Then, from a group of related modules, we can create a package. Create a simple module:

```python
def hi(name):
    print("Hello, " + name)
```

Save it as "module1" in your directory.

Use the module:

```python
import module1
module1.hi("Ali")
# Hello, Ali
```

#### Built-in module

We can import various built-in modules in Python.

```python
import platform
print(platform.system())
# Windows
```

Import module from a package:

```python
import matplotlib.pyplot as plt
```

If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future content.

To get full video tutorial and certificate, please, enroll in the course through this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)