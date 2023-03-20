---
title: "4- Install and run jupyter notebook platform"
datePublished: Sat Jun 26 2021 10:09:17 GMT+0000 (Coordinated Universal Time)
cuid: ckqdlpsbj0b0xgss19y015yf8
slug: 4-install-and-run-jupyter-notebook-platform
tags: tutorial, python, research, learning, programming-languages

---

To write and execute Python code, you can use many platforms, such as "Jupyter Notebook," "Spyder," and "Google Colab." In this learning series, we use the "Jupyter Notebook" platform.

The Jupyter Notebook is a free web application for creating and sharing documents that contain live code, equations, visualizations, and narrative text.

Firstly, we activate our environment:

```python
conda activate da35
```

Then, we install jupyter notebook:

```python
conda install jupyter
```

To confirm that Jupyter Notebook is installed, look at the list of installed packages:

```python
conda list
```

To start running it, inside Anaconda Prompt write:

```python
jupyter notebook
```

This window should be opened:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624702799444/EWdM0RDcs.png align="left")

#### Install a collection of various different notebook extensions for Jupyter:

```python
conda install -c conda-forge jupyter_contrib_nbextensions
```

In the opened Jupyter Notebook window, click on "Nbextentions", then select any necessary extensions.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624712028463/s5J0sqDSn.png align="left")

To close jupyter notebook, inside conda mrompt, use control and c.

```python
ctrl+c
```

If you find this content helpful, please consider [SUBSCRIBING](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA) to my channel for future updates.

If you would like to get the full video tutorial and a certificate, you can enroll in the course by following this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)