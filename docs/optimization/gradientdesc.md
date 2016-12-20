# Gradient Descent

Say we have chosen an appropriate class of $F$ functions. Finding the global minimizer
of the training error for most interesting choices of $F$ is $NP$-hard, but in practice there are 
many choices of smoothly-parameterized $F$s that are easy to optimize with gradient methods.

Let the function $F_{\theta} \in F$ be a differentiable parameterization of $F where $\theta \in R^{|\theta|}$
and $|\theta|$ is the number of parameters. Assume the loss $L$ is a differentiable function of its arguments.

\begin{equation}
  Train_S(\theta) \equiv Train_S(f_{\theta}) = E_{(x,y)\approx S} [L(f(\theta);y)]
\end{equation}

is differentiable. If $f_{\theta}(x)$ is easy to compute, then it immediately follows that the training error
$Train_S(\theta)$ and its derivative $\bigtriangleup Train_S(\theta)$ can be computed at the cost 
of $|S|$ evaluations of $f_{\theta}(x)$ and  $\bigtriangleup f_{\theta}(x)$.
In this setting, we can use Gradient Descent (GD) which is a greedy method for minimizing arbitrary
differentiable functions.
Given a function $F(\theta)$, GD operates as follows :


![Gradient Descent](../images/GD.png)

The learning rate $\epsilon$ is a tunable problem-dependent parameter that has a considerable effect
on the speed of the optimization.

Stochastic Gradient Descent (SGD) is an important generalization of GD that is well-suited for machine learning 
applications. Unlike the standard GD, which computes $\bigtriangledown Train_S(\theta)$ on the entire
training set $S$, SGD uses the unbiases approximation $\bigtriangledown Train_s(\theta)$, where $s$
is a randomly chosen subset of the training set $S$. The "minibatch" $s$ can consist of as little as
one training case, but using more training cases if more cost-effective.
SGD tends to work better than GD on large datasets where each iteration of GD is very expensive.
Batch GD is also trivially parallelizable.

# Momentum
Momentum methods use gradient info to update the parameters in a direction that is more effective than
steepest descent by accumulating speed in directions that consistently reduce the cost function.
Formally, a momentum method maintains a velocity vector $v_t$ which is updated as follows:

\begin{align}
  v_{t + 1} = \mu v_t - \epsilon \bigtriangledown F(\theta_t) \\
  \theta_{t+1} = \theta_t + v_{t + 1}
\end{align}

The momentum decay coefficient $\mu \in [0,1)$ controls the rate at which old gradients are discarded.
Its physical interpretation is the "friction" of the surface of the objective function, and its 
magnitude has an indirect effect on the magnitude of the velocity.

Side Note: A variant of momentum is known as Nesterov's accelerated gradient.


