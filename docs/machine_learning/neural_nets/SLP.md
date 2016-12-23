# Single-Layer Perceptron
The perceptron is the simplest form of a neural netwrok used for classification of patterns said to be linearly separable meaning that the patterns that lie on the opposite side of a hyperplane. It consists of one neuron with adjustable synaptic weights and bias. The perceptron built around built around a single neuron is limited to performing pattern classification with only two classes. By expanding the output (computation) layer of the perceptron to include more than one neuron, we may correspondingly form classification with more than two classes.


A neural model consists of a linear combiner followed by a hard limiter (performing say the signum function). The summing node of the neuronal model computes a linear combination of the inputs applied to its synapses and also incorporates an externally applied bias, remember this bias incorporates relations independent of input. So the hard limiter input is :

\begin{equation}
v = \sum^{m}_{i=1} w_i x_i + b
\end{equation}

In the simplest form of the perceptron there are two decision regions separated by a hyperplane defined by
\begin{equation}
 \sum^{m}_{i=1} w_i x_i + b = 0
\end{equation}

The synaptic weights are adapted on an iteration-by-iteration basis. For the adaptation, the perceptron convergence algorithm is used.

## Perceptron Convergence Theorem
Lets define our input vector :
\begin{equation}
x(n) = [+1, x_1(n), x_2(n),...,x_m(n)]^T
\end{equation}

where $n$ is the iteration step in applying the algorithm. Lets define our weights :
\begin{equation}
w(n) = [b(n), w_1(n), w_2(n),...,w_m(n)]^T
\end{equation}

The linea combiner output is written in the form :
\begin{align}
v(n) = \sum^{m}_{i=0} w_i(n)x_i(n) \\
= w^T(n)x(n)
\end{align}

where $w_0(n)$ represents the bias $b(n)$.

The algorithm for adapting weights is formulated as follows :

If the $n^{th}$ member of the training set $x(n)$ is correctly classified by the weight vector $w(n)$ computed at the $n^{th}$ iteration of the algorithm, no correction is made to the weight vector of the perceptron in accordance with the rule :

$W(n + 1) = w(n)$  if $w^T x(n) > 0$ and x(n) belongs to class $C_1$

$W(n + 1) = w(n)$  if $w^T x(n) \leq 0$ and x(n) belongs to class $C_1$

else, the weight vector of the perceptron is updated in accordance with the rule

$W(n + 1) = w(v) - \eta(n)x(n)$  if $w^T x(n) > 0$ and x(n) belongs to class $C_1$

$W(n + 1) = w(v) + \eta(n)x(n)$  if $w^T x(n) \leq 0$ and x(n) belongs to class $C_1$



