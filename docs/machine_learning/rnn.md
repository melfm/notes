# Recurrent Neural Networks


The idea behind RNNs is the ability to connect previous information to the present task. One limitation of Vanilla Neural Networks is that they accept a fixed-sized vector as input and produce a fixed-sized vector as output. In addition, they perform this mapping using a fixed amount of computational steps (e.g. number of layers in the model).

RNNs are neural networks that accept their own outputs as inputs. The most basic model would be at time step $t$, for $t \in {0,1,...,n}$ it accepts $X_t$ vector and a previous state vector, $S_{t-1}$ as input.
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

They essentially combine the input vector with their state vector with a fixed but learned function to produce a new state vector. This is like running a fixed program with certain inputs and internal variables.

Now the question is how wide the graph should be? Since each time step is a duplicate, it might make sense to initially have a graph $G$,
that represents a single time step : $G(X_t, S_{t-1}) \rightarrow (P_t, S_t)$.
So we could execute the graph for each time, feeding the state returned from the previous execution into the current execution along with the input. There is a problem with this since the gradients computed during backpropagation in terms of propagating the error to time step $t-1$. This means that the network won't learn the dependencies. We could make it wide, as wide as our sequence but then the backpropagation would fail due to the vanishing / exploding gradient problem. That is backpropagating errors over too many time steps often causes them to vanish i.e. become insignificantly small or explode (become overwhelmingly large). So that's why we keep the number of graphs small.

The usual approach for dealing with long sequences is to `truncate' the backpropagation by backpropagating a maximum of $n$ steps.Note the tradeoffs : higher $n$ lets us capture longer term dependencies, but more expensive computationally and memory-wise. 

## RNN Computation
They accept an input vector $x$ and give an output vector $y$. This output vector's contents are influenced not only by the input you feed in, but on the entire history of inputs that have been fed in.
The RNN has an internal state that gets updated every time 'step' function is called. This function updates the state and returns the output vector. So this function, combines the previous hidden state and the current input to obtain the new state. You add the two, and then squash them using the activation function, say tanh to get the new state vector.

## Computation Formulas
- $s_t$ is the hidden state at time step $t$. It's the 'memory' of the network. $s_t$ is calculated based on the previous hidden state and the input at the current step: $s_t = f(Ux_t + W_{s_{t-1}})$. The function $f$ usually is a nonlinearity such as tanh or ReLU. $s-1$ which is required to calculate the first hidden state is typically initialized to all zeros.

A few notes :
- Think of hidden state $s_t$ as the memory of the network. $s_t$ captures information about what happened in all the previous time steps. The output at step $o_t$ is calculated solely based on the memory at time $t$.
- Unlike vanilla deep neural network, which uses different parameter at each layer, a RNN shares the same parameters($U,V,W$) across all steps. This reflects the fact that we are performing the same task at each step, just with different inputs. This reduces the total number of parameters we need to learn!
- When you see diagrams showing outputs at each time step, depending on the task you may not care about all! So in some cases you would only care about the final step. We may not even need inputs at each time step. The main feature of an RNN is its hidden state, which captures information about a sequence.
## TensorFlow Style
Say the graph is $n$ time steps wide, so time-step is a duplicate, sharing the same variables.
Easiest way is to build these duplicates parts in parallel. So this means represent each type of duplicate tensor(the rnn inputs, the rnn outputs (hidden state), the prediction, the loss) as a list of tensors.

So each training step is run by executing the graph, while grabbing the final state produced by that execution to pass on to the next execution.

Most basic RNN: output = new_state = activation(W * input + U * state + B)







### Truncated Backpropagation
It is common to truncate the gradients for backrpopagation to a fixed number (num_steps) of unrolled steps. This is implemented by feeding inputs of length num_steps at a time and doing backward pass after each iteration.

# LSTM
Designed to remember information for long periods of time.

Resources:
1. http://colah.github.io/posts/2015-08-Understanding-LSTMs/

