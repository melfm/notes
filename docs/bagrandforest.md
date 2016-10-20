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
With $K$ classes, the bagged predictor is the class that receives the most votes :
\begin{equation}
\hat{G_{bag}}(x) = arg_k max \hat{f_{bag}}(x)
\end{equation}

Here the majority of votes is not used instead we average the probabilities from individual classifiers :
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

## Boosting for classification
Combine many weak classifiers to produce one powerful 'committe'.
For classification into two categories labele {-1,1{,
\begin{equation}
G(x) = sign \Bigg{(\sum^{M}_{m=1}\ alpha_m G_m(x))}
\end{equation}
where $G_m(x)$ is a weak learner and $\alpha_m$ are weights.

## Adaboost
Earliest boosting alg for 2 classes only.

# Forward Stagewise Additive Modeling
Generally boosting fits an additive model
\begin{equation}
f(x) = \sum^{M}_{m=1} \beta_mb(x; \gamma_m)
\end{equation}
$b()$ are basis functions i.e. weak learners, gamma tunes the basis function.

TBC
