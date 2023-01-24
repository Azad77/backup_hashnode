# 3- Create Hello World App in Flask

To create Hello World app in Flask, First, import the Flask class from the flask package:

```python
from flask import Flask
```

Then, set the app as an instance of Flask:

```python
app = Flaks(__name__)
```

Define a function index route to display “Hello, World! This is my first from Flask”:

```python
@app.route("/")
def hello():
        return 'Hello, World! This is my first app from Flask.'
```

Save a script as “[hello.py](http://hello.py)”

Then run the script with cmd using:

```python
python hello.py
```

Now open your internet browser and write:

[http://192.168.100.2:5000](http://192.168.100.2:5000)

or [localhost:5000](http://localhost:5000)

Your first web page should be opened like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672738814525/45b44d74-2484-48ab-a7ab-86b059cc93c3.png align="center")

To quit running it press CTRL+C

**The complete code is:**

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
        return 'Hello, World! This is my first app from Flask.'

if __name__ == "__main__":
        app.run(debug=True)
```

<p>* If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>