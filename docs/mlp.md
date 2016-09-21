# Softmax Regressions

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













