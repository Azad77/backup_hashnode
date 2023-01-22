# 4- Templates in Flask

Each template contains HTML which is the standard language of the web. The template files will be stored in the templates directory inside the project folder. Flask uses the Jinja template library to render templates.

Firstly, create a directory for your project templates using cmd:

```python
(venv) mkdir C:\Users\gardi\flask-tutorial\templates
```

For example, let's create an HTML file and write Hello World of Programming! inside it in blue color:

```python
<html>
    <body>
        <h1 style='color:blue'>Hello World of Programming!</h1>
    </body>
</html>
```

Now let's create a python script and save it as hello1.py.

At the beginning of the script we have to import Flask and render\_template:

```python
from flask import Flask, render_template
```

Then create app:

```python
app = Flask(__name__)
```

We define route **hello** to return **hello.html** template using render\_template:

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

Inside cmd run the Python script with command:

```python
python hello1.py
```

Open your localhost:

[http://localhost:5000/](http://localhost:5000/)

A web page like the following should be opened:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672755906922/00feb1b3-b838-492f-b75f-2370cb3defa2.png align="center")