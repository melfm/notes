Models used for sequential data:

## Autoregressive models
Try to predict the next term or the sequence from previous terms using "delay taps".
This is a memoryless model for sequences. A linear auto regressive would take a weighted average of those to predict the next term.
We can make this more complicated by adding hidden units. So in a feedforward neural net, we might take some previous input terms, put them through
some hidden units and predict the next term.

## Generative models
If we give a generative model some hidden state, and if we give this hidden state its own internal dynamics, we get a much more
interesting model which can store info in its hidden state for a long time.

## Linear Dynamical Systems
Generative models with real-valued hidden state that cannot be observed directly.
The hidden state has linear dynamics with Gaussian noise and produces the observations using a linear
model with Gaussian noise.
One nice property is that a linearly transformed Gaussian is a Gaussian. So the distribution over the hidden
state given the data so far is Gaussian. This can be computed using "Kalman filtering", a recusive way to update
the representation of the hidden state given the observations.

# Hidden Markov model
These models have a discrete one-of-N hidden state. Transitions between states are stochastic and controlled by a transition matrix.
We say the state is "hidden" because we can't be sure which state produced a given output.
To predict the next output we need to infer the probability distribution over hidden states.
Method based on dynamic programming enables us to do so.

## Limitation
When a hidden Markov model generates data, at each time step it must select one of its hidden states.
With $N$ hidden states it can only remember $log(N)$ bits about what it generated so far.
As the information increases, the number of required states becomes too large.

# Stochastic models
Linear dynamical systems and hidden Markov models are stochastic, but the posterior probability distribution over their hidden 
states given the observed data so far is a deterministic function of the data.