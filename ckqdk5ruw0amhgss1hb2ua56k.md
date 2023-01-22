# 3- Create environments and install packages

Click on start in Microsoft. Then, select: *Anaconda Prompt (miniconda 3)*.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624697542188/DBm70TCvK.png align="left")

Your miniconda opened with the *base environment*.

List of commands in conda available [here](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)

To show packages already installed into the environment we can use:

```python
conda list
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624697127489/R3AqD_Fht3.png align="left")

To show environments of miniconda use:

```python
conda env list
```

The output is:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624697640014/bRIhe-659.png align="left")

#### Create new environment:

In this learning series, we create and use a new environment "da35" with Python version 3.5:

```python
conda create --name da35 python=3.5
```

#### Tip:

Not all Python libraries available for all Python versions. We prefer Python 3.5 for data analysis so we named it da35.

#### Go to your newly created environment "da35":

```python
conda activate da35
```

#### Tip:

(Every time when you start working inside this environment you have to activate it because libraries you installed inside it not available to base and other environments.)

#### Install packages:

We have some commands to install libraries such as "conda", "pip".

#### Tip:

(Before installing packages, you have to activate the environment that you like the packages install within.)

For instance, to install NumPy (scientific computing) and seaborn (statistical data visualization) packages we use:

```python
conda install numpy
pip install seaborn
```

If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content.

To get full video tutorial and certificate, please, enroll in the course through this link: [https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7](https://www.udemy.com/course/python-for-researchers/?referralCode=886CCF5C552567F1C4E7)