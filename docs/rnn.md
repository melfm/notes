# Recurrent Neural Networks

RNNs are neural networks that accept their own outputs as inputs.
The most basic model would be at time step $t$, for $t \in {0,1,...,n} it accepts $X_t$ vector and a previous state vector, $S_{t-1} as input.
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
that represents a single time step : $G(X_t, S_{t-1}) \rightarrow (P_t, S_t)$
