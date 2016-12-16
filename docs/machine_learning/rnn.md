# Recurrent Neural Networks

The idea behind RNNs is the ability to connect previous information to the present task. 
One limitation of vanilla neural networks is that they accept a fixed-sized vector as input and produce a fixed-sized vector as output. 

RNNs accept their own outputs as inputs. The most basic model would be at time step $t$, for $t \in {0,1,...,n}$. It accepts $X_t$ vector and a previous state vector, $S_{t-1}$ as input.
It then produces a state vector $S_t$ and a prediction.

\begin{equation} 
S_t = tanh(W(X_t \| S_{t-1}) + b_s)
\end{equation}

They are powerful because they combine two properties:
- Distributed hidden state that allows them to store info about the past efficiently.
- Non-linear dynamics that allows them to update their hidden state in complicated ways.

Recurrent neural nets are \textit{deterministic}. So think of the hidden state of an RNN as the equivalent to the deterministic probability distribution over hidden states in a linear dynamical system or hidden Markov model.


## RNN Computation
They accept an input vector $x$ and give an output vector $y$. This output vector's contents are influenced not only by the input you feed in, but on the entire history of inputs that have been fed in.
The RNN has an internal state that gets updated every time 'step' function is called. This function updates the state and returns the output vector. So this function, combines the previous hidden state and the current input to obtain the new state. You add the two, and then squash them using the activation function, say tanh to get the new state vector.

## Computation Formulas
- $s_t$ is the hidden state at time step $t$. It's the 'memory' of the network. 
- $s_t$ is calculated based on the previous hidden state and the input at the current step: $s_t = f(Ux_t + W_{s_{t-1}})$. - - The function $f$ usually is a nonlinearity such as tanh or ReLU. $s_{-1}$ which is required to calculate the first hidden state is typically initialized to all zeros.

A few notes :
- Think of hidden state $s_t$ as the memory of the network. $s_t$ captures information about what happened in all the previous time steps. The output at step $o_t$ is calculated solely based on the memory at time $t$.
- Unlike vanilla deep neural network, which uses different parameter at each layer, a RNN shares the same parameters($U,V,W$) across all steps. This reflects the fact that we are performing the same task at each step, just with different inputs. This reduces the total number of parameters we need to learn!
- When you see diagrams showing outputs at each time step, depending on the task you may not care about all! So in some cases you would only care about the final step. We may not even need inputs at each time step. The main feature of an RNN is its hidden state, which captures information about a sequence.

### Backpropagation through time
- Modify the backprop to incorporate linear constraints between the weights.
- We compute the gradients as usual, then modify the gradients so that they satisfy the constraint.

\begin{align}
Constrain: w_1 = w_2 \\
Need: \bigtriangleup w_1 = \bigtriangleup w_2 \\
compute: \frac{\partial E}{\partial w_1} & \frac{\partial E}{\partial w_2} \\
use \frac{\partial E}{\partial w_1} + \frac{\partial E}{\partial w_2}
\end{align}

- So if the weights started off satisfying the constraints, they will continue to do so.
- Think of BPTT in the time domain:
  - The forward pass builds up a stack of the activities of all the units at each time step.
  - Backward pass peels activities off the stack to compute the error derivatives at each time step.
  - After the backward pass we add together the derivatives at all the different times for each weight.

# Initial activity state
- Learn the initial states as learned parameters.
  - Start off with initial random guess for the initial states.
  - At the end of each training sequence, backpropagate through time all the way to the initial states to get the gradient
  of the error function w.r.t. each initial state.
  - Adjust the initial states by following the negative gradient.

# Input to RNN
Several ways:
- Specify the initial states of all the units.
- Specify the initial states of a subset of the units.

# Teaching signals
Several ways:
- Specify desired final activities of all the units.
- Specify desired activities of all units for the last few steps.





