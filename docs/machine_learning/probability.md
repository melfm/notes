# Probability

Probability theory provides means of quantifying uncertainty
and axioms for deriving new uncertain statements

## Probability of an event
Let's define it as the fraction of times that event occurs out of the total number of trials
* Probabilities must lie in the interval $[0, 1]$
* If the events are mutually exclusive and if they include all possible outcomes, then the
probabilities of those events must sum to one

## Fundamental Rules of Probability
\begin{equation}
sum \ rule \quad p(X) = \sum_Y p(X, Y)
\end{equation}

\begin{equation}
product \ rule \quad p(X,Y) = p(Y|X)p(X)
\end{equation}

Note: $p(X = x_i)$ is sometimes called the $\textbf{marginal}$ probability, because
it is obtained by marginalizing or summing out the other variables (say $Y$ in this case)

## Random variable
A random variable is a variable that can taken on different
values randomly. Random variable may be discrete or continuous.
* The probability that $X$ takes the value $r$ is denoted $P(X=r)$
* May simply write $P(X)$ to denote a distribution over the random
variable $X$ or $p(r)$ to denote the distribution evaluated for the particular value $r$


## Joint probability
- Measures the likelihood of two events occurring together at the same point in time
- $p(X,Y)$ is a joint probability -> The probability of $X$ and $Y$
- $P(X = x, Y= y)$ denotes the probability that $X =x $ and $ Y=y$
- $p(X=x \ and \ Y=y) = p(x,y)$
- e.g. P of clouds and rain today


## Conditional Probability
- $P(Y|X)$ is a conditional probability -> The probability of $Y$ given $X$
- Probability of some event, given that some other event has happened
- From the product rule and symmetry property $p(X,Y)=p(Y,X)$ we get the following
relationship between conditional probabilities
\begin{equation}
P(Y| X) = \frac{P(X|Y)p(Y)}{P(X)}
\end{equation}
- This is called the $\textbf{Bayes' theorem}$
- Using the rum rule, the denominator in Bayes' theorem can be expressed in terms of the
quantities appearing in the numerator
\begin{equation}
P(X) = \sum_Y p(X|Y)p(Y)
\end{equation}
- Relation to joint probability
	- $p(x|y)=\frac{p(x,y)}{p(y)}$
- If X and Y are independent -> $p(x|y)=p(x)$
- e.g. "critical hit" roll  20 then 19 or 20

\begin{equation}
	\rho(critical | first=20) = \frac{\rho(second=19 \quad or \quad 20)\rho(first=20)}{\rho(first=20)} = \frac{2}{20}
\end{equation}

\begin{equation}
	\rho(critical | first!=20) = 0 \quad not \quad independent!
\end{equation}
Note: It is important not to confuse conditional probability with
computing what would happen if some actions were undertaken. The conditional
probability that a person is from Germany given that they speak German is quite
high, but if a randomly selected person is taught to speak German, their
country of origin does not change

### Discrete random variable
- Has a finite or countably finite number of states
- These states are not necessarily integers; they can also
just be named states that are not considered to have any
numerical values
- X denotes a random variable
- X can take on a countable number of values
	- $X \in {x_1,...,x_n}$
- The probability that X takes on a specific value
	- $P(X = x_i)$ or $p(x_i)$


### Continuous Random Variable
- Associated with a real value
- X takes on a value in a continuum
- Probability density function, $p(x)$
- Evaluated over finite intervals of the continuum
	- $p(x \in (a,b)) = \int_a^b p(x)dx$

## Probability Distributions
- Description of how likely a random variable or set of random
variables is to take on each of its possible states
- Probability distribution over discrete variables may be described
using a probability mass function (PMF)
- Probability distribution over continuous random variables may
be described using a probability density function (PDF)

## Measures of Distributions

- Mean (expected value of a random variable)
	- $\mu = E[X]$
	- $\mu = \sum_{i=1}^n x_i p(x_i)$ discrete case
	- $\mu = \int xp(x)dx $ continuous case
- Variance (Measure of variability of a random variable)
    - How much the values of a function of a random var vary
    as we sample different values of $x$
	- $Var(X) = E[(X - \mu)^2]$
	- $Var(X) = \sum_{i=1}^n (x_i - \mu)^2 p(x_i)$ discrete case
	- $Var(X) = \int (x - \mu)^2 p(x)dx$
- Square root of variance is standard deviation, $\sigma ^2=Var(X)$

### Expectation
- The expectation or expected value of some function $f(x)$ w.r.t
a probability distribution $P(x)$ is the average or mean value that
$f$ takes on when $x$ is drawn from $P$
- For discrete variables :
    - $E_{x \sim P}[f(x)] = sum_x P(x)f(x)$
- For continuous:
    - $E_{x \sim P}[f(x)] = \int P(x)f(x) dx$


### Covariance
- Measure of how much two random variables change together
	- $Conv(X_i,X_j) = E[(X_i - \mu_i)(X_j - \mu_j)]$
- If $Conv(X,Y)>0$ when X is above its expected value ->
	- then Y tends to be above its expected value
- If $Conv(X,Y)<0$ when X is above its expected value ->
	- then Y tends to be below its expected value
- If X,Y are independent, $Conv(X,Y)=0$


### Covariance Matrix, $\Sigma$
- Defines variational relationship between each pair of random variables
	- $\Sigma_{i,j} = Conv(X_i, X_j)$
- Generalization of variance, diagonal elements represent variance of each random variable
	- $Conv(X_i,X_i)=Var(X_i)$
- Covariance matrix is symmetric, positive semi-definite

### Correlation
- Normalize the contribution of each variable in order to measure
only how much the variables are related, rather than being affected
by the scale of the separate variables



### Independence
- Two random variables $x$ and $y$ are independent if their probability
distribution can be expressed as a product of two factors
- If X,Y are independent, then
    - $p(x,y)=p(x)p(y)$
    - e.g. probability of coin flip
- Two random variables are conditionally independent given a random variable
$z$ if the conditional probability distribution over $x$ and $y$ factorizes
in this way for every value of $z$:

\begin{equation}
    \forall x \in x,y \in y, z\in z, p(x=x,y=y|z=z) = p(x=x|z=z)p(y=y|z=z)
\end{equation}

Note: The notions of covaraince and independence are related but distinct.
Related because two variables that are independent have zero covariance,
and two variables that have non-zero covariance are dependent.

2nd Note: It is possible for two variables to be dependent but have
zero covariance.

### Law of Total Probability
Discrete
- $\sum_xp(x)=1$
- $p(x)=\sum_yp(x,y)$
- $p(x)=\sum_yp(x|y)p(y)$

Continuous
- $\int p(x)dx=1$
- $p(x)=\int p(x,y)dy$
- $p(x)=\int p(x|y)(y)dy$

### Marginal Probability
- Sometimes we know the probability distribution over a set of
variables and want to know the probability distribution over
just a subset of them
- e.g. suppose we have discrete random variables $x$ and $y$
we know $P(x,y)$. We can find $P(x)$ with the sum rule:
    - $\forall x \in x, P(X=x) = \sum_y P(X=x, Y=y)$
- For continuous variables, we use integration instead of summation
    - $p(x) = \int p(x,y)dy$

### Chain Rule of Conditional Probability
- Any joint probability distribution over many random variables
may be decomposed into conditional distributions over only one
variable:

\begin{equation}
    P(x^{(1)}, ..., x^{(n)}) =  P(x^{(1)})\Pi^n_{i=2} P(x^{(i)} | x^{(1)}, ..., x^{(i)})
\end{equation}
- This is known as chain rule or product rule of probability

## Probability Distributions
### Bernoulli Distribution
- Distribution over a single binary random variable
- Controlled by a single parameter $\Phi \in [0,1]$ -> gives probability
of random variable being equal to 1

### Multinoulli Distribution
- Or categorical distribution is a distribution over a single dicrete
variable with $k$ different states where $k$ is finite.
- Special case of multinomial distribution
- parameterized over $p \in [0,1]^{k-1}$ where $p_i$ gives the probability
of the i-th state
- Used to refer to distributions over categories of objects
    - So no need to compute the expectation or variance of
    multinoulli-distributed random vars

### Gaussian Distribution
- Most common distribution over real numbers is the normal distribution
- Two parameters $\mu \in R$ and $\sigma \in (0, \infty)$ control it
    - $\mu$ gives the coordinate of the central peak (mean)
    - $\sigma$ is standard deviation

Q: Why are normal distributions a sensible choice in many cases?
First, many distributions we want to model are truly close to being
normal distributions. The central limit theorem shows that the sum of
many independent random variables is approximately normally distributed.
Secondly, out of all possible probability distributions with the same
covariance, the normal distribution encodes the maximum amount of uncertainty over the real numbers. We can think of it as being the one that inserts
the least amount of prior knowledge into a model

### Multivariate Normal Distribution
- The normal distribution generalizes to $R^n$
- The parameter $\mu$ still gives the mean though now it is vector-valued

### Exponential and Laplace Distributions
- In the context of deep learning, we often want a probability distribution
with a sharp point at $x=0$. To get this we use the exponential distribution

\begin{equation}
    p(x;\lambda) = \lambda 1_{x \geq 0}exp(-\lambda x)
\end{equation}
- Indicator function $1_{x \geq 0}$ to assign probability zero to all
negative values of x






















