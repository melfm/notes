# Numerical Computation

## Poor Conditioning
- Refers to how rapidly a function changes w.r.t small changes to its input
- Functions that change rapidly when their inputs are perturbed slightly
can be problematic for scientific computation because of rounding errors

## Gradient-Based Optimization
- Optimization refers to either minimizing or maximizing some function
$f(x)$ by altering $x$
- We denote the value that minimizes or maximizes a function with a superscript $*$ e.g.  $x^{\ast} = argmin f(x)$
- Suppose we have a function $y = f(x)$.
    - The derivative is useful for minimizing a function because it tells how to change $x$ in order to make a small improvement in $y$.
    - We know $f(x - \epsilon sign(f^{'}(x)))$ is less than $f(x)$
    - We can thus reduce $f(x)$ by moving $x$ in small steps
    - This is called gradient descent
- Often want to minimize functions that have multiple inputs
    - $f : R^n \rightarrow R$
    - For the ''minimization'' to make sense, there must still be only one scalar output
    - For functions with multiple inputs, we use ${\textbf{partial derivatives}}$


- The partial derivative $ \frac{\partial }{\partial x_i} f(x)$ measures how $f$ changes as only the variable $x_i$ increases at point $x$
- The $\textbf{gradient}$ generalizes the notion of derivative to the case where the derivative is w.r.t a vector
    - The gradient of $f$ is the vector containing all of the partial derivatives, denoted $\triangledown_xf(x)$
    - Element $i$ of the gradient is the partial derivative of $f$ w.r.t. $x_i$

## Beyond the Gradient: Jacobian and Hessian Matrices
- Sometimes we need to find all of the partial derivatives of a function whose input and output are both vectors
- The matrix containing all such partial derivatives is known as a $\textbf{Jasobian matrix}$
    - If we have a function $f: R_m \rightarrow R_n$, then the Jacobian matrix $J \in R^{nxm}$ of $f$ is defined such that $J_{i,j} = \frac{\partial }{\partial_{x_j}} f(x)_i$
- Sometimes we want the derivative of a derivative (second derivative)
    - For a function $f: R^n \rightarrow R$, the derivative w.r.t. $x_i$ of the derivative of $f$ w.r.t. $x_j$ is denoted as $\frac{\partial^2}{\partial x_i \partial x_j}$
    - Recall in a single dimension $\rightarrow$ $\frac{d^2}{dx^2} f$ denoted by $f^{''}(x)$
- The second derivative tells us how the first derivative will change as we vary the input
    - Important because it says whether a gradient step will cause as much of an improvement as we would expect based on the gradient alone
- Think of second derivative as measuring $\textbf{curvatures}$


- When the function has multiple input dimensions, there are many second derivatives
- These derivatives can be collected together into a matrix called the $\textbf{Hessian matrix}$

\begin{equation}
    H(f)(x)_{i,j} = \frac{\partial^2}{\partial x_i \partial x_j}f(x)
\end{equation}

- Equivalently, the Hessian is the Jacobian of the gradient
- Because the Hessian matrix is real and symmetric we can decompose it into a set of real eigenvalues and an orthogonal basis of eigenvectors
- The second derivative in a specific direction represented by a unit vector $d$ is given by $d^T Hd$
    - When $d$ is an eigenvector of $H$ the second derivative in that direction is given by the corresponding eigenvalue

### Newton's Method
- We can use info from the Hessian matrix to guide the search
- The simplest method is Newtons which is based on using a second-order Taylor series expansion to approximate $f(x)$
- When $f$ is a positive definite quadratic function, Newton's method jumps to the minimum of the function directly
    - This is useful near a local minimum, but it can be harmful property near a saddle point


- In the context of deep learning, these optimization algorithms lack guarantee
- To gain some guarantee, we can restrict ourselves to functions that are either $\textbf{Lipschitz continuous}$ or have Lipschitz continuous derivatives
    - This is a function $f$ whose rate of change is bounded by a Lipschitz constant

\begin{equation}
    \forall x, \forall y, |f(x) - f(y)| \leq \ell ||x-y||_2
\end{equation}
- Lipschitz continuity is a fairly weak constraint
- The most successful field of specialized optimization is $\textbf{convex optimization}$
    - They can provide more guarantees by making stronger restrictions


