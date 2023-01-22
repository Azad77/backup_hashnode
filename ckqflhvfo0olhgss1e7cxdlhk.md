# 10- Python file handling

Python has several functions for creating, reading, updating, and deleting files.

#### open() function

For working with files the function is: open(fileName, mode) There are four different modes for opening a file:

"r" - Read - Default value. Opens a file for reading, error if the file does not exist

"a" - Append - Opens a file for appending, creates the file if it does not exist

"w" - Write - Opens a file for writing, creates the file if it does not exist

"x" - Create - Creates the specified file, returns an error if the file exists

Assume we have a txt file named data in your directory folder.

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

If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future content.

To get full video tutorial and certificate, please, enroll in the course through this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)