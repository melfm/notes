# Logistic Regression
- Used for classification into 2 classes. The two classes will be coded as 0 and 1.
- Define the probability that the event occurs $P(y = 1) = p$  then $E(y) = p$.

We would like to use a linear function to model $p$ as a function of $x-variables$.

\begin{equation}
f (p) = \beta_0 + \beta_1 x_1 + ... + \beta_p x_p
\end{equation}

We want $f()$ such that $f(p)$ covers the real line (-inf, +inf). One such function is the logit :

\begin{equation}
logit(p) = log \frac{p}{1-p}
\end{equation}

We solve for p:

\begin{align}
log \frac{p}{1-p} = \beta_0 + \beta_1x \\
p = \frac{e^{\beta_0 + \beta_1x}}{1 + e^{\beta_0+\beta_1x}}
\end{align}
