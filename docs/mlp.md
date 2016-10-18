# Weight space
This space has one dimension per weight. A point in the space represents a particular setting of all the weights. Each training case can be represented as a hyperplane through the origin. The weights must lie on one side of this hyper-plane to get the answer correct.

# Linear neurons (linear filters)
The neuron has a real-valued output which is a weighted sum of its inputs. 

\begin{equation}
y = \sum{_i} w_i x_i = w^T x
\end{equation}

The aim of learning is to minimize the error summed over all training cases, where the error is the squared difference between the desired output and the actual output. Using iterative methods to solve this gives us a generalized multi-layer, non-linear neural networks, despite being less efficient to compute.

## Delta-rule
Define the errors as the squared residuals summed over all training cases:

\begin{equation}
E = \frac{1}{2} \sum_{n \in training} {(t^n - y^n)}^2
\end{equation}

We put a 1/2 in front so it cancels out with the square term when we differentiate.
We now differentiate this error measure to get error derivatives for weights :

\begin{equation}
\frac{\partial E}{\partial w_i} = \frac{\partial y^n}{\partial w_i} \frac{ dE^n}{ dy^n}
\end{equation}

\begin{equation}
= - \sum x^{n}_i (t^n - y^n)
\end{equation}

To do the differentiation we use the chain rule. The chain rule says that how the error changes as we change the weight will be how the output changes times how the error changes as we change the output! (the way you do it is that you cancel out the dy's... ). Note how the first term is a partial derivative, that is there are different ways of changing the output and here we are just considering the change to weight $i$.

So out learning rule becomes the following :

\begin{equation}
\bigtriangleup w_i = -\epsilon \frac{\partial E}{\partial w_i}= \sum \epsilon x^{n}_{i}(t^n - y^n)
\end{equation}

We change the weights by the amount of epsilon times the derivative of the error w.r.t the weight and with a minus sign because we want the error to go down. This minus then cancels out with the minus in the above term and that gives the final expression : sum of all training cases, learning rate times input value times the difference between target and actual output.

# Linear neurons

# Logistic neurons
These give a real-valued output that is a smooth and bounded function of their total input.
\begin{equation}
z = b + \sum_i x_i w_i
\end{equation}

\begin{equation}
 y = \frac{1}{1 + e ^{-z}}
\end{equation}

The fact that the logit function changes continuously, gives nice derivatives which makes learning easy!

## The derivatices of a logistic neuron
The derivatives of the logit, z, w.r.t. the inputs and weights :
\begin{equation}
\frac{\partial z}{\partial w_i} = x_i
\end{equation}

\begin{equation}
\frac{\partial z}{\partial w_i} = w_i
\end{equation}

The derivatives of the output w.r.t. the logit is simple if expressed in terms of the output:
\begin{equation}
\frac{dy}{dz} = y (1 - y)
\end{equation}

Now to learn the weights we need the derivative of the output w.r.t. each weight.
Using chain rule we can get the derivatives needed for learning the weights.

\begin{equation}
\frac{\partial y}{\partial w_i} = \frac{\partial z}{\partial w_i} \frac{\partial y}{\partial z} = x_i y (1-y)
\end{equation}

We now have the learning rule :
\begin{equation}
\frac{\partial E}{\partial w_i} = \sum \frac{\partial y^n}{\partial w_i} \frac{\partial E}{\partial y^n} = - \sum x^{n}_{i} y^n (1-y^n) (t^n - y^n)
\end{equation}

The way the error changes the weights, is by summing over training cases times the residual (difference between output and target) but note the middle term, this is the slope of logistic. So here we're just modifying the delta rule.

# Backpropagation
The idea is to get error derivatives w.r.t. hidden neuron activities. Each hidden activity can affect many output units and can therefore have many separate effects on the error. These effects must be combined. Once we have the error derivatives for the hidden activities, its easy to get the error derivatives for the weights going into a hidden unit.
First we definee our error, we differentiate that and this tells us how the error changes as we change the activity of the output unit. So once we have the error derivative w.r.t. output of the hidden unit, we then want to use all the derivatives in the output layer to compute the same quantity in the hidden layer that comes before.
The core of backpropagation is taking error derivatives in one layer, and from them computing the error derivatives that come before that. 

# Softmax Regressions
This is a generalization of the logistic function, it squashes a k-dimensional vector of arbitrary real values to a k-dimensional vector of real values with ranges (0,1).
Consider the MNIST classification. A softmax regression has two steps: first we add up the evidence of our input being in certain classes, and then we convert that evidence into probabilities.

Think of bias as extra evidence, we want to able to say that some things are more likely independent of the input. The result is that the evidence for a class $i$ given an input $x$ is:

\begin{equation} 
evidence_i = \sum_j W_{i,j}x_j + b_i
\end{equation}

where $W_i$ is the weights and $b_i$ is the bias for class $i$, and $j$ is an index for summing over the pixels in input image $x$. To convert evidence into probabilities we use the `softmax' function:

\begin{equation} 
y = softmax(evidence)
\end{equation}

Softmax serves as an activation function, shaping the output of our linear function into probability form, that is a probability distribution over 10 cases.

\begin{equation} 
y = softmax(Wx + b)
\end{equation}

# Cross-entropy
When we train a neural network, we need to define what it means for the model to be good. Actually we usually define the other way round, what it means for a model to be bad, called cost or loss. We then try to minimize how bad it is.
Cross-entropy arises from thinking about information compressing codes in information theory.


\begin{equation} 
H_{{y}'}(y) = - \sum_i {y}'_{i} log(y_i)
\end{equation}

where $y$ is the predicted probability distribution and ${y}'$ is the true distribution.


# Weight Initialization
One should generally initialize weights with a small amount of noise for symmetry breaking and to prevent 0 gradients.
If using ReLU neurons, it is good practce to initialize them with a slightly positive initial bias to avoid `dead neurons'.


# Ways to reduce overfitting
- Weight-decay
- Weight-sharing
- Early stopping
- Model averaging
- Bayesian fitting of neural nets
- Dropout
