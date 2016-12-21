# Backpropagation Numerical example

Assume the following network :

![Simple network with values](../images/backprop_simpl_net.png)

The goal is to optimize the weights so that the net can learn how to correctly map arbitrary input to outputs.

![Initial values](../images/simpl_net_init_vals.png)

Let's assume the above initial weights with the inputs as 0.05 and 0.1 and assume the desired output is 0.01 and 0.99.

## Forward pass
We start by feeding the values forward through the network.
A variable $z$ is defined as the total input to the hidden unit before the logistic nonlinearity.

\begin{align}
    z1 = (w1  x1 + w2  x2 + b1) \\
    z1 = (0.15 x 0.05 + 0.2 x 0.1 + 0.30) = 0.3275
\end{align}

We then apply the logistic activation function to get the output of the hidden layer 1 :

\begin{equation}
  h1 = \sigma (z1) = \frac{1}{1 + e ^ {- 0.3275}} = 0.5812 
\end{equation}

We repeat the same for $h2 = 0.5969$.

\begin{align}
  y1 = (w5  h1 + w6  h1 + b2)  \\
  y1 = (0.4 x 0.5812 + 0.45 x 0.5812) + 0.6 = 1.094 \\
  \hat{y1} = \sigma (y1) = 0.7491
\end{align}

Same for $out_y2 = 0.7703$.

## Total error
\begin{equation}
  E_{total} = \sum \frac{1}{2}(target - output)^2
\end{equation}

NB. The $\frac{1}{2}$ is just there to cancel the differentiation later on.

\begin{equation}
  E_y1 = \frac{1}{2}(t1 - \hat{y1})^2 = \frac{1}{2}(0.01 - 0.7491)^2 = 0.2731
\end{equation}

\begin{equation}
  E_y2 = \frac{1}{2}(0.01 - 0.7703)^2 = 0.289
\end{equation}

## Backward pass
Backpropagation updates each of the weights so that they cause the output to be closer to the target output, thereby minimizing the error for each output neuron and the network as a whole.

### Output layer
Consider $w5$. We want to know how much a change in $w5$ affects the total error : $\frac{\partial E_{total}}{\partial w5}$

Using the chain rule :

\begin{equation} 
\frac{\partial E_{total}}{\partial w5} = \frac{\partial E_{total}}{\partial \hat{y1}} \frac{\partial \hat{y1}}{\partial h1} \frac{\partial h1}{\partial w5} 
\end{equation}

We now calculate each piece in this equation.
First, how much the total error change w.r.t the output :

\begin{align}
    E_{total} = \frac{1}{2}(t1 - \hat{y1})^2 + \frac{1}{2}(t2 - \hat{y2})^2 \\
    \frac{\partial E_{total}}{\partial \hat{y1}} = 2 * \frac{1}{2} (t1 - \hat{y1})^{2-1} + 0 \\
    = -(t1 - \hat{y1}) = -(0.01 - 0.7491 ) = 0.7391
\end{align}

Next, how much output $ \hat{y1}$ changes w.r.t its total net input?
We are going to take partial derivative of the logistic function :

\begin{equation}
  \hat{y1} = \frac{1}{1 + e ^{-\hat{y1}}} \\
  \frac{\partial \hat{y1}}{\partial h1} = \hat{y1}(1- \hat{y1}) = 0.7391(1 - 0.7391) = 0.1928
\end{equation}

Finally, how much the total net output of $ \hat{y1}$ change w.r.t. $w5$?

\begin{align}
  \hat{y1} = w5 * out_{h1} + w6 * out_{h2} + b2 \\
  \frac{\partial \hat{y1}}{\partial w5} = 1  * out_{h1} * w5^{1-1} + 0 + 0 = 0.5932
\end{align}

Now we can put it all together :

\begin{equation} 
\frac{\partial E_{total}}{\partial w5} = \frac{\partial E_{total}}{\partial \hat{y1}} \frac{\partial \hat{y1}}{\partial h1} \frac{\partial h1}{\partial w5} 
\end{equation}

\begin{equation} 
\frac{\partial E_{total}}{\partial w5} = 0.7391 * 0.1928 * 0.5932 = 0.0845
\end{equation}

To decrease the error we subtract this value from the current weight multiplied by the selected learning rate (0.5) :

\begin{equation} 
    w5 = w5 - \alpha * \frac{\partial E_{total}}{\partial w5} = 0.4 - 0.5 * 0.0845 = 0.3578
\end{equation}

We then repeat this process to get the new weights, $w6 = 0.4078 $, $w7 = ? $ and $w8 = ? $ :

Now we need to conitnue the backpropagation, with the original weights of course.

### Hidden Layer
Now we calculate the new values for $w1$, $w2$, $w3$ and $w4$ :

![Hidden Layer backporpagation](../images/backprop_hiddenL.png)


\begin{equation} 
\frac{\partial E_{total}}{\partial w1} = \frac{\partial E_{total}}{\partial out_{h1}} \frac{\partial out_{h1}}{\partial net_{h1}} \frac{\partial net_{h1}}{\partial w1} 
\end{equation}


TBC



## Reference
This was taken from here : https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/
Just slight syntax and number changes.

