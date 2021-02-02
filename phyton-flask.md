# Flask Notları
**Flask** is a small and lightweight Python web framework that provides useful tools and features that make creating web applications in Python easier. 

Flask uses the **Jinja template** engine to dynamically build HTML pages using familiar Python concepts such as variables, loops, lists, and so on. 

## Projede Flask paketinin kurulumu
$ cd project-folder
$ pipenv install flask

## Projede kurulu Flask versiyonunu görme 
$ pipenv run python -c "import flask; print(flask.__version__)"

app = Flask(__name__)
The passed special variable __name__ holds the name of the current Python module. It’s used to tell the instance where it’s located. You need this because Flask sets up some paths behind the scenes.

@app.route('/')
It is a **decorator** that turns a regular Python function into a **Flask view function**, which converts the function’s return value into an *HTTP response* to be displayed by an HTTP client, such as a web browser. 

Flask provides a **render_template()** helper function that allows use of the Jinja template engine. 


The **url_for()** helper function to generate the appropriate location of the file. The first argument specifies that you’re linking to a static file and the second argument is the path of the file inside the static directory.

{% block title %} {% endblock %}
The block that serves as a placeholder for a title, you’ll later use it in other templates to give a custom title for each page in your application without rewriting the entire <head> section each time.

{{ url_for('index')}}
A function call that will return the URL for the index() view function. 

{% block content %} {% endblock %}
Another block that will be replaced by content depending on the child
template (templates that inherit from base.html) that will override it.

{% extends 'base.html' %} tag to inherit from the base.html template. 