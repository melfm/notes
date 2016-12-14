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
