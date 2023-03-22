---
title: "5- Step-by-Step Guide to Setting Up a Database for Your Poll Project"
datePublished: Sun May 08 2022 00:27:18 GMT+0000 (Coordinated Universal Time)
cuid: cl2wk2j0d05ext4nvff3g88mk
slug: 5-step-by-step-guide-to-setting-up-a-database-for-your-poll-project
tags: django, web-development

---

Are you planning to create a poll project and wondering how to set up the database? Look no further! In this article, we provide you with a step-by-step guide on how to properly set up your Poll Project's database. From changing the TIME\_ZONE to running the necessary commands, we've got you covered. By following these simple steps, you'll have your database up and running in no time. So, let's get started!

Open the PollProject/settings.py file. By default, the configuration uses SQLite.

Inside PollProject/settings.py, set the TIME\_ZONE to your timezone. For example, in my case, it is: `TIME_ZONE = 'Asia/Baghdad'`.

To create the tables in the database, run the following command:

```python
py manage.py migrate
```

The migrate command looks at the INSTALLED\_APPS setting and creates any necessary database tables according to the database settings in the PollProject/settings.py file.

The guide includes changing the TIME\_ZONE to the user's timezone and running the migrate command to create the necessary database tables. Following these steps will ensure that the Poll Project's database is properly set up and ready for use.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.