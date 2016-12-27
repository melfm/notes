# Boltzmann Machine
- Stochastic Hopfield nets with hidden units are called Boltzmann machines
- They are good at modelling binary data, given a set of binary training vectors, they can use the hidden units to fit a model and assigns probability to every possible binary vector.
- Useful in cases such as monitoring complex systems to detect unusual behaviour. For example in a nuclear power station with binary dials, we want to detect if its in an unusual state even if its a state never seen before. So its not a supervised learning, its a model of normal states.
- If we have models of several different distributions it can be used to compute the posterior probability that a particular distribution produced the observed data.

\begin{equation}
	p(\textrm{Model i|data}) = \frac{p(\textrm{data|Model i})}{\sum_j p(\textrm{data|Model j})}
\end{equation}

- So given the observed data, the probability it came from Model |, under the assumption that it came from one of our models, is the probability that Model | would have produced the data divided by the same quantity for all models. 

## Data generation with a causal model
- In a causal model we generate data in two sequential steps:
	- Pick the hidden states (laten variables from their prior distribution
	- Then pick the visible states from their conditional distribution given the hidden states
- This is a kind of neural network, causal, *generative model*.
- It uses logistic units and biases for the hidden units and weights on the connections between hidden and visible units to assign a probability to every possible visible vector.
- The probability of generating a visible vector $v$ is computed by summing over all possible hidden states.

\begin{equation}
	p(v) = \sum_j p(h)p(v|h)
\end{equation}

## How a Boltzmann Machine generates data
- Energy based model, so we don't generate data causally.
- It's not a causal generative model.
- Everything is defined in terms of the energies of join configurations of visible and hidden units.
- The energies of joint configurations are related to their probabilities in two ways.
	- Define the probability to be $p(v,h) \alpha e^{-E(v,h)}$
	- Alternatively, define the probability of finding the net in that joint configuration after updating all the stochastic binary units many times.

## The energy of a joint configuration
\begin{equation}
	-E(v,h) = \sum_{i \in vis} v_ib_i + \sum_{k \in hid} h_kb_k + \sum_{i < j} v_iv_jw_{ij} + \sum_{i,k} v_ih_kw_{ik} + \sum_{k<l} h_kh_lw_{kl}
\end{equation}

- Put the negative energy to save having to put lots of minus signs.
- Here $v$ is on the visible units and $h$ on the hidden units, $b$ is bias of unit $k$.
- The visible-visible interactions
- Weight between visible unit $i$ and hidden unit $k$.

## Using energies to define probabilities
- The probability of a joint configuration over both visible and hidden units depends on the energy of that joint configuration compared with the energy of all other joint configurations.
\begin{equation}
	p(v,h) = \frac{e^{-E(v,h)}}{\sum_{u,g} e^{-E(u,g)}}
\end{equation}
- The denominator is usually called the partition function.
- To get the probability of a configuration of the visible units we take the sum of the probabilities of all the joint configurations.
\begin{equation}
	p(v,h) = \frac{\sum_h e^{-E(v,h)}}{\sum_{u,g} e^{-E(u,g)}}
\end{equation}
- If there are more than a few hidden units, we can't compute the normalizing terms (the partition function) because it has exponentially many terms.
- We can use Markov Chain Monte Carlo to get samples from the model starting at random global config:
	- Keep picking units at random and allowing them to stochastically update their states based on their energy gaps.
	- Run the Markov Chain until it reaches its stationary distribution (thermal equilibrium,$t=1$).
		- The probability of a global configuration is then related to its energy by the Boltzmann distribution.
\begin{equation}
	p(v,h) \alpha e^{-E(v,h)}
\end{equation}


Q. This is a Boltzmann Machine, what is $P(V_1 = 1, V_2 = 0)$ ? 
![Question](images/boltzmann_q.png)

A. There are four configurations. Each has an energy and from the energies we can calculate the probabilities.
- $E(V_1 = 0, V_2=0) = 0$ because nothing is on.
- $E(V_1 = 0, V_2=1) = -1$.
- $E(V_1 = 1, V_2=0) = -1$.
- $E(V_1 = 1, V_2=1) = 0$.

Thus:
\begin{align}
	\sum_s exp(-E(s)) = exp(0) + exp(1) +exp(1) + exp(0) \approx 7.4366 \\
	E(V_1 = 1, V_2 =0) \approx \frac{exp(1)}{7.4366} \approx 0.366
\end{align}

## Boltzmann machine learning
- Want to maximize the product of the probabilities that the Botlzmann machine assigns to the binary vectors in the training set.
	- Equivalent to maximizing the sum of the log probabilities that the Boltzmann machine assigns to the training vectors.
- Also equivalent to maximizing the probability that we would obtain exactly $N$ training cases if:
	- Let the network settle to its stationary distribution $N$ different times with no external input.
	- Sample the visible vector once each time.






