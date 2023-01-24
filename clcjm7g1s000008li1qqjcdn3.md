# 8- Forms in Flask

Create “form.html” file that contains a form to answer a question: “What is the most popular programming language?” and three fields for answers:

```css
<form action = "http://localhost:5000/result" method = "POST">
    <p>What is the most popular programming languages?</p>
    <p>First <input type = "text" name = "First popular" /></p>
    <p>Second <input type = "text" name = "Second popular" /></p>
    <p>Third <input type = "text" name = "Third popular" /></p>
    <p><input type = "submit" value = "submit" /></p>
</form>
```

And create a “results.html” file to return results:

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

And now prepare a “[form.py](http://form.py)” script:

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

<p>* If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>