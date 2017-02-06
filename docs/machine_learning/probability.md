# Probability

## Discrete random variable
- X denotes a random variable
- X can take on a countable number of values
	- $X \in {x_1,...,x_n}$
- The probability that X takes on a specific value
	- $P(X = x_i)$ or $p(x_i)$

## Continuous Random Variable
- X takes on a value in a continuum
- Probability density function, $p(x)$
- Evaluated over finite intervals of the continuum
	- $p(x \in (a,b)) = \int_a^b p(x)dx$

## Measures of Distributions

- Mean (expected value of a random variable)
	- $\mu = E[X]$
	- $\mu = \sum_{i=1}^n x_i p(x_i)$ discrete case
	- $\mu = \int xp(x)dx $ continuous case
- Variance (Measure of variability of a random variable)
	- $Var(X) = E[(X - \mu)^2]$
	- $Var(X) = \sum_{i=1}^n (x_i - \mu)^2 p(x_i)$ discrete case
	- $Var(X) = \int (x - \mu)^2 p(x)dx$
- Square root of variance is standard deviation, $\sigma ^2=Var(X)$

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
Probability of x and y:
- $p(X=x \quad and \quad Y=y) = p(x,y)$	
- e.g. P of clouds and rain today

### Independence
If X,Y are independent, then
- $p(x,y)=p(x)p(y)$
- e.g. probability of coin flip

### Conditional Probability
Probability of x given y -> $p(X=x|Y=y)=p(x|y)$
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

### Law of Total Probability
Discrete
- $\sum_xp(x)=1$
- $p(x)=\sum_yp(x,y)$
- $p(x)=\sum_yp(x|y)p(y)$

Continuous
- $\int p(x)dx=1$
- $p(x)=\int p(x,y)dy$
- $p(x)=\int p(x|y)(y)dy$





















