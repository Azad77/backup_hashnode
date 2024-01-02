---
title: "3- Create environments and install packages"
datePublished: Sat Jun 26 2021 09:25:44 GMT+0000 (Coordinated Universal Time)
cuid: ckqdk5ruw0amhgss1hb2ua56k
slug: 3-create-environments-and-install-packages
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704217268858/9e653d7f-7566-46fa-b988-ceaeee022a53.jpeg
tags: tutorial, python, research, learning, programming-languages

---

Click on "Start" in Microsoft. Then, select "*Anaconda Prompt (miniconda 3)*".

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624697542188/DBm70TCvK.png align="left")

Your miniconda should open with the "*base environment*".

The list of available commands in conda is [**here**](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf).

To show the packages already installed in the environment, use:

```python
conda list
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624697127489/R3AqD_Fht3.png align="left")

To show the environments in miniconda, use:

```python
conda env list
```

The output should be:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624697640014/bRIhe-659.png align="left")

#### Creating a new environment

In this learning series, we will create and use a new environment called "da35" with Python version 3.5:

```python
conda create --name da35 python=3.5
```

#### Tip:

Not all Python libraries are available for all Python versions. We prefer Python 3.5 for data analysis, so we named it da35.

#### Go to your newly created environment "da35":

```python
conda activate da35
```

#### Tip:

Every time you start working inside this environment, you need to activate it because the libraries you installed inside it are not available in the base and other environments.

#### Install packages:

There are different commands to install libraries, such as "conda" and "pip".

#### Tip:

Before installing packages, activate the environment where you want to install the packages.

For instance, to install NumPy (for scientific computing) and seaborn (for statistical data visualization) packages, use:

```python
conda install numpy
pip install seaborn
```

If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.

If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)