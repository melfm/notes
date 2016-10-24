# Bagging, Random Forests, Boosting
All use trees as building blocks to construct more powerful prediction models.

# Bootstrap
A bootstrap sample is a sample with replacement with the same number of observations as the original.

## Bagging
\text{Bootstrap aggregation}, or \textit{bagging} is a method for reducing variance of a learning method.
It aims to make the predictor less reliant on a particular sample, this reduces variance.
This works well on learning algorithms such as decision trees since they suffer from high variance. This means that if we split the training data into two parts at random and fit a decision tree to both halves, the results we get could be quite different.
In contrast, an algorithm with low variance will yield similar results of applied repeatedly.
However destroys the interpretability of trees.

## Bagging for classification
With $K$ classes, the bagged predictor is the class that receives the most votes:
\begin{equation}
\hat{G_{bag}}(x) = arg_k max \hat{f_{bag}}(x)
\end{equation}

Here the majority of votes is not used instead we average the probabilities from individual classifiers:
\begin{equation}
\hat{p_{bag}}(x) = \frac{1}{B}\sum^{B}_{b=1} \hat{p_b}(x)
\end{equation}

Summary: Bagging involves creating multiple copies of the original training data using bootstrap, fitting a separate decision tree to each copy and then combining all of the trees in order to create a single predictive model.

# Random Forests
- Build $m$ trees from $m$ boostrapped samples
- Look at the trees, for each split, find the best split among $p$ variables.
- Look at the forests, for each split, find the best split among a random subset of $p$ variables (e.g. sqrt(p) variables) recursively. So for each split choose a different random subset.

Note : In building a random forest at each split the algorithm is not allowed to consider a majority of the available predictor. This works well because it means on average the splits don't even consider the strong predictor and this gives other predictors more of a chance. This process is known as \textit{decorrelation}, making the average of the resulting tree less variable and hence more reliable.

## Out of bag samples
Each bootstrap sample (one bag) on average uses 2/3 of their observations leaving about 1/3 unused.
The OOB observation can be used to estimate the test error. So we don't need a train/test split.

# Boosting
Similar to bagging but the trees are grown sequentially. Each tree is grown using info from prev tree. No bootstrap involved, each tree is fit on a modified version of the original data set.

## Adaboost
Earliest boosting alg for 2 classes only.
A weak classifier is one whose error rate is only slightly better than random guessing. e.g. tree stump (a tree with a single split)
Combine many weak classifiers to produce one powerful 'committe'. The weak classifiers do not have equal weight.
For classification into two categories labele {-1,1},
\begin{equation}
G(x) = sign (\sum^{M}_{m=1}\alpha_m G_m(x))
\end{equation}
where $G_m(x)$ is a weak learner and $\alpha_m$ are weights.

Adaboost algorithm, ommitted here but basically we initialize the weights, for $M$ number of classifiers, we do the fitting and compute the error and whatnot, upate the weights and in the end for the final classification we take a sum of these classifiers.
## Updating the weights
\begin{equation}
w_i = w_i exp[\alpha_mI(y_i \neq G_m (x_i))]
\end{equation}

So if classified correcty, the weight of an observation remains unchanged,
If classified incorrectly, the weight is increased by multiplying with $exp(alpha_m)$, where alpha varies with the degree of misclassification.

# Forward Stagewise Additive Modeling
Generally boosting fits an additive model
\begin{equation}
f(x) = \sum^{M}_{m=1} \beta_mb(x; \gamma_m)
\end{equation}
$b()$ are basis functions i.e. weak learners, gamma tunes the basis function.

Here we take the following :
\begin{equation}
G(x) = sign (\sum^{M}_{m=1}\alpha_m G_m(x))
\end{equation}

$x$ is the input data; ${\beta_m, \gamma_m}$ are model parameters;
$b_m(x;\gamma_y)$ are any arbitrary function of $x$.
We estimate $b_m(x;\gamma_y)$ using say some loss function which measures prediction errors over training data.
The problem is directly optimizing such loss function is difficult for all $M$ iterations simultaneously.
So instead we optimize over one single base function and at each iteration we find the best fit to the 'residual' from the previous iteration. The basic idea is sequentially adding new base functions without changing the parameters that have been added.

AdaBoost is essentially a forward stagewise additive model where the objective function is the exponential loss.
\begin{equation}
L(y, f(x)) = exp(-tf(x))
\end{equation}
Based on this boosting variants can be developed so we can change base or loss function.
Depending on what loss function we pick, we may penalize incorrect classifications more heavily for instance.
Some examples are the following functions :

- Misclassification  $I(sign(f) \neq y)
- Exponential  $exp(-yf)$
- Binom deviance $log(1+exp(-2yf))
- Squared error $(y - f)^2$
- Support vector  $max(0,1 - yf)$

If you draw these and compare their robustness.
