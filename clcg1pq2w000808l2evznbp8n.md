---
title: "3- How to Create a Hello World App in Flask: A Step-by-Step Guide"
datePublished: Tue Jan 03 2023 09:46:12 GMT+0000 (Coordinated Universal Time)
cuid: clcg1pq2w000808l2evznbp8n
slug: 3-how-to-create-a-hello-world-app-in-flask-a-step-by-step-guide
tags: programming-blogs, python, flask, hello-world

---

Are you interested in learning how to create a simple web application using Flask? Look no further! In this step-by-step guide, we'll show you how to create a "Hello, World!" app in Flask. You'll learn how to set up your development environment, write a Python script to define your app, and run your app locally. With Flask's powerful features, you'll be well on your way to building more complex web applications in no time. So, let's get started!

1- Install Python and Flask on your computer. If you don't have them already, you can download Python from the official website and install Flask using pip.

2- Open a new Python script and import the Flask class from the flask package using the following line of code:

```python
from flask import Flask
```

3- Create a new Flask object called `app` using the following line of code:

```python
app = Flaks(__name__)
```

4- Define a function that will be called when the user visits the root URL (`/`) of the app. This function should return the string "Hello, World! This is my first from Flask". Here's an example:

```python
@app.route("/")
def hello():
        return 'Hello, World! This is my first app from Flask.'
```

5- Save the Python script as [`hello.py`](http://hello.py).

6- Open a terminal or command prompt and navigate to the directory where you saved [`hello.py`](http://hello.py).

7- Run the Python script using the following command:

```plaintext
python hello.py
```

8- Open a web browser and enter the URL [`http://localhost:5000`](http://localhost:5000) into the address bar.

9- You should see the message "Hello, World! This is my first from Flask" displayed in your web browser.

10- To stop the Flask app, press `CTRL+C` in the terminal or command prompt.

That's it! You've successfully created a Hello World app in Flask. From here, you can start building more complex web applications using Flask's powerful features.

The complete code for the Hello World app in Flask is:

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
        return 'Hello, World! This is my first app from Flask.'

if __name__ == "__main__":
        app.run(debug=True)
```

In conclusion, this step-by-step guide provides a simple and easy-to-follow process for creating a "Hello, World!" app in Flask. By following the instructions, users can quickly set up their development environment, write a Python script to define their app, and run their app locally. Flask's powerful features make it an excellent framework for building more complex web applications in the future.

\* If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content