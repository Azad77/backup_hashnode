---
title: "2- Creating a project"
datePublished: Sat May 07 2022 19:15:25 GMT+0000 (Coordinated Universal Time)
cuid: cl2w8xfow04vcu5nv0ck5febe
slug: 2-creating-a-project
tags: django, web-development, python-projects

---

First, navigate to the directory where you want to store your code (e.g., "Desktop") using the command line:

```xml
cd desktop
```

Next, create a new Django project named "PollProject" with the following command:

```xml
django-admin startproject PollProject
```

Navigate to the newly created project directory:

```xml
cd PollProject
```

To verify that your Django project is working properly, run the following command:

```xml
py manage.py runserver
```

Finally, open your web browser and go to "[**http://127.0.0.1:8000/**](http://127.0.0.1:8000/)". If everything is working correctly, you should see a "Congratulations!" page:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651950771773/b_H86m3tJ.png align="left")

If you find this content helpful, please consider [**subscribing**](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.