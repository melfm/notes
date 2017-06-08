# Probability

Probability theory provides means of quantifying uncertainty
and axioms for deriving new uncertain statements

## Random variable
A random variable is a variable that can taken on different
values randomly. Random variable may be discrete or continuous.
### Discrete random variable
- Has a finite or countably finite number of states
- Note: these states are not necessarily integers; they can also
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

### Joint probability
- Probability mass function can act on many variables at the same time
- $P(X = x, Y= y)$ denotes the probability that $X =x $ and $ Y=y$
- $p(X=x \quad and \quad Y=y) = p(x,y)$
- e.g. P of clouds and rain today

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

### Conditional Probability
- Probability of some event, given that some other event has happened
Probability of x given y -> $p(X=x|Y=y)=p(x|y)$
- Formula:
    - $P(Y=y| X=x) = \frac{P(Y=y,X=x)}{P(X=x)}$
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





















