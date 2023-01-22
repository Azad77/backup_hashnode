# 13- Create static files

Static files are necessary files to render the complete web page such as images, JavaScript, or CSS.

First, create a directory called static in your polls directory: Sublime Text> select polls> right click> New Folder> Name it "static".

Then, create another directory called polls and within that create a file called style.css.
Put the following code in that stylesheet (polls/static/polls/style.css):
```
li a {
    color: green;
}
```
Next, add the following at the top of polls/templates/polls/index.html:
```
{% load static %}

<link rel="stylesheet" type="text/css" href="{% static 'polls/style.css' %}">
```
Reload http://localhost:8000/polls/ and you should see that the question links are green.

Then, create an images subdirectory in the polls/static/polls/ directory. Inside this directory, put an image called background. In other words, put your image in polls/static/polls/images/background.jpg

Then, add to your stylesheet (polls/static/polls/style.css):
```
body {
    background: white url("images/background.jpg") no-repeat;
}
```

Reload http://localhost:8000/polls/ and you should see the background loaded in the top left of the screen.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652527806616/3RrdKKVjO.png align="left")

For more details about the Django basic tutorial, go to the main source of this tutorial:
https://docs.djangoproject.com/en/4.0/intro/tutorial06/


