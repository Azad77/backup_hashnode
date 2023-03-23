---
title: "4- Creating Templates in Flask: A Beginner's Guide"
datePublished: Tue Jan 03 2023 14:27:09 GMT+0000 (Coordinated Universal Time)
cuid: clcgbr0n6000308k5e40tfie2
slug: 4-creating-templates-in-flask-a-beginners-guide
tags: blogging, python, web-development, flask

---

If you're new to Flask and want to learn how to create templates using HTML, this beginner's guide is for you. Flask is a micro web framework written in Python that allows you to build web applications quickly and easily. Templates are a key component of web development, and Flask uses the Jinja template library to render them. In this guide, you'll learn how to create a templates directory for your Flask project, write an HTML file, create a Python script, and use Flask's render\_template function to display your template on a web page.

Now, let's get started. Firstly, create a directory for your project templates using cmd:

```python
(venv) mkdir C:\Users\gardi\flask-tutorial\templates
```

This command will create a new directory called "templates" in your project folder. All of your HTML templates will be stored in this directory.

For example, let's create an HTML file and write "Hello World of Programming!" inside it in blue color:

```python
<html>
    <body>
        <h1 style='color:blue'>Hello World of Programming!</h1>
    </body>
</html>
```

Now let's create a Python script and save it as "[hello1.py](http://hello1.py)".

At the beginning of the script, we have to import Flask and render\_template:

```python
from flask import Flask, render_template
```

Then create the app:

```python
app = Flask(__name__)
```

We define a route "hello" to return the "hello.html" template using render\_template:

```python
@app.route("/")
def hello():
        return render_template('hello.html')
```

Finally, we run the app:

```python
if __name__ == "__main__":
        app.run(debug=True)
```

Inside cmd run the Python script with the command:

```python
python hello1.py
```

Open your localhost:

[**http://localhost:5000/**](http://localhost:5000/)

A web page like the following should be opened:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672755906922/00feb1b3-b838-492f-b75f-2370cb3defa2.png align="center")

In conclusion, this beginner's guide provides a clear and concise explanation of how to create templates in Flask using HTML and the Jinja template library. By following the steps outlined in this guide, even those new to Flask can easily create a templates directory for their project, write an HTML file, create a Python script, and use Flask's render\_template function to display their template on a web page. With this knowledge, developers can quickly and easily build web applications using Flask.

\* If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content