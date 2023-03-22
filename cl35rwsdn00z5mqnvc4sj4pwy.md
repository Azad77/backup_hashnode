---
title: "13- How to Create and Use Static Files in Django: A Step-by-Step Guide."
datePublished: Sat May 14 2022 11:16:43 GMT+0000 (Coordinated Universal Time)
cuid: cl35rwsdn00z5mqnvc4sj4pwy
slug: 13-how-to-create-and-use-static-files-in-django-a-step-by-step-guide
tags: django, web-development, static

---

Are you struggling to create and use static files in Django? Look no further! In this step-by-step guide, we'll walk you through the process of creating a directory for your static files, adding a stylesheet, and even incorporating images into your web page. With our easy-to-follow instructions, you'll be able to render a complete and visually appealing web page in no time. So, let's get started!

Static files are necessary files to render the complete web page such as images, JavaScript, or CSS.

First, create a directory called static in your polls directory: Sublime Text&gt; select polls&gt; right click&gt; New Folder&gt; Name it "static".

Then, create another directory called polls and within that create a file called style.css. Put the following code in that stylesheet (polls/static/polls/style.css):

```python
li a {
    color: green;
}
```

Next, add the following at the top of polls/templates/polls/index.html:

```python
{% load static %}

<link rel="stylesheet" type="text/css" href="{% static 'polls/style.css' %}">
```

Reload http://localhost:8000/polls/ and you should see that the question links are green.

Then, create an images subdirectory in the polls/static/polls/ directory. Inside this directory, put an image called background. In other words, put your image in polls/static/polls/images/background.jpg

Then, add to your stylesheet (polls/static/polls/style.css):

```python
body {
    background: white url("images/background.jpg") no-repeat;
}
```

Reload http://localhost:8000/polls/ and you should see the background loaded in the top left of the screen.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652527806616/3RrdKKVjO.png align="left")

In conclusion, this step-by-step guide provides a clear and concise explanation of how to create and use static files in Django. By following these instructions, users can easily add static files such as images, JavaScript, or CSS to their web pages and create visually appealing websites.

For more details about the Django basic tutorial, go to the main source of this tutorial: https://docs.djangoproject.com/en/4.0/intro/tutorial06/

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.