# Linear model for regression

## Overview
- Predict the value of one or more continuous target variables $t$ given the value of a D-dimensional vector $x$ of input variables. 
- An example is polynomial curve fitting which is a specific example of a broad class of functions called linear regression models.
- Share the property of being linear functions of the adjustable parameters.
- We can obtain a more useful class of functions by taking linear combinations of a fixed set of nonlinear functions of the input variables, known as $basis$ functions.
- From a probabilistic perspective, we aim to model the predictive distribution $p(t|x)$ because this expresses our uncertainty about the value of $t$ for each value of $x$. From this conditional distribution we can make predictions of $t$ for new values of $x$.

## Linear Basis Function Models
- Simplest model involves a linear combination of the input variables

\begin{equation}
	y(x,w) = w_0 + w_1x_1 + ... + w_Dx_D
\end{equation}

where $x=(x_1,...,x_D)^T$.
- This is linear regression.
- Linear function of the input and hence imposes significant limitations on the model.
- Extend it by considering linear combinations of fixed nonlinear functions of the input variables of the form,

\begin{equation}
	y(x,w) = w_0 + \sum_{j=1}^{M-1} w_j \phi(x) = w^T(x)
\end{equation}

- Typically use some form of fixed pre-processing or feature extraction.
- By using nonlinear basis function, we allow the func $y(x,w)$ to be a nonlinear function of the input vector $x$.

