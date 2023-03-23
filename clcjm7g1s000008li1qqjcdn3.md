---
title: "8- Create Custom Forms with Flask: A Step-by-Step Guide"
datePublished: Thu Jan 05 2023 21:43:10 GMT+0000 (Coordinated Universal Time)
cuid: clcjm7g1s000008li1qqjcdn3
slug: 8-create-custom-forms-with-flask-a-step-by-step-guide
tags: python, web-development, flask, programming-languages

---

This article provides a step-by-step guide on how to create a form using Flask, a Python web framework. You will learn how to create a form that prompts the user to answer the question "What is the most popular programming language?" with three answer fields. Additionally, you will be guided on how to create a results page and a Python script to run the form. By following the instructions provided in this article, you can easily create your own forms using Flask and obtain results based on the user's input.

Create a "form.html" file that contains a form to answer the question "What is the most popular programming language?" with three fields for answers:

```css
<form action = "http://localhost:5000/result" method = "POST">
    <p>What is the most popular programming languages?</p>
    <p>First <input type = "text" name = "First popular" /></p>
    <p>Second <input type = "text" name = "Second popular" /></p>
    <p>Third <input type = "text" name = "Third popular" /></p>
    <p><input type = "submit" value = "submit" /></p>
</form>
```

Create a "results.html" file to display the results:

```css
<html>
   <body>
      <table border = 1>
         {% for key, value in result.items() %}
            <tr>
               <th> {{ key }} </th>
               <td> {{ value }} </td>
            </tr>
         {% endfor %}
      </table>
   </body>
</html>
```

Prepare a "[form.py](http://form.py)" script:

```python
from flask import Flask, render_template, request
app = Flask(__name__)

@app.route('/')
def student():
   return render_template('form.html')

@app.route('/result',methods = ['POST', 'GET'])
def result():
   if request.method == 'POST':
      result = request.form
      return render_template("results.html",result = result)

if __name__ == '__main__':
   app.run(debug = True)
```

Run the Python script and the following page should be opened:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672955458875/07d3baf0-7efb-4f4e-b04c-1885a0037fde.png align="center")

Fill out the form and submit it to get the results page like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672955501857/60cc94d7-6810-4d1e-a7e2-008c755df245.png align="center")

This article provides instructions on how to create a form using Flask, a Python web framework. Specifically, it shows how to create a form that asks the user to answer the question "What is the most popular programming language?" and provides three fields for the answers. The article also includes instructions on how to create a results page and a Python script to run the form. By following the instructions provided in this article, users can create their own forms using Flask and obtain results based on the user's input.

\* If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content