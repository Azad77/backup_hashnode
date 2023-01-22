# 4- Install and run jupyter notebook platform

To write and execute python codes you can use many platforms such as "jupyter notebook", "Spyder" and "Google Colab". In this learning series we use "jupyter notebook" platform.

The Jupyter Notebook is a free web application for creating and sharing documents that contain live code, equations, visualizations, and narrative text.

Firstly, we activate our environment:

```python
conda activate da35
```

Then, we install jupyter notebook:

```python
conda install jupyter
```

Look at the list of installed packaged to confirm jupyter notebook is installed:

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

To close jupyter notebook, inside conda mrompt use control and c.

```python
ctrl+c
```

If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content.

To get full video tutorial and certificate, please, enroll in the course through this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)