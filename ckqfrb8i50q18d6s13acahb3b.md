---
title: "11- Directories and files"
datePublished: Sun Jun 27 2021 22:21:29 GMT+0000 (Coordinated Universal Time)
cuid: ckqfrb8i50q18d6s13acahb3b
slug: 11-directories-and-files
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704015479775/875891c8-9b6c-45ea-b3e0-2c6d27db4a84.png
tags: tutorial, python, research, learning, programming-languages

---

os module functions:

* * **os.getcwd()**: obtains the current working directory.
        
    * **os.chdir(dir)**: changes the current working directory to dir.
        
    * **os.listdir(dir=".")**: lists files in the directory dir.
        
    * **os.path.exists(path)**: checks whether the path exists.
        
    
    To print the current directory:
    

```python
import os # import modules
print (os.getcwd()) # e.g., "C:\Users\Azad"
```

To change the current directory to the home directory:

```python
import os, os. path # import modules
home_dir = os.path.expanduser ("~") # get home directory
print(home_dir)
os.chdir (home_dir )
```

To list all files in the home directory:

```python
print(os.listdir()) 
# ['$netrc', '.anaconda', '.bash_history', '.bundle', ...]
```

If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.

If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)