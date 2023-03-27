---
title: "21- How to Add a New Menu Item to QGIS Software with PyQGIS"
datePublished: Fri Jun 25 2021 08:27:33 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2n384000le7s1ftdm2syd
slug: 21-how-to-add-a-new-menu-item-to-qgis-software-with-pyqgis
tags: tutorial, programming-blogs, python, learning, gis

---

Learn how to customize your QGIS software and improve your workflow by adding a new menu item with PyQGIS. This step-by-step guide explains how to import the `webbrowser` module, define a function that opens a specified website in a web browser, create a `QAction` instance, and add it to the help menu. With this new menu item, you can quickly access a website of your choice directly from QGIS. Follow the instructions in this article to enhance your QGIS experience and streamline your work.

Import the `webbrowser` module:

```python
import webbrowser
```

  
Define a function that opens the specified website in a web browser:

```python
def open_website(): webbrowser.open('https://smartrs.blog/series/pyqgis-basics')
```

Create a `QAction` instance with the label "Go to: Introduction to PyQGIS":

```python
website_action = QAction('Go to: Introduction to PyQGIS')
```

Connect the `triggered` signal of the `QAction` to the `open_website()` function:

```python
website_action.triggered.connect(open_website)
```

Add a separator to the help menu:

```python
iface.helpMenu().addSeparator()
```

Add the `website_action` `QAction` to the help menu:

```python
iface.helpMenu().addAction(website_action)
```

Now, from the "Help" menu, click on the newly created item "Go to: Introduction to PyQGIS" to open the website.

Here's the overall code:

```python
# Import the webbrowser module
import webbrowser

# Define a function that opens the specified website in a web browser
def open_website():
    webbrowser.open('https://smartrs.blog/series/pyqgis-basics')

# Create a QAction instance with the label "Go to: Introduction to PyQGIS"
website_action = QAction('Go to: Introduction to PyQGIS')

# Connect the triggered signal of the QAction to the open_website() function
website_action.triggered.connect(open_website)

# Add a separator to the help menu
iface.helpMenu().addSeparator()

# Add the website_action QAction to the help menu
iface.helpMenu().addAction(website_action)
```

In conclusion, this article provides a step-by-step guide on how to add a new menu item to the QGIS software with PyQGIS. By following the instructions provided in the article, users can add a new menu item to the help menu, which will open a specified website in a web browser. This article is helpful for users who want to customize their QGIS software and improve their workflow.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content