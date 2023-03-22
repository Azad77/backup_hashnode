---
title: "8- How to Create an Admin User and Display the Poll App in Django"
datePublished: Sun May 08 2022 09:10:05 GMT+0000 (Coordinated Universal Time)
cuid: cl2x2qty806n7u5nv860f9isq
slug: 8-how-to-create-an-admin-user-and-display-the-poll-app-in-django
tags: django, web-development

---

Learn how to create an admin user in Django with this step-by-step guide. Follow the instructions below to set up a superuser account and access the admin login screen. You'll also discover how to display the poll app on the admin index page by editing the appropriate file. Whether you're new to Django or looking to expand your skills, this tutorial will help you get started.

To create an admin user, run the following command:

```
pythonCopy codepython manage.py createsuperuser
```

Enter any username, for example, Azad, and press enter. Then enter your email address, for example, [**azad977@gmail.com**](mailto:azad977@gmail.com). Next, create a password. You should see the following message:

```
pythonCopy codeSuperuser created successfully.
```

Now, open a web browser and go to [**http://127.0.0.1:8000/admin/**](http://127.0.0.1:8000/admin/). You should see the admin login screen. Try logging in with the superuser account you created in the previous step.

To display the poll app on the admin index page, open the polls/admin.py file and edit it to look like this:

```
pythonCopy codefrom django.contrib import admin
from .models import Question

admin.site.register(Question)
```

If you find this content helpful, please consider [**subscribing**](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.