# Unconstrained Optimization Techniques
Consider a cost function $E(w)$ that is continuously differentiable with some unknown weight (parameter) vector $w$.
The function $E(w)$ maps the elements of $w$ into real numbers. It is a measure of how to choose the weight (parameter) vector $w$ of an adaptive filtering algorithm so that it behaves in an optimum manner. We want to find an optimal solution $w^*$ that satisfies the condition :

\begin{equation}
E(w^{*}) \leq E(w)
\end{equation}

This means we need to solve an $unconstrained optimization problem$, stated as :

\textit{ Minimize the cost function E(w) with respect to the weight vector w}

The necessary condition for optimality is :
\begin{equation}
\bigtriangledown E(w^*) = 0
\end{equation}

where $\bigtriangledown$ is the gradient operator.

## Method of Steepest Descent
Here the successive adjustements applied to the weight vector $w$ are in the direction of the steepest descent, that is direction opposite to the gradient vector $\bigtriangledown E(w)$.

The steepst descent algorithm is formally described by :
\begin{equation}
w(n + 1) = w(n) - \eta g(n) 
\end{equation}

where $\eta$ is called the stepsize or learning-rate parameter and $g(n)$ is the gradient vector evaluated at the point $w(n)$. In going from iteration $n$ to $n + 1$ the algorithm applies the correction :
\begin{equation}
\bigtriangleup w(n) = w(n + 1) - w(n) = - \eta g(n)
\end{equation}

Think of this as an error-correction rule. The method of steepest descent converges slowly and $\eta$ has a profound influence on its convergence.
