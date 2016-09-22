# Recurrent Neural Networks

RNNs are neural networks that accept their own outputs as inputs.
The most basic model would be at time step $t$, for $t \in {0,1,...,n}$ it accepts $X_t$ vector and a previous state vector, $S_{t-1}$ as input.
It then produces a state vector $S_t$ and a prediction.

\begin{equation} 
S_t = tanh(W(X_t \| S_{t-1}) + b_s)
\end{equation}

Here we are concatenating the input and state vector.

\begin{equation} 
P_t = US_t + b_p
\end{equation}

Dimensions :
$W \in R^{d \times (2 + d)}, b_s \in R^d, U \in R^{2 \times d}, d_p \in R^2$  and $d$ is the step size (size of state vector).

Now the question is how wide the graph should be? Since each time step is a duplicate, it might make sense to initially have a graph $G$,
that represents a single time step : $G(X_t, S_{t-1}) \rightarrow (P_t, S_t)$.
So we could execute the graph for each time, feeding the state returned from the previous execution into the current execution along with the input. There is a problem with this since the gradients computed during backpropagation in terms of propagating the error to time step $t-1$. This means that the network won't learn the dependencies. We could make it wide, as wide as our sequence but then the backpropagation would fail due to the vanishing / exploding gradient problem. That is backpropagating errors over too many time steps often causes them to vanish i.e. become insignificantly small or explode (become overwhelmingly large). So that's why we keep the number of graphs small.

The usual approach for dealing with long sequences is to `truncate' the backpropagation by backpropagating a maximum of $n$ steps.Note the tradeoffs : higher $n$ lets us capture longer term dependencies, but more expensive computationally and memory-wise. 

# TensorFlow Style
Say the graph is $n$ time steps wide, so time-step is a duplicate, sharing the same variables.
Easiest way is to build these duplicates parts in parallel. So this means represent each type of duplicate tensor(the rnn inputs, the rnn outputs (hidden state), the prediction, the loss) as a list of tensors.

So each training step is run by executing the graph, while grabbing the final state produced by that execution to pass on to the next execution.



