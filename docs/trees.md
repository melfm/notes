# Classification and Regression Trees
## Decision trees
Set of splitting rules used to segment the predictor space and summarized in a tree. Tree-based methods are simple and useful for interpretatin.

### Prediction via Stratification of the Feature Space
1. Divide the predictor space - that is, the set of possible values for $X_1, X_2,...,X_p$ into $J$ distinct and non-overlapping regions $R_1, R_2,...,R_J$.
2. For every observation that falls into the region $R_j$, we make the same prediction, which is simply the mean of the response values for the training oversations in $R_j$.

So for example in Step 1, if you have two regions $R_1$ and $R_2$ and the response mean for first region is 10, given $x \in R_1$ it will predict 10.
You could divide these regions into any shape, such as high-dimensional rectangles or boxes.
The goal is to find boxes $R_1,...,R_J$ that minimize the RSS given by :

\begin{equation}
\sum_{j=1}^{J} \sum_{i \in R_j} {(y_i -\hat{y_{R_j}})}^2
\end{equation}
