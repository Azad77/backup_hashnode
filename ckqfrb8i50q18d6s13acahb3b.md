# 11- Directories and files

os module functions:

* **os.getcwd()** obtains current working directory
    
* **os.chdir(dir)** changes current working directory to dir
    
* **os.listdir(dir=".")** list files in directory dir
    
* **os.path.exists(path)** checks whether path exists
    

Print current directory:

```python
import os # import modules
print (os.getcwd()) # e.g., "C:\Users\Azad"
```

Change the current directory to the home directory:

```python
import os, os. path # import modules
home_dir = os.path.expanduser ("~") # get home directory
print(home_dir)
os.chdir (home_dir )
```

List all files in the home directory:

```python
print(os.listdir()) 
# ['$netrc', '.anaconda', '.bash_history', '.bundle', ...]
```

If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future content.

To get full video tutorial and certificate, please, enroll in the course through this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)