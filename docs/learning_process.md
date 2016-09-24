# Learning Processes 
## Boltzmann Learning
The Boltzmann learning rule is a stochastic algorithm. A neural network with this learning rule is a Boltzmann machine.
The neurons constitute a recurrent structure, and they operate in a binary manner since they are for instance either in an `on' state or `off' state.
The machine is characterized by an energy function, $E$, the value of which is determined by the particular states occupied by the inidividual neurons of the machine :

\begin{equation}
E = -\frac{1}{2} \sum_j \sum_k w_{kj}x_k x_j
\end{equation}

where $x_j$ is the state of neuron $j$, and $w_{kj}$ is the synaptic weight connecting neurons $j$ to neuron $k$.
However $j \neq k$ means that none of the neurons in the machine has a self-feedback.
The machine operates by choosing a neuron at random say neuron $k$ - at some step of the learning process, then flipping the state of neuron $k$ from state $x_k$ to state $-x_k$ at some *temperature* $T$ with probability :

\begin{equation}
P(X_k \Rightarrow -X_k) = \frac{1}{1 + exp(-\bigtriangleup E_k / T )}
\end{equation}

where $\bigtriangleup E_k$ is the energy change resulting from such a flip! If this rule is applied repeatedly, the machine will reach thermal equilibrium.
The neurons of a Boltzmann machine partition into two functional groups:visible and hidden.
The visible neurons provide an interface between the network and the environment in which it operates; wheras the hidden neurons always operate freedly. There are two modes of operation:


1. Clamped condition, in which the visible neurons are all clamped onto specific states determined by the environment.

2. Free-running condition, in which all the neurons (visible and hidden) are allowed to operate freely.




