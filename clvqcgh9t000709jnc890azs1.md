---
title: "Introduction to Deep Learning in R Programming"
datePublished: Fri May 03 2024 07:19:03 GMT+0000 (Coordinated Universal Time)
cuid: clvqcgh9t000709jnc890azs1
slug: introduction-to-deep-learning-in-r-programming
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724478147508/89a13172-9d4c-4982-8b99-fa88ed28508c.png
tags: artificial-intelligence, deeplearning, rprogramming

---

Hi everyone, today we're diving into some R programming with neural networks. First, we need to make sure we have all the tools we need, so we load up some **libraries** that help us with data and building neural networks. Then, we're going to work with a classic dataset called Iris.

```r
# Install devtools
# install.packages("devtools")
# Install keras
# devtools::install_github("rstudio/keras")

# Load necessary libraries
library(tidyverse)   # For data manipulation
library(keras3)      # For building neural networks
library(tensorflow)  # Backend for Keras
library(datasets)    # Provides sample datasets
```

The **Iris dataset** has different types of flowers, and we want to teach our computer to recognize them based on their features. But computers like numbers, not flower names, so we convert the flower types into numbers.

Next, we **split our dataset** into two parts: one for teaching our computer (the training set) and one for testing how well it learned (the test set). We make sure both sets have a good mix of flower types.

```r
# Load Iris dataset
data(iris)


# Convert class labels to numeric format (0, 1, 2)
iris[,5] <- as.numeric(iris[,5]) - 1

# Convert iris dataframe to a matrix
iris <- as.matrix(iris)

# Set dimension names to NULL
dimnames(iris) <- NULL


# Determine sample size and split the dataset into training and test sets
ind <- sample(2, nrow(iris), replace=TRUE, prob=c(0.67, 0.33))

# Select rows for training set where ind is 1
iris.training <- iris[ind==1, 1:4]

# Select rows for test set where ind is 2
iris.test <- iris[ind==2, 1:4]

# Split the class attribute for training set
iris.trainingtarget <- iris[ind==1, 5]  # Select the class labels corresponding to the training set samples

# Split the class attribute for test set
iris.testtarget <- iris[ind==2, 5]  # Select the class labels corresponding to the test set samples
```

Now, here's where things get interesting. We want our computer to understand the different flower types, but it's not as simple as saying 'this is a setosa' or 'this is a versicolor.' We need to speak the computer's language, which is 0s and 1s.

So, we do something called **'one-hot encoding.'** It's like translating flower names into a special code that the computer can understand. Each type of flower gets its own code, like a secret language.

```r
# One hot encode training target values:
# Convert the class labels of the training set into a one-hot encoded format.
# One-hot encoding transforms categorical labels into a binary matrix where each column represents a unique class, 
# and the column corresponding to the class label is marked as 1 while others are 0.
iris.trainLabels <- to_categorical(iris.trainingtarget)

# One hot encode test target values:
# Similar to the above, convert the class labels of the test set into a one-hot encoded format.
iris.testLabels <- to_categorical(iris.testtarget)
```

Just to be sure everything's going smoothly, we **take a quick peek at our translated test** set to make sure our codes look right.

```r
# Print out the one-hot encoded test labels to double-check the result
print(iris.testLabels)
```

## Model 1

Now, we're going to learn about building a neural network using R programming language. Let's start with Model 1.

First, we **construct our model**. Think of a model as a blueprint for our neural network. We **initialize** our model by creating an empty container for layers.

```r
## Constructing the Model
# Initialize a sequential model
model <- keras_model_sequential()
```

Then, we **add layers** to our model. Each layer processes data in a different way. In our first layer, we add what's called a dense layer. This layer has 8 units, which are like small processing units. We use an activation function called ReLU, which helps the network learn complex patterns in the data. Since this is our first layer, we also specify the input shape, which is the number of features in our data, in this case, 4 features from the Iris dataset.

Next, we add another dense layer. This time, it has 3 units. We use a different activation function called softmax. Softmax is handy for classification tasks because it gives us probabilities for each class.

```r
# Add layers to the model
# Add a dense (fully connected) layer with 8 units/neurons, ReLU activation function, and input shape of (4,)
# The input shape (4,) corresponds to the number of features in the input data (4 features in Iris dataset)
# The ReLU activation function introduces non-linearity to the network
# The first layer requires specification of input shape since it's the first layer in the model
model %>% 
  layer_dense(units = 8, activation = 'relu', input_shape = c(4)) %>% 
  # Add another dense layer with 3 units/neurons, softmax activation function
  # Softmax activation is commonly used for multi-class classification tasks
  # It ensures that the output values are between 0 and 1 and sum up to 1, representing class probabilities
  layer_dense(units = 3, activation = 'softmax')
```

Once our model is constructed, we check its **summary** to see its architecture, including the number of layers and parameters.

```r
# Print a summary of the model architecture, including the number of layers, 
# the type of layers, and the number of parameters in each layer.
summary(model)
```

After that, we **compile our model**. Compiling means configuring the model for training. We specify the loss function, optimizer, and metrics. The loss function tells the model how wrong it is during training. We use categorical crossentropy since we have multiple classes. The optimizer updates the model based on the data it sees and the loss function. We choose Adam optimizer, which is quite popular.

Lastly, we want to **see how accurate our model** is during training, so we use accuracy as our metric.

```r
# Get model configuration
get_config(model)
# This line retrieves the configuration of the neural network model. 
# It provides details about the architecture, such as the number of layers, 
# the activation functions used, the number of units in each layer, etc.


# Get layer configuration
# Retrieve information about the first layer in the model
get_layer(model, index = 1)

# List the model's layers
model$layers  # This line lists all the layers in the model

# List the input tensors
model$inputs # This line retrieves the list of input tensors for the neural network model. 

# List the output tensors
model$outputs # This line retrieves the list of output tensors for the neural network model
# Compile And Fit The Model:
# Compile the model
model %>% compile(
  loss = 'categorical_crossentropy',  # Specify the loss function for categorical classification
  optimizer = 'adam',                  # Specify the optimizer algorithm (Adam)
  metrics = 'accuracy'                 # Specify the metric to evaluate model performance (accuracy)
)
```

Then, we **train our model** using the fit function. We provide it with our training data and labels, specify the number of epochs (training iterations), batch size (number of samples the model sees before updating), and a validation split (portion of training data used for validation).

We can **visualize how our model** learns over epochs by plotting its training history. We plot both the loss and accuracy for both training and validation data. This helps us understand if our model is improving over time.

```r
# Store the fitting history in `history` 
history <- model %>% fit(
  iris.training,           # Training data features (input)
  iris.trainLabels,        # Training data labels (output)
  epochs = 200,            # Number of training epochs (iterations over the entire dataset)
  batch_size = 5,          # Number of samples per gradient update
  validation_split = 0.2   # Fraction of the training data to be used as validation data
)


# Plot the history
plot(history) # Plotting the training history provides visual insights into the model's performance over each epoch.

# Visualize The Model Training History:
# Plot the model loss of the training data
plot(history$metrics$loss, main="Model Loss", xlab = "epoch", ylab="loss", col="blue", type="l")
# This command creates a plot of the model's loss on the training data over epochs.

# Plot the model loss of the test data
lines(history$metrics$val_loss, col="green")

# Add legend
legend("topright", c("train","test"), col=c("blue", "green"), lty=c(1,1))

# Plot the accuracy of the training data 
plot(history$metrics$acc, main="Model Accuracy", xlab = "epoch", ylab="accuracy", col="blue", type="l")

# Plot the accuracy of the validation data
lines(history$metrics$val_acc, col="green")

# Add Legend
legend("bottomright", c("train","test"), col=c("blue", "green"), lty=c(1,1))
```

Lastly, we **evaluate our model** on the test data to see how well it performs on unseen data. We **print out** the evaluation score to see its performance.

```r
# Evaluate on test data and labels
score <- model %>% evaluate(iris.test, iris.testLabels, batch_size = 128)
# Print the score
print(score)
```

And that's Model 1! We've built our first neural network in R and trained it on the Iris dataset. In the next section, we'll explore more models and dive deeper into neural networks. Stay tuned!"

## Model 2

Now, we're going to **fine-tune our model** by adding more layers. Let's dive into it.

First, we **initialize our sequential model**, which is like a blank canvas waiting for us to add layers. We'll call it model2.

```r
# Initialize the sequential model
model2 <- keras_model_sequential()
```

Now, let's add layers to our model. We start by adding a dense layer with 8 units. Think of units as little computational blocks. We use the ReLU activation function, which helps the network learn complex patterns. Since this is our first layer, we need to specify the input shape, which is (4,). This means our data has 4 features.

Next, we add another dense layer, this time with 5 units and ReLU activation function. This layer automatically receives input from the previous one, so we don't need to specify the input shape again.

Finally, we add the output layer. This layer has 3 units because we have 3 classes in the Iris dataset. We use the softmax activation function here to get probabilities for each class.

```r
# Add layers to model2:
# Add a dense layer with 8 units and ReLU activation function.
# Input shape is specified as (4,), indicating the input features.
# This layer connects to the input layer implicitly.
# Initialize the sequential model

model2 %>% 
  # Add a dense layer with 8 units and ReLU activation function.
  # Input shape is specified as (4,), indicating the input features.
  # This layer connects to the input layer implicitly.
  layer_dense(units = 8, activation = 'relu', input_shape = c(4)) %>% 
  
  # Add another dense layer with 5 units and ReLU activation function.
  # This layer automatically receives input from the previous layer.
  layer_dense(units = 5, activation = 'relu') %>% 
  
  # Add the output layer with 3 units and softmax activation function.
  # This layer produces the final output probabilities for the three classes in the Iris dataset.
  layer_dense(units = 3, activation = 'softmax')
```

With our layers set, let's **compile the model**. We specify the loss function as categorical crossentropy, which is suitable for classification tasks. The optimizer we're using is Adam, a popular choice for training neural networks. We also want to track the accuracy metric during training.

```r
# Compile the model
model2 %>% compile(
  loss = 'categorical_crossentropy',
  optimizer = 'adam',
  metrics = 'accuracy'
)
```

Now, it's time to **train our model**. We fit it to our training data, specifying the number of epochs (how many times we go through the entire dataset) and the batch size (how many samples we use in each update).

```r
# Fit the model to the data
model2 %>% fit(
  iris.training, iris.trainLabels, 
  epochs = 200, batch_size = 5, 
  validation_split = 0.2
)
```

Once training is done, we **evaluate our model** on the test data to see how well it performs on unseen examples.

```r
# Evaluate the model
score2 <- model2 %>% evaluate(iris.test, iris.testLabels, batch_size = 128)
```

And there we have it! Our model is trained and evaluated. Let's **print out** the evaluation score to see how well our model2 performed."

```r
# Print the score
print(score2)
```

## Model 3

Alright, let's dive into **building our third model**, which we'll creatively call "model 3". Now, before we get into the nitty-gritty, let's understand what's going on. First off, we start by **creating a sequential model**. Think of it as a blueprint for our neural network. We're going to stack layers on top of each other, like building blocks.

```r
# Hidden Units:
# Initialize a sequential model
model3 <- keras_model_sequential()
```

Next, we **add layers to our model**. The first layer we add is what we call a "dense" layer. This layer has 28 hidden units. These units are like small computational hubs that process information. We use a "ReLU" activation function here, which helps introduce non-linearity into our model, allowing it to learn complex patterns from the data.

Moving on, we add another dense layer. This one has 3 units, which correspond to the 3 classes in our output. We use a "softmax" activation function here. This function gives us probabilities for each class, essentially telling us how confident our model is about its predictions.

```r
# Add layers to the model
model3 %>% 
  # Add a dense layer with 28 units and ReLU activation function.
  layer_dense(units = 28, activation = 'relu', input_shape = c(4)) %>% 
  # Add another dense layer with 3 units (output classes) and softmax activation function.
  layer_dense(units = 3, activation = 'softmax')
```

Now, it's time to **compile our model**. Compiling is where we define some crucial settings for training, like what loss function to use (in our case, categorical crossentropy), which optimizer to use (Adam, a popular choice), and what metrics to track during training (accuracy, in our case).

```r
# Compile the model
model3 %>% compile(
  loss = 'categorical_crossentropy',
  optimizer = 'adam',
  metrics = 'accuracy'
)
```

With our model compiled, we train it using our **training data**. We'll train it for 200 epochs, which means we'll go through our entire dataset 200 times. Each time, we'll adjust our model's parameters to make it better at predicting.

```r
# Fit the model to the data
model3 %>% fit(
  iris.training, iris.trainLabels, 
  epochs = 200, batch_size = 5, 
  validation_split = 0.2
)
```

After training, it's **evaluation time**! We want to see how well our model performs on data it hasn't seen before (our test data). We calculate a score that tells us how accurate our model is.

```r
# Evaluate the model
score3 <- model3 %>% evaluate(iris.test, iris.testLabels, batch_size = 128)
```

And there you have it! We've built, trained, and evaluated our third model. Now, let's see how well it did by **printing out** its score. Ready? Let's go!

```r
# Print the score
print(score3)
```

## The entire code together:

```r
# Install devtools
# install.packages("devtools")
# Install keras
# devtools::install_github("rstudio/keras")

# Load necessary libraries
library(tidyverse)   # For data manipulation
library(keras3)      # For building neural networks
library(tensorflow)  # Backend for Keras
library(datasets)    # Provides sample datasets


# Load Iris dataset
data(iris)


# Convert class labels to numeric format (0, 1, 2)
iris[,5] <- as.numeric(iris[,5]) - 1

# Convert iris dataframe to a matrix
iris <- as.matrix(iris)

# Set dimension names to NULL
dimnames(iris) <- NULL


# Determine sample size and split the dataset into training and test sets
ind <- sample(2, nrow(iris), replace=TRUE, prob=c(0.67, 0.33))

# Select rows for training set where ind is 1
iris.training <- iris[ind==1, 1:4]

# Select rows for test set where ind is 2
iris.test <- iris[ind==2, 1:4]

# Split the class attribute for training set
iris.trainingtarget <- iris[ind==1, 5]  # Select the class labels corresponding to the training set samples

# Split the class attribute for test set
iris.testtarget <- iris[ind==2, 5]  # Select the class labels corresponding to the test set samples


# One hot encode training target values:
# Convert the class labels of the training set into a one-hot encoded format.
# One-hot encoding transforms categorical labels into a binary matrix where each column represents a unique class, 
# and the column corresponding to the class label is marked as 1 while others are 0.
iris.trainLabels <- to_categorical(iris.trainingtarget)

# One hot encode test target values:
# Similar to the above, convert the class labels of the test set into a one-hot encoded format.
iris.testLabels <- to_categorical(iris.testtarget)


# Print out the one-hot encoded test labels to double-check the result
print(iris.testLabels)
#--------------------------------------- model 1 ----------------------------------------
## Constructing the Model
# Initialize a sequential model
model <- keras_model_sequential() 

# Add layers to the model
# Add a dense (fully connected) layer with 8 units/neurons, ReLU activation function, and input shape of (4,)
# The input shape (4,) corresponds to the number of features in the input data (4 features in Iris dataset)
# The ReLU activation function introduces non-linearity to the network
# The first layer requires specification of input shape since it's the first layer in the model
model %>% 
  layer_dense(units = 8, activation = 'relu', input_shape = c(4)) %>% 
  # Add another dense layer with 3 units/neurons, softmax activation function
  # Softmax activation is commonly used for multi-class classification tasks
  # It ensures that the output values are between 0 and 1 and sum up to 1, representing class probabilities
  layer_dense(units = 3, activation = 'softmax')

# Print a summary of the model architecture, including the number of layers, 
# the type of layers, and the number of parameters in each layer.
summary(model)


# Get model configuration
get_config(model)
# This line retrieves the configuration of the neural network model. 
# It provides details about the architecture, such as the number of layers, 
# the activation functions used, the number of units in each layer, etc.


# Get layer configuration
# Retrieve information about the first layer in the model
get_layer(model, index = 1)

# List the model's layers
model$layers  # This line lists all the layers in the model

# List the input tensors
model$inputs # This line retrieves the list of input tensors for the neural network model. 

# List the output tensors
model$outputs # This line retrieves the list of output tensors for the neural network model

# Compile And Fit The Model:
# Compile the model
model %>% compile(
  loss = 'categorical_crossentropy',  # Specify the loss function for categorical classification
  optimizer = 'adam',                  # Specify the optimizer algorithm (Adam)
  metrics = 'accuracy'                 # Specify the metric to evaluate model performance (accuracy)
)


# Store the fitting history in `history` 
history <- model %>% fit(
  iris.training,           # Training data features (input)
  iris.trainLabels,        # Training data labels (output)
  epochs = 200,            # Number of training epochs (iterations over the entire dataset)
  batch_size = 5,          # Number of samples per gradient update
  validation_split = 0.2   # Fraction of the training data to be used as validation data
)


# Plot the history
plot(history) # Plotting the training history provides visual insights into the model's performance over each epoch.

# Visualize The Model Training History:
# Plot the model loss of the training data
plot(history$metrics$loss, main="Model Loss", xlab = "epoch", ylab="loss", col="blue", type="l")
# This command creates a plot of the model's loss on the training data over epochs.

# Plot the model loss of the test data
lines(history$metrics$val_loss, col="green")

# Add legend
legend("topright", c("train","test"), col=c("blue", "green"), lty=c(1,1))

# Plot the accuracy of the training data 
plot(history$metrics$acc, main="Model Accuracy", xlab = "epoch", ylab="accuracy", col="blue", type="l")

# Plot the accuracy of the validation data
lines(history$metrics$val_acc, col="green")

# Add Legend
legend("bottomright", c("train","test"), col=c("blue", "green"), lty=c(1,1))

# Evaluate on test data and labels
score <- model %>% evaluate(iris.test, iris.testLabels, batch_size = 128)

# Print the score
print(score)
#------------------------------------ model 2 ----------------------------
# Fine-tuning Your Model:
# Adding Layers

# Initialize the sequential model
model2 <- keras_model_sequential() 


# Add layers to model2:
# Add a dense layer with 8 units and ReLU activation function.
# Input shape is specified as (4,), indicating the input features.
# This layer connects to the input layer implicitly.
# Initialize the sequential model

model2 %>% 
  # Add a dense layer with 8 units and ReLU activation function.
  # Input shape is specified as (4,), indicating the input features.
  # This layer connects to the input layer implicitly.
  layer_dense(units = 8, activation = 'relu', input_shape = c(4)) %>% 
  
  # Add another dense layer with 5 units and ReLU activation function.
  # This layer automatically receives input from the previous layer.
  layer_dense(units = 5, activation = 'relu') %>% 
  
  # Add the output layer with 3 units and softmax activation function.
  # This layer produces the final output probabilities for the three classes in the Iris dataset.
  layer_dense(units = 3, activation = 'softmax')



# Compile the model
model2 %>% compile(
  loss = 'categorical_crossentropy',
  optimizer = 'adam',
  metrics = 'accuracy'
)


# Fit the model to the data
model2 %>% fit(
  iris.training, iris.trainLabels, 
  epochs = 200, batch_size = 5, 
  validation_split = 0.2
)

# Evaluate the model
score2 <- model2 %>% evaluate(iris.test, iris.testLabels, batch_size = 128)

# Print the score
print(score2)
#-------------------------------model 3 -------------------------------
# Hidden Units:
# Initialize a sequential model
model3 <- keras_model_sequential() 

# Add layers to the model
model3 %>% 
  # Add a dense layer with 28 units and ReLU activation function.
  layer_dense(units = 28, activation = 'relu', input_shape = c(4)) %>% 
  # Add another dense layer with 3 units (output classes) and softmax activation function.
  layer_dense(units = 3, activation = 'softmax')


# Compile the model
model3 %>% compile(
  loss = 'categorical_crossentropy',
  optimizer = 'adam',
  metrics = 'accuracy'
)

# Fit the model to the data
model3 %>% fit(
  iris.training, iris.trainLabels, 
  epochs = 200, batch_size = 5, 
  validation_split = 0.2
)

# Evaluate the model
score3 <- model3 %>% evaluate(iris.test, iris.testLabels, batch_size = 128)

# Print the score
print(score3)
# Source of the code: https://rpubs.com/Nilafhiosagam/541333
```

#### Source of the code: [https://rpubs.com/Nilafhiosagam/541333](https://rpubs.com/Nilafhiosagam/541333)