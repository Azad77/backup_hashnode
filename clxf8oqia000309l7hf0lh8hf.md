---
title: "Comparison of Different ML Classifiers on Synthetic Dataset"
datePublished: Fri Jun 14 2024 22:07:26 GMT+0000 (Coordinated Universal Time)
cuid: clxf8oqia000309l7hf0lh8hf
slug: comparison-of-different-ml-classifiers-on-synthetic-dataset
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724479581908/4009db5c-a8b3-4113-b38d-d9e0ae97ee58.png
tags: python, machine-learning, classification

---

Hello everyone! In this lesson, we will compare different machine learning classifiers on a synthetic dataset using Python.

First, let's import the necessary **libraries.** We will use `matplotlib` for plotting, `numpy` for numerical operations, and `sklearn` for machine learning functions.

```python
# Importing necessary libraries
import matplotlib.pyplot as plt  # Library for plotting
import numpy as np  # Library for numerical operations
from sklearn.ensemble import RandomForestClassifier
from matplotlib.colors import ListedColormap  # For customizing colormap
from sklearn.datasets import make_classification  # For generating synthetic datasets
from sklearn.inspection import DecisionBoundaryDisplay  # For displaying decision boundaries
from sklearn.model_selection import train_test_split  # For splitting dataset into train and test sets
from sklearn.neighbors import KNeighborsClassifier  # k-Nearest Neighbors classifier
from sklearn.neural_network import MLPClassifier  # Multi-layer Perceptron classifier
from sklearn.pipeline import make_pipeline  # For creating a pipeline of transformers and estimators
from sklearn.preprocessing import StandardScaler  # For standardizing features
from sklearn.tree import DecisionTreeClassifier  # Decision Tree classifier
```

Next, we will create a **list of classifier** names. These are "Nearest Neighbors," "Decision Tree," "Random Forest," and "Neural Net."

We will also create a list of classifiers. For this, we will use k-Nearest Neighbors with k=3, Decision Tree with a max depth of 5, Random Forest with a max depth of 5 and 10 estimators, and a Multi-layer Perceptron.

```python
# List of classifier names
names = [
    "Nearest Neighbors",
    "Decision Tree",
    "Random Forest",
    "Neural Net"
]

# List of classifiers
classifiers = [
    KNeighborsClassifier(3),  # k-Nearest Neighbors with k=3
    DecisionTreeClassifier(max_depth=5, random_state=42),  # Decision Tree Classifier with max depth of 5
    RandomForestClassifier(max_depth=5, n_estimators=10, max_features=1, random_state=42),  # Random Forest Classifier
    MLPClassifier(alpha=1, max_iter=1000, random_state=42)  # Multi-layer Perceptron Classifier
]
```

Now, let's **generate a complex synthetic dataset** with 1000 samples and 20 features. We will add some noise to the dataset to make it more interesting.

```python
# Generating a complex synthetic dataset
X, y = make_classification(
    n_samples=1000,  # Number of samples in the dataset
    n_features=20,  # Number of features in the dataset
    n_redundant=2,  # Number of redundant features
    n_informative=10,  # Number of informative features
    n_clusters_per_class=2,  # Number of clusters per class
    random_state=1  # Random seed for reproducibility
)
rng = np.random.RandomState(2)
X += 2 * rng.uniform(size=X.shape)  # Adding noise to the dataset 
```

We will only use the first two features for visualization. We will **split the dataset** into training and testing sets, with 40% of the data used for testing.

```python
# Using only the first two features for visualization
X = X[:, :2]

# Splitting the dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.4, random_state=42
)
```

Next, we will **create a figure for plotting the data**. We will set the range for the x and y axes based on the dataset values. We will plot the dataset using red and blue colors for different classes.

We will then iterate over the classifiers. For each classifier, we will create a pipeline with a standard scaler and the classifier. We will fit the classifier on the training data and calculate the accuracy score on the test data.

We will plot the decision boundaries for each classifier. We will also plot the training and testing points on the same plot.

Finally, we will adjust the layout and display the plot.

```python
# Creating a figure for plotting
figure = plt.figure(figsize=(18, 6))
x_min, x_max = X[:, 0].min() - 0.5, X[:, 0].max() + 0.5
y_min, y_max = X[:, 1].min() - 0.5, X[:, 1].max() + 0.5

# Plotting the dataset
cm = plt.cm.RdBu
cm_bright = ListedColormap(["#FF0000", "#0000FF"])
ax = plt.subplot(1, len(classifiers) + 1, 1)
ax.set_title("Input data")
ax.scatter(X_train[:, 0], X_train[:, 1], c=y_train, cmap=cm_bright, edgecolors="k")
ax.scatter(X_test[:, 0], X_test[:, 1], c=y_test, cmap=cm_bright, alpha=0.6, edgecolors="k")
ax.set_xlim(x_min, x_max)
ax.set_ylim(y_min, y_max)
ax.set_xticks(())
ax.set_yticks(())

# Iterate over classifiers
for i, (name, clf) in enumerate(zip(names, classifiers), start=2):
    ax = plt.subplot(1, len(classifiers) + 1, i)

    # Constructing a pipeline with standard scaler and the classifier
    clf = make_pipeline(StandardScaler(), clf)
    # Fitting the classifier
    clf.fit(X_train, y_train)
    # Calculating the accuracy score
    score = clf.score(X_test, y_test)
    # Plotting decision boundaries
    DecisionBoundaryDisplay.from_estimator(
        clf, X, cmap=cm, alpha=0.8, ax=ax, eps=0.5
    )

    # Plotting training and testing points
    ax.scatter(X_train[:, 0], X_train[:, 1], c=y_train, cmap=cm_bright, edgecolors="k")
    ax.scatter(X_test[:, 0], X_test[:, 1], c=y_test, cmap=cm_bright, edgecolors="k", alpha=0.6)

    ax.set_xlim(x_min, x_max)
    ax.set_ylim(y_min, y_max)
    ax.set_xticks(())
    ax.set_yticks(())
    ax.set_title(name)
    # Adding accuracy score as text on each subplot
    ax.text(x_max - 0.3, y_min + 0.3, ("%.2f" % score).lstrip("0"), size=15, horizontalalignment="right")

# Adjusting layout and displaying the plot
plt.tight_layout()
plt.show()
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718402720856/8b5326d6-652d-4cef-97f5-b14d03bc2571.png align="center")

**Analyses results:** Our analysis of the classifier performance reveals that the Neural Net emerged victorious, achieving an impressive accuracy of 81% on the test data. This suggests that the Neural Net was more adept at capturing the intricate patterns within the data compared to the other classifiers.

Following closely behind was the Decision Tree classifier, boasting an accuracy of 80%. Meanwhile, the Nearest Neighbors and Random Forest classifiers achieved slightly lower accuracies of 76% and 79%, respectively.