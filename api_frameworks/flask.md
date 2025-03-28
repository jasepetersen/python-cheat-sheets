# Flask Cheat Sheet

## Installation

```bash
pip install flask
```

## Basic App

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, World!"
```

## Run the App

```bash
flask run
```

Or:

```python
if __name__ == "__main__":
    app.run(debug=True)
```

## Route Parameters

```python
@app.route("/user/<username>")
def show_user(username):
    return f"User: {username}"
```

## Query Parameters

```python
from flask import request

@app.route("/search")
def search():
    q = request.args.get("q")
    return f"Query: {q}"
```

## HTTP Methods

```python
@app.route("/submit", methods=["GET", "POST"])
def submit():
    if request.method == "POST":
        return "Form submitted"
    return "Submit form"
```

## JSON Request and Response

```python
from flask import jsonify, request

@app.route("/json", methods=["POST"])
def json_example():
    data = request.get_json()
    return jsonify(data)
```

## Templates

```python
from flask import render_template

@app.route("/hello/<name>")
def hello(name):
    return render_template("hello.html", name=name)
```

## Redirect and URL Building

```python
from flask import redirect, url_for

@app.route("/redirect-me")
def redirect_me():
    return redirect(url_for("home"))
```

## Error Handling

```python
@app.errorhandler(404)
def not_found(e):
    return "Not Found", 404
```

## Sessions

```python
from flask import session

app.secret_key = "your-secret-key"

@app.route("/set/")
def set_session():
    session["user"] = "Alice"
    return "Session set"

@app.route("/get/")
def get_session():
    return session.get("user", "Not set")
```

## Static Files

Place files in `static/` and access like:

```html
<img src="{{ url_for('static', filename='logo.png') }}">
```

## Form Data

```python
@app.route("/form", methods=["POST"])
def form():
    name = request.form["name"]
    return f"Hello {name}"
```

## File Upload

```python
from flask import request
from werkzeug.utils import secure_filename

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["file"]
    filename = secure_filename(file.filename)
    file.save(f"./uploads/{filename}")
    return "File uploaded"
```
