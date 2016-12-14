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


## The momentum method
- Used to improve the learning speed when doing gradient descent. 
- Damps oscillations in directions of high curvature.
- Accumulates consistent components of the gradient and attenuates the fluctuating ones.
- Enables using bigger learning rates because the learning os now more stable.

Think of a ball on the area surface. The location of this ball in the horizontal plane represents the weight vector. The ball starts off stationary and initially it follows the direction of steepest descent.  So it's following the gradient happily but as soon as its got some velocity it no longer goes in the same direction as the gradient. Its momentum somehow makes it keep going in the previous direction. Our goal is to get to a low point so we must lose energy. So we introduce viscocity : Make the velocity die off gently.

### The quation of momentum
The effect of the gradient is to increment the previous velocity. The velocity also decays by $\alpha$ :
\begin{equation}
  v(t) = \alpha v(t - 1) - \epsilon \frac{\partial E}{\partial w} (t)
\end{equation}

The weight change is equal to the current velocity
\begin{align}
  \bigtriangleup w(t) = v(t) \\
  = \alpha v(t - 1) - \epsilon \frac{\partial E}{\partial w}(t)
\end{align}

The weight change can be expressed in terms of the previous weight change and the current gradient :

\begin{equation}
  = \alpha \bigtriangleup w(t - 1) - \epsilon \frac{\partial E}{\partial w}(t)
\end{equation}

### The behaviour of momentum
- Be careful to set the momentum, at the beginning of learning there may be very large gradients.
- In the beginning, have a small (e.g. 0.5)
- Once the large gradients are gone and we've reached a normal phase of learning, smoothly raise it to 0.9.

## Adaptive Learning Rate
- Each connection in the neural net should have its own adaptive learning rate
- This is set emprirically by observing what happens to the weight on that connection when we update it
- If the weight keeps reversing its gradient, we turn down the learning weight. If the gradient stays consistent, we turn up the learning weight.

\begin{align}
    \bigtriangleup w_{ij} = -\epsilon g_{ij} \frac{\partial E}{\partial w_{ij}} \\
    if \Bigg( \frac{\partial E}{\partial w_{ij}}(t) \frac{\partial E}{\partial w_{ij}} (t-1) \Bigg) > 0 \\
    then g_{ij}(t) = g_{ij} (t - 1) + .05 \\
    else g_{ij}(t) = g_{ij} (t - 1) * .95
\end{align}
  

So why is this a good idea? In a deep multilayer net, the learning weights can vary widely between different weights.
Another factor is the fan-in of the unit (that is just the shape say going from input to hidden layer, kind of looks like a fan). So the size of this fan-in determines the size of the overshoot effect that you get when you simultaneously change many of the different incoming weights to fix up some error.

Tricks to make it work better ?
- Limit the size of the gains. A reasonable range is 0.1 to 10. Or 0.1 to 100.
- Don't want the gains to get huge because it can easily get into an instability and destroying weights.
This was designed for full batch learning but can be applied with mini batches but they had better be pretty big mini batches. That'll ensure that the sign, changing signs of gradient aren't due to sampling error of mini batches, but rather due to the other side of the ravine.
