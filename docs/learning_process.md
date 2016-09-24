# Learning Processes 
## Boltzmann Learning
The Boltzmann learning rule is a stochastic algorithm. A neural network with this learning rule is a Boltzmann machine.
The neurons constitute a recurrent structure, and they operate in a binary manner since they are for instance either in an `on' state or `off' state.
The machine is characterized by an energy function, $E$, the value of which is determined by the particular states occupied by the inidividual neurons of the machine :

\begin{equation}
E = -\frac{1}{2} \sum_j \sum_k w_{kj}x_k x_j
\end{equation}

where $x_j$ is the state of neuron $j$, and $w_{kj}$ is the synaptic weight connecting neurons $j$ to neuron $k$.
However $j \neq k$
