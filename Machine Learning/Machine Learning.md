# Improving Deep Neural Networks: Hyperparameter tuning, Regularization and Optimiztion

When we create our model, we have to decide the hyperparameters in order to improve the performence of our model, the possible hypermaters could be:

- Number of layers
- Number of hidden units
- Learning rate
- activation functions

![ML iterative process](images/ml_iterative_process.png)

It is very difficult to guess the best choic of hyperparameters 

## How to splite data into  Train/dev/test

We often splite the data into train/dev/test set. The test set.

Train set used to train the model.
Dev set(hold-out cross validation set) used to test the model's performence and compare different algorithms.
Test set used to test the model and get unbiased estimate.

- Small dataset : 
    60%/20%/20% or 70%/30%
- Big dataset :
    98%/1%/1%

The test set and dev set should come from the same distribution. In some times, the test set is not necessary.

## Bias-Variance trade-off
