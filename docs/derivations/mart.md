# MART Algorithm

Derive the MART algorithm for the Poisson distribution


Poisson distribution:
\begin{align}
	Y_i \sim \frac{\lambda(x_i)^{y_i}exp(-\lambda(x_i))}{y_i!}
\end{align}

Poisson regression:
\begin{align}
	log(\lambda(x_i)) = f(x_i)
\end{align}

a) Derive the initialization constant $f_0$ of the MART algorithm:

Let $Y = (Y_1, Y_2, ...,Y_n)$ be i.i.d. observations from a Poisson distribution with unknown parameter $\lambda$. The likelihood function is :

\begin{align}
	L(\lambda, y) = \prod_{i=1}^{n} f(x_i; \lambda) \\
	=\prod_{i=1}^{n} \frac{\lambda(x_i)^{y_i}e^{(-\lambda(x_i))}}{y_i!} \\
	=\frac{\lambda^{\sum_{i=1}^{n}y_i}e^{n(-\lambda(x_i))}}{y_i!}
\end{align}

By diferentiating the log of this function with respect to $\lambda$ and ignoring the constant term that does not depend on $\lambda$, we get the Poisson loglikelihood function
\begin{align}
	l(\lambda; y) = \sum_{i=1}^{n}(y_i log(\lambda(x_i)) - \lambda(x_i))
\end{align}


Now because we fit the model sequentially, we rewrite the likelihood as a function of $f(x)$


\begin{align}
l(y) \propto \sum_{i=1}^{n}(y_i f(x_i) - e^{f(x_i)})
\end{align}



Here gamma is the constant that minimzies the loss. Note that $f_0 = \gamma$.
\begin{align}
f_0(x) = arg \underset{\gamma} min \sum_{i=1}^{n} Loss(y_i; \gamma)\\
= arg \underset{\gamma}  max \sum_{i=1}^{n} (y_i \gamma - e^{\gamma})
\end{align}


Now we set the first derivative to zero to find the maximum :


\begin{align}
l(y) \propto \sum_{i=1}^{n}(y_i \gamma - e^{\gamma})
\end{align}


\begin{align}
 0 = \sum_{i=1}^{n} [ y_i - e^ \gamma]  \\
 \sum_{i=1}^{n} y_i = n e^{\gamma} \\
 \frac{1}{n} \sum_{i=1}^{n} y_i = e^\gamma \\
 \gamma = log \big(\frac{1}{n} \sum_{i=1}^{n} y_i \big)
\end{align}


b) Compute pseudo residuals :


\begin{align}
r_{im} = - \bigg[\frac{\partial l(y_i, f(x_i))}{\partial f(x_i)} \bigg]_{f=f_{m-1}}\\
= \frac{\partial \bigg[\sum_{i=1}^{n} \big[y_i f(x_i) - e^{f(x_i)} \big] \bigg]}{\partial f(x_i)}\\
= \sum_{i}^{} \bigg[ y_i - e^{f(x_i)} \bigg]
\end{align}


c) State the step of fitting a tree, be specific about the type of tree being fitted :

Fit regression tree :
This step involves finding the new split which involves maximization over which variable to split on and which value to split on. Here we are taking one split. And in this case, we are fitting tree to residuals which are continuous so essentially fitting a regression tree.



d) For each terminal node, compute fitted values.
Fitted value in leaf $j$ of iteration $m$ is a constant :

\begin{align}
\gamma_{jm} = arg \underset{\gamma}min \sum_{x_i \in R_{jm}}^{} Loss(y_i; f_{m-1}(x_i) + \gamma)
\end{align}

This minimization is different than the initialization because $L$ is a function of not just gamma but :

\begin{align}
f_{m-1}(x_i) + \gamma
\end{align}

Algebraic Minimization :

\begin{align}
\gamma_{jm} = arg \underset{\gamma}min \sum_{x_i \in R_{jm}}^{} Loss (y_i; f_{m-1}(x_i) + \gamma)
\end{align}

\begin{align}
 l = \sum_{i=1}^{n} \big[y_i(f_{m-1}(x_i) ) - e^{f_{m-1}(x_i) + \gamma} \big]\\
 \frac{\partial l}{\partial \gamma} = \sum_{i=1}^{n} \bigg[ y_i - e^{f_{m-1}(x_i) + \gamma } \bigg]
\end{align}


Set the derivative to zero

\begin{align}
0 = \sum_{i=1}^{n} \bigg[ y_i - e^{f_{m-1}(x_i)+\gamma } \bigg]
\end{align}



THIS IS WRONG, IT CAN BE SOLVED in close form!!!!

\wrong{This cannot be solved for gamma in closed form, hence we use a numerical optimization. 
The newton-Raphson method for iteratively maximizing a function requires derivatives of the function
evaluated at an initial guess:}

\begin{align}
 f_m = f_{m-1} - l^\prime(f_{m-1})/ l''(f_{m-1}) 
\end{align}

Gamma represents one iteration update of the Newton-Raphson method hence :

\begin{align}
	\gamma = -l'(f_{m-1}) / l'' (f_{m-1})
\end{align}


For calculating the residuals, we had already computed :

\begin{align}
	l'(f_{m-1}) = \sum_{i} (y_i - p_i)
\end{align}

where $p(x_i) = e^{f_{m-1}(x_i)}$

Therefore

\begin{align}
\frac{\partial l^2}{\partial \gamma^2} = \sum_{i=1}^{n} \bigg[o - e ^{f_{m-1}(x_i)}\bigg]
\end{align}


\begin{align}
= - \frac{\sum_{i=1}^{n} \bigg[ y_i - e^{f_{m-1}(x_i)}    \bigg]}{ \sum_{i=1}^{n} \bigg[- e ^{f_{m-1}(x_i)}\bigg]}   \\
= \frac{\sum_{i=1}^{n} \bigg[ y_i - e^{f_{m-1}(x_i)}    \bigg]}{ \sum_{i=1}^{n} \bigg[e ^{f_{m-1}(x_i)}\bigg]}  
\end{align}


e) State the update stage. We just calculated one step of iteration and updated $f_m$. We need to repeat this for $m$ iterations.

Update $f_m = f_{m-1} +$ fitted values.

Note: Each observation falls into a leaf and $f_{m-1}$ is the fitted constant in that leaft 
