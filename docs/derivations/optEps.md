Problem : I don't remember the question :D


In order to demonstrate the optimal learning rate derivation, we are going to exploit the following properties:

A gradient of an error function E(w) is a column vector of partial derivatives with respect to each of the parameters, w :

\begin{equation}
    g = \nabla E(w) = \frac{\partial E}{\partial w} = [\frac{\partial E}{\partial w1} \frac{\partial E}{\partial w2} \dots \frac{\partial E}{\partial wn} ]^T
\end{equation}

One important property of gradient vector is its local direction towards the steepest ascent. Hence the negative gradient shows the steepest descent. Given the current point w(k), the next point w(k+1) is obtained by a one-dimensional search in the direction of \textit{-g(w(k))}  :
\begin{equation}
    w(k+1) = w(k) - \eta g(w(k))
\end{equation}


If we apply the first-order gradient method, the convergence can be very slow. The most common improvement is using the second derivatives that defines the curvature of the function. When there are two or more unknown weights, an error function is a hyper-surface E(w), and we must calculate the corresponding (N,N) symmetric Hessian matrix. The advantage of second-order method is that it finds the global minimum, as opposed to the first-order method which finds local minimum.

Here we use the first-order method, using the properties of the chain rule defined below to derive optimal \(\eta\). In general:

\begin{equation}
   \frac{dz}{dx} = \frac{dz}{dy} . \frac{dy}{dx}
\end{equation}


For the special case where A is a symmetric matrix and x is a vector, the scalar
\(\alpha\) is :


$$\alpha = {x^TAx}$$

then
\begin{equation}\label{eq1}
\frac{\partial \alpha}{\partial x} = 2*x^TA
\end{equation}

The error function E(w) is defined as:

\begin{equation}
E(w(k)) = \frac{1}{2}w^TQw
\end{equation}


We are going to use property \ref{eq1} to denote the partial derivative term as follows : 

\begin{equation}
\frac{\partial E}{\partial w} = w^TQ
\end{equation}

* Note how the fraction term cancels out with the 2 in the derivative term.

Let \textit{d} denote the current direction, which is the negative of the gradient : 

\begin{equation}
    d = - \nabla E(w(k)) = -Qw
\end{equation}

Now to compute the next iteration of the steepest descent algorithm, $\eta$ being the generic step-length :

\begin{align}
    E(w(k)+\eta d) &= \frac{1}{2}(w + \eta d)^TQ(w + \eta d) \\
	&= \frac{1}{2}(w^TQw) + \frac{1}{2} \eta d^T Qw + \frac{1}{2} \eta Qw^Td + \frac{1}{2} \eta_{}^{2} d^TQd \\
    &= \frac{1}{2}(w^TQw) + (\frac{1}{2} \eta d^T d + \frac{1}{2} \eta d^Td) + \frac{1}{2} \eta_{}^{2} d^TQd \\
     &= \frac{1}{2}(w^TQw) + \eta d^TQw + \frac{1}{2} \eta_{}^{2} d^TQd \\
     &= E(w(k)) - \eta d^Td + \frac{1}{2} \eta_{}^{2} d^TQd
\end{align}

Note that in step(7) we replaced \textit{Qw} with \textit{d} which negates the expression. We also made use of the fact that $$Q = Q^T$$.


Optimizing the value of $\eta$ i.e. taking the partial derivative with respect to $\eta$ yields:

\begin{equation}\label{eq2}
\frac{\partial E}{\partial \eta} = \eta d^TQd - d^T d 
\end{equation}

By setting equation (\ref{eq2}) to 0 and solving for  \(\eta\):

\begin{equation}\label{eq3}
\eta = \frac{d^Td}{d^TQd}
\end{equation}

Now we substitute $d$ back in to the equation :

\begin{equation}
 = \frac{Qw^TQw}{Qw^TQQw} = \frac{w^TQ^2w}{w^TQ^3w}
\end{equation}
