# Boltzmann Machine
- Stochastic Hopfield nets with hidden units are called Boltzmann machines
- They are good at modelling binary data, given a set of binary training vectors, they can use the hidden units to fit a model and assigns probability to every possible binary vector.
- Useful in cases such as monitoring complex systems to detect unusual behaviour. For example in a nuclear power station with binary dials, we want to detect if its in an unusual state even if its a state never seen before. So its not a supervised learning, its a model of normal states.
- If we have models of several different distributions it can be used to compute the posterior probability that a particular distribution produced the observed data.

\begin{equation}
	p(\textrm{Model i|data}) = \frac{p(\textrm{data|Model i})}{\sum_j p(\textrm{data|Model j})}
\end{equation}

## Data generation with a causal model
- In a causal model we generate data in two sequential steps:
	- Pick the hidden states (laten variables from their prior distribution
	- Then pick the visible states from their conditional distribution given the hidden states
- This is a kind of neural network, causal, *generative model*.
- It uses biases for the hidden units and weights on the connections between hidden and visible units to assign a probability to every possible visible vector.
- The probability of generating a visible vector $v$ is computed by summing over all possible hidden states.

\begin{equation}
	p(v) = \sum_j p(h)p(v|h)
\end{equation}

## How a Boltzmann Machine generates data
- Energy based model, so we don't generate data causally.
- It's not a causal generative model.
- Everything is defined in terms of the energies of join configurations of visible and hidden units.

