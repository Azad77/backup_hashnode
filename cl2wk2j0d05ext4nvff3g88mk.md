---
title: "5- Database setup"
datePublished: Sun May 08 2022 00:27:18 GMT+0000 (Coordinated Universal Time)
cuid: cl2wk2j0d05ext4nvff3g88mk
slug: 5-database-setup
tags: django, web-development

---

Open the PollProject/settings.py file. By default, the configuration uses SQLite.

Inside PollProject/settings.py, set the TIME\_ZONE to your timezone. For example, in my case, it is: `TIME_ZONE = 'Asia/Baghdad'`.

To create the tables in the database, run the following command:

```python
py manage.py migrate
```

The migrate command looks at the INSTALLED\_APPS setting and creates any necessary database tables according to the database settings in the PollProject/settings.py file.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.