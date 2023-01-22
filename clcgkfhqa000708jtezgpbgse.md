# 5-Routing in Flask

Modern web applications apply meaningful URLs to assist users to come back to them easily when they can remember them.

Use the [**route()**](https://flask.palletsprojects.com/en/2.2.x/api/#flask.Flask.route) decorator to connect a function to a URL.

We can use index route ('/') and then define it:

```python
@app.route('/')
def index():
    return 'index.html'

if __name__ == "__main__":
    app.run(debug=True)
```

Or we can use hello route and then define it to return "Hello, Welcome to blog SmartRS!" directly:

```python
@app.route('/hello')
def hello():
    return 'Hello, Welcome to blog SmartRS!'

if __name__ == "__main__":
    app.run(debug=True)
```

Run the application using:

```python
python "filename".py
```