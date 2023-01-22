# 6- Static files in Flask

Static files are necessary files to render the complete web page such as images, JavaScript, or CSS.

### **Create new folders:**

First, create a directory called static in your project directory using cmd:

```python
mkdir C:\Users\gardi\flask-tutorial\static
```

Inside static folder create a "style" folder for styling the page and "img" folder for images using cmd:

```python
mkdir C:\Users\gardi\flask-tutorial\static\style
```

```python
mkdir C:\Users\gardi\flask-tutorial\static\img
```

### Create Python, HTML, and CSS files

Create a Python file to render index template and save it as "static.py":

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route("/")
def index():
   return render_template("index.html")

if name == '__main__':
   app.run(debug = True)
```

**Then create index.html**

```python
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>CS304: Flask</title>
    <link rel="stylesheet" type="text/css" 
          href="{{ url_for('static', filename='style.css') }}">
</head>
<body>

    <h1>Using Static File</h1>

    </body>
</html>
 
```

This sentence code defines the link of the style file:

```python
    <link rel="stylesheet" type="text/css" 
          href="{{ url_for('static', filename='style.css') }}"> 
```

### **Create css style file:**

Create a css file inside "static\\style" folder for styling your pages and save it as "style.css":

```css
html { font-family: sans-serif; background: #eee; padding: 1rem; }
body { max-width: 960px; margin: 0 auto; background: white; }
h1 { font-family: serif; color: #377ba8; margin: 1rem 0; }
a { color: #377ba8; }
hr { border: none; border-top: 1px solid lightgray; }
nav { background: lightgray; display: flex; align-items: center; padding: 0 0.5rem; }
nav h1 { flex: auto; margin: 0; }
nav h1 a { text-decoration: none; padding: 0.25rem 0.5rem; }
nav ul  { display: flex; list-style: none; margin: 0; padding: 0; }
nav ul li a, nav ul li span, header .action { display: block; padding: 0.5rem; }
.content { padding: 0 1rem 1rem; }
.content > header { border-bottom: 1px solid lightgray; display: flex; align-items: flex-end; }
.content > header h1 { flex: auto; margin: 1rem 0 0.25rem 0; }
.flash { margin: 1em 0; padding: 1em; background: #cae6f6; border: 1px solid #377ba8; }
.post > header { display: flex; align-items: flex-end; font-size: 0.85em; }
.post > header > div:first-of-type { flex: auto; }
.post > header h1 { font-size: 1.5em; margin-bottom: 0; }
.post .about { color: slategray; font-style: italic; }
.post .body { white-space: pre-line; }
.content:last-child { margin-bottom: 0; }
.content form { margin: 1em 0; display: flex; flex-direction: column; }
.content label { font-weight: bold; margin-bottom: 0.5em; }
.content input, .content textarea { margin-bottom: 1em; }
.content textarea { min-height: 12em; resize: vertical; }
input.danger { color: #cc2f2e; }
input[type=submit] { align-self: start; min-width: 10em; }
```

Run the "static.py" script inside cmd:

```css
python static.py
```

Now open your internet browser and write:

[**localhost:5000**](http://localhost:5000)

Your styled web page should be opened like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672913501318/a0212502-ca25-4ee0-9ee5-2c0c52f90065.png align="center")

### Load background image

Inside img directory, put an image and name it "background.jpg".

To insert the background image add the following code to the index template:

```css
<img src= "{{ url_for("static", filename= "img/background.jpg") }}">
```

The index file is now should be looks like this:

```css
<html lang="en">

<head>

    <meta charset="utf-8">

    <title>CS304: Flask</title>

    <link rel="stylesheet" type="text/css"

          href="{{ url_for('static', filename='style.css') }}">

</head>

<body>

<img src= "{{ url_for("static", filename= "img/background.jpg") }}">

    </body>

</html>
```

Now reload opened web page to inset the background image looks like that:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672912977561/423df376-ee8b-4e22-924a-a63526607496.png align="center")