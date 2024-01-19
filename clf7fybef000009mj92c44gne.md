---
title: "Step-by-Step Guide to Packaging and Publishing Python Projects on PyPI"
datePublished: Mon Mar 13 2023 23:13:59 GMT+0000 (Coordinated Universal Time)
cuid: clf7fybef000009mj92c44gne
slug: step-by-step-guide-to-packaging-and-publishing-python-projects-on-pypi
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704217863699/c3d513ed-4846-4008-92b6-6e92815ad856.jpeg
tags: python, package, pypi

---

Are you looking for a step-by-step guide to packaging and publishing your Python projects on PyPI? Look no further! This comprehensive guide will walk you through everything you need to know, from organizing your files and creating a package to uploading it to PyPI for easy installation using pip. With clear instructions and helpful examples, you'll be able to share your Python projects with the world in no time.

In this guide, a straightforward project called "smartrs" is utilized. However, you can substitute your name instead to generate a distinct package name that won't clash with packages uploaded by other individuals who are also following this tutorial.

**Step 1: Organizing Your Project Files:**

Make the subsequent arrangement of files and folders on your computer's storage device:

```python
packaging/
└── src/
    └── smartrs/
        ├── __init__.py
        └── example.py
```

It's recommended that the name of the directory holding Python files matches the project name. This makes configuration easier and clearer for package users. To import the directory as a package, an empty init.py file is necessary. An example.py module within the package can contain the package's logic such as functions, classes, and constants. You can add the necessary content to the example.py file:

```python
def add_ten(number):
     return number + 10
```

**Step 2: Generating Necessary Files:**

To prepare the project for distribution, you need to include certain files in the package. Once you've completed this step, the structure of the project will resemble the following:

```python
packaging/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── smartrs/
│       ├── __init__.py
│       └── example.py
└── tests/
```

To set up a directory for testing purposes, create a folder called "**tests/**" and leave it empty for the time being.

To specify which "backend" tool to use for creating distribution packages for your project, you need to create a file called "**pyproject.toml**". This file is used by "frontend" build tools like pip and build to identify the appropriate "backend" tool.

Open `pyproject.toml` and enter:

```python
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```

Open `pyproject.toml` and enter the following content. Change the `name` to include the name of your package:

```python
[project]
name = "smartrs"
version = "0.0.1"
authors = [
  { name="Example Author", email="author@example.com" },
]
description = "A small example package"
readme = "README.md"
requires-python = ">=3.7"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
"Homepage" = "https://github.com/pypa/sampleproject"
"Bug Tracker" = "https://github.com/pypa/sampleproject/issues"
```

**Step 3: Preparing README and License:**

**Prepare README.md:**

Access the [README.md](http://README.md) file and input the subsequent information:

```python
# Example Package

This is a simple example package. You can use
[Github-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.
```

**Prepare a LICENSE:**

Including a license is a crucial requirement for every package uploaded to the Python Package Index. To add a license, you can open the LICENSE file and input the text of your chosen license. An example of a commonly used license is the MIT license:

```python
Copyright (c) 2018 The Python Packaging Authority

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

**Step 4: Creating Distribution Archives:**

The subsequent action is to create distribution packages for the software package. These archives are produced and then uploaded to the Python Package Index, where they can be installed using pip.

Execute this command in the directory where the **pyproject.toml** file is located, inside the "packaging" folder, you can use shift+right click&gt; Git Bash Here:

```python
python -m build
```

The execution of this instruction is expected to produce a significant amount of written information, and upon its completion, it should create two files within the dist directory.

```python
dist/
├── smartrs-0.0.1-py3-none-any.whl
└── smartrs-0.0.1.tar.gz
```

The `tar.gz` file is a [source distribution](https://packaging.python.org/en/latest/glossary/#term-Source-Distribution-or-sdist) whereas the `.whl` file is a [built distribution](https://packaging.python.org/en/latest/glossary/#term-Built-Distribution).

**Step 5: Uploading to PyPI:**

To begin, your initial task is to create a PyPI account by completing the registration process.

After completing your registration, you will be able to utilize twine for uploading distribution packages. To do so, it is necessary to install Twine:

```python
pip install --upgrade twine
```

After installing, execute Twine to upload all the files stored in the dist folder.

```python
twine upload --verbose dist/*
# username: __token__
# password: pypi-AgEIcHlwaS5vcmc..... (your token)
```

You will be prompted for a username and password for your PyPI account.

To use an API token:

* Set your username to `__token__`
    
* Set your password to the token value, including the `pypi-` prefix
    

Once uploaded, your package should be viewable on PyPI; for example:

[https://pypi.org/project/smartrs/0.0.1/](https://pypi.org/project/smartrs/0.0.1/)

To install the package you have uploaded, you may utilize pip and confirm its functionality:

```python
pip install smartrs==0.0.1
```

```python
Successfully built smartrs 
Installing collected packages: smartrs 
Successfully installed smartrs-0.0.1
```

**Step 6: Verifying Installation:**

One way to verify that the package was installed properly is by importing it and running a test.

```python
from smartrs import example
example.add_ten(5)
```

Well done, you have successfully packaged and shared a Python project!

In conclusion, packaging and publishing Python projects on PyPI is an important and necessary step for sharing your code with the world. With the help of this step-by-step guide, you can easily organize your files, create a package, and upload it to PyPI for easy installation using pip. By following the instructions provided and utilizing helpful tools like Twine, you can successfully publish your Python projects and make them accessible to others. Remember to include a license and a README file to provide important information about your project, and don't hesitate to consult additional resources for more information and guidance.

For more information visit:

* [Packaging Python Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects/)
    
* [Python Packages](https://www.tutorialsteacher.com/python/python-package)
    
* [How to create a Python package and publish it on PyPI in 5 minutes](https://www.youtube.com/watch?v=EIwLZiTuYoA)