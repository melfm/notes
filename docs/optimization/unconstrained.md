# Unconstrained Optimization Techniques
Consider a cost function $E(w)$ that is continuously differentiable with some unknown weight (parameter) vector $w$.
The function $E(w)$ maps the elements of $w$ into real numbers. It is a measure of how to choose the weight (parameter) vector $w$ of an adaptive filtering algorithm so that it behaves in an optimum manner. We want to find an optimal solution $w^*$ that satisfies the condition :

\begin{equation}
E(w^{*}) \leq E(w)
\end{equation}

This means we need to solve an unconstrained optimization problem, stated as :

 Minimize the cost function E(w) with respect to the weight vector w

The necessary condition for optimality is :
\begin{equation}
\bigtriangledown E(w^*) = 0
\end{equation}

where $\bigtriangledown$ is the gradient operator.

