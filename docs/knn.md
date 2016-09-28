#K-Nearest Neighbors
Many classifiers attempt to estimate the conditional distribution of Y given X, and then classify a given observation to the class with the highest estimated probability, KNN being one. Given a positive integer $K$ and a test observation $x_0$, the KNN classifier first identifies the $K$ points in the training data that are closest to $x_0$, represented by $\mathrm{N}_{0}$.
It then estimates the conditional probability for class $j$ as the fraction of points in $ \mathrm{N}_{0}$ whose response values equal $j$:

\begin{equation}
Pr(Y = j| X = x_0) = \frac{1}{K}\sum_{i \in \mathrm{N_0}} I(y_i = j).
\end{equation}

KNN applies Bayes rule and classifies the test observation $x_0$ to the class with the largest probability.
Clearly the choice of $K$ has a drastic effect. Usually $K = 1$ is overly flexible and finds patterns in the data that don't correspond to the Bayes decision boundary. This corresponds to a classifier that has low bias but very high variance. As $K$ grows, the method becomes less flexible and produces a decision boundary that is close to linear. This corresponds to a low-variance but high-bias classifier. Similar to regression, there is no strong relationship between the training error rate and test error. With $K = 1$ the KNN training error rate is 0, but the test error may be quite high!
