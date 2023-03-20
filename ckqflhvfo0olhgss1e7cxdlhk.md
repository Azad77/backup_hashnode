---
title: "10- Python file handling"
datePublished: Sun Jun 27 2021 19:38:41 GMT+0000 (Coordinated Universal Time)
cuid: ckqflhvfo0olhgss1e7cxdlhk
slug: 10-python-file-handling
tags: tutorial, python, research, learning, programming-languages

---

Python provides several functions for creating, reading, updating, and deleting files.

#### open() function

The function used for working with files is `open(fileName, mode)`. There are four different modes for opening a file:

* "r" - Read - Default value. Opens a file for reading. Throws an error if the file does not exist.
    
* "a" - Append - Opens a file for appending. Creates the file if it does not exist.
    
* "w" - Write - Opens a file for writing. Creates the file if it does not exist.
    
* "x" - Create - Creates the specified file. Throws an error if the file exists.
    

Assuming we have a text file named "data" in our directory folder:

#### read() mode

```python
file = open('data.txt', 'r')
```

Print every line in the file

```python
for each in file:
    print (each)

# This is for testing!
```

#### write() mode

```python
file = open('data.txt','w')
file.write("The write command allows us to write in a particular file. ")
file.close()
```

Open the file again:

```python
file = open('data.txt', 'r')
print(file.read())
# The write commandIt allows us to write in a particular file.
```

#### append() mode

```python
file = open('data.txt','a')
file.write("This will add this sentence.")
file.close()
```

Open the file:

```python
file = open('data.txt', 'r')
print(file.read())
# The write commandIt allows us to write in a particular file. This will add this sentence.
```

If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.

If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)