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

High Bias estimator means the model can not fit well the training set. So the model is underfitting the data.
High variance means the model is over fitting. This estimator is complexe enough to fit the train data but it don't work well
in test set.
A estimator could be high bias and high variance at the same time. In this condition, the estimator is complexe enough but
it still don'tt work well in the train set.

## Basic Recipe for Machine Learning

### High Bias

Estimator doesn't work well in the train set.
Measure:

- User more hidden units
- Add more hidden layers
- Train longer
- Try another architecture of neuro network

### High variance

Estimator doesn't work well for the test set.
Mesure:

- Use more data to train our model
- Regularization
- Find new neuro networl architecture

Firstly, you have to get rid of high bias problem by fitting or overfitting train data, and then we try to resolve the high variance problem.
We can find we use different approche to resolve the two problems. So we can increase one without hurt another one.


# Regularization

## L2 regularization 

Regularization could prevent the overfitting.
If the parameters W very small, so the Z will become relatively small. So the Z will take on a very small range of values.
So the activation function **tanh** will be relatively linear. So the neural network will be computing something not too far from linear function.

If we add regularization, the cost function $J$ will decrease monotonically on very single elevation. Otherwise, not. It is very useful for debug.(But in tensorflow palyground, this phenomenon is not very evident.)

What you should remember -- the implications of L2-regularization on:

- The cost computation:
  - A regularization term is added to the cost
- The backpropagation function:
  - There are extra terms in the gradients with respect to weight matrices
- Weights end up smaller ("weight decay"):
  - Weights are pushed to smaller values

### Observation 
- The value of  $λ$  is a hyperparameter that you can tune using a dev set.
- L2 regularization makes your decision boundary smoother. If $λ$  is too large, it is also possible to "oversmooth", resulting in a model with high bias.
-  Although we increase the numbre of iteration, the boundary also keeps slippy and the forme of boundary doesn't change.


What is L2-regularization actually doing?:

L2-regularization relies on the assumption that a model with small weights is simpler than a model with large weights. Thus, by penalizing the square values of the weights in the cost function you drive all the weights to smaller values. It becomes too costly for the cost to have large weights! This leads to a smoother model in which the output changes more slowly as the input changes.

What you should remember -- the implications of L2-regularization on:

The cost computation:
A regularization term is added to the cost
The backpropagation function:
There are extra terms in the gradients with respect to weight matrices
Weights end up smaller ("weight decay"):
Weights are pushed to smaller values.

## Dropout regularization


We set some probability of eliminationg a node in neural network for each sample.So we train our sample with deminished network. So the network become more simple and prevent the overfitting.

Don't not use dropout at test time.


### Note:
A common mistake when using dropout is to use it both in training and testing. You should use dropout (randomly eliminate nodes) only in training.
Deep learning frameworks like tensorflow, PaddlePaddle, keras or caffe come with a dropout layer implementation. Don't stress - you will soon learn some of these frameworks.

### What you should remember about dropout
- Dropout is a regularization technique.
- You only use dropout during training. Don't use dropout (randomly eliminate nodes) during test time.
- Apply dropout both during forward and backward propagation.
- During training time, divide each dropout layer by keep_prob to keep the same expected value for the activations. For example, if keep_prob is 0.5, then we will on average shut down half the nodes, so the output will be scaled by 0.5 since only the remaining half are contributing to the solution. Dividing by 0.5 is equivalent to multiplying by 2. - Hence, the output now has the same expected value. You can check that this works even when keep_prob is other values than 0.5.

### Other regularization methodes

- Data augmentation.
- **Early stopping** When the network start to overfit the dataset, wo stop to train our model. It didn't  recommanded. It could be used to save time.So we just ust it when we try to find best hyperparameters. 


### What we want you to remember from this notebook:

- Regularization will help you reduce overfitting.
- Regularization will drive your weights to lower values.
- L2 regularization and Dropout are two very effective regularization techniques.


#  Normalizing inputs

Normalizing input features could speed up training.

## Initialization for Deep Nerworks


- General
  
     $$W^{[l]} = np.random.randn(shape) * \sqrt{\frac{2}{n^{[l-1]}}}$$

- For **tanh** activation function - Xavier initialization
  $$\sqrt{\frac{1}{n^{[l-1]}}} $$

- $$\sqrt{\frac{2}{n^{[l-1]}+n^{[l]}}}$$

- The weights  W[l]W[l]  should be initialized randomly to break symmetry.
- It is however okay to initialize the biases  b[l]b[l]  to zeros. Symmetry is still broken so long as  W[l]W[l]  is initialized randomly.
- Initializing weights to very large random values does not work well.
- Hopefully intializing with small random values does better. The important question is: how small should be these random values be? Lets find out in the next part!

- Different initializations lead to different results
- Random initialization is used to break symmetry and make sure different hidden units can learn different things
- Don't intialize to values that are too large
- He initialization works well for networks with ReLU activations.



# Graduent Checking
Backpropagation computes the gradients $\frac{\partial J}{\partial \theta}$, where $\theta$ denotes the parameters of the model. $J$ is computed using forward propagation and your loss function.

Because forward propagation is relatively easy to implement, you're confident you got that right, and so you're almost  100% sure that you're computing the cost $J$ correctly. Thus, you can use your code for computing $J$ to verify the code for computing $\frac{\partial J}{\partial \theta}$. 

Let's look back at the definition of a derivative (or gradient):
$$ \frac{\partial J}{\partial \theta} = \lim_{\varepsilon \to 0} \frac{J(\theta + \varepsilon) - J(\theta - \varepsilon)}{2 \varepsilon} \tag{1}$$

If you're not familiar with the "$\displaystyle \lim_{\varepsilon \to 0}$" notation, it's just a way of saying "when $\varepsilon$ is really really small."

We know the following:

- $\frac{\partial J}{\partial \theta}$ is what you want to make sure you're computing correctly. 
- You can compute $J(\theta + \varepsilon)$ and $J(\theta - \varepsilon)$ (in the case that $\theta$ is a real number), since you're confident your implementation for $J$ is correct. 

Lets use equation (1) and a small value for $\varepsilon$ to convince your CEO that your code for computing  $\frac{\partial J}{\partial \theta}$ is correct!

## 2) 1-dimensional gradient checking

Consider a 1D linear function $J(\theta) = \theta x$. The model contains only a single real-valued parameter $\theta$, and takes $x$ as input.

You will implement code to compute $J(.)$ and its derivative $\frac{\partial J}{\partial \theta}$. You will then use gradient checking to make sure your derivative computation for $J$ is correct. 

<img src="images/1Dgrad_kiank.png" style="width:600px;height:250px;">
<caption><center> <u> **Figure 1** </u>: **1D linear model**<br> </center></caption>

The diagram above shows the key computation steps: First start with $x$, then evaluate the function $J(x)$ ("forward propagation"). Then compute the derivative $\frac{\partial J}{\partial \theta}$ ("backward propagation"). 

**Exercise**: implement "forward propagation" and "backward propagation" for this simple function. I.e., compute both $J(.)$ ("forward propagation") and its derivative with respect to $\theta$ ("backward propagation"), in two separate functions. 