---
title: "4- 🌟 Pykid Modules 🌟"
datePublished: Tue Jan 02 2024 15:45:34 GMT+0000 (Coordinated Universal Time)
cuid: clqwity80000008l9ca9ka50e
slug: 4-pykid-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704210244381/522d69e2-82b5-43c6-a492-107611149ae4.jpeg
tags: programming-blogs, python, python3, coding, python-beginner

---

**Hey there, coding explorers!**

**Ready for an awesome Python adventure? Let's dive into a world of fun with code, where we can make computers do amazing things! ✨**

**First up, let's learn how to add numbers and words together by creating a simple module! 🪄**

**Imagine we have a super-special treasure chest called 'my\_**[**module.py**](http://module.py)**'. Inside, we'll store a function ✨ called 'add' that can add anything!**

**Here's how it looks:**

```python
def add(a, b):  # This line says: "Hey, here's a function named 'add' that takes two things!"
  return a + b  # This line says: "Take those two things and add them together!"
```

**For example, if you use Jupyter Notebook, create a new plain text file. Write the code in it and save this module in your directory.**

**To use our funny 'add' function, we'll open the treasure chest like this:**

```python
import my_module  # This line says: "Hey, let's bring in the 'my_module' treasure chest!"
from my_module import add  # This line says: "And let's take out the 'add' function from the chest!"
```

**Now, let's test it out!**

* **Adding numbers:**
    

```python
add(2023, 2024)  # This line says: "Use the 'add' function to add 2023 and 2024!"
# Output: 4047
```

* **Adding words:**
    

```python
add("Python", " is fun!")  # This line says: "Add 'Python' and ' is fun!' together!"
# Output: Python is fun!
```

**Wait, there's more! Let's make some animal sounds!**

**We'll use a special module called 'playsound' from 'playsound' library that we installed and another interesting function ✨ that we are creating called 'sound'!**

**Here's how it works:**

```python
from playsound import playsound  # This line says: "Bring in the 'playsound' module!"

def sound(animal): # This line says: "Here's a function named 'sound' that takes the name of an animal!"
    if animal == 'cat':
        playsound('https://www.myinstants.com/media/sounds/meow_3.mp3')  
    elif animal == 'dog':
        playsound('https://www.myinstants.com/media/sounds/dog-barking-sound-effect.mp3')  
    elif animal == 'cow':
        playsound('https://www.myinstants.com/media/sounds/cow1.mp3')  
    elif animal == 'duck':
        playsound('https://www.myinstants.com/media/sounds/duck.mp3')  
    else:
        print("Sorry, I don't know that animal's sound!") # Oops!
```

**Save these fun sounds in a 'module\_**[**sound.py**](https://bard.google.com/faq#coding)**' treasure chest! ✨**

**Now, let's hear some animals! Try 'cat', 'dog', 'duck', or 'cow'!**

```python
sound("cat") 
sound("dog") 
sound("duck") 
sound("cow") 
sound("lion") # Output: Sorry, I don't know that animal's sound!
```

**️ Built-in module**

**Python comes with several built-in modules that we can import and use in our programs.**

**We can even ask the computer what kind of system it is!**

```python
import platform
print("Your platform system is:", platform.system())  # This line says: "Tell me what kind of computer you are!"
# Output: Your platform system is: Windows 🪟
```

**Stay tuned for more exciting coding adventures!**