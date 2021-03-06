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

where $\hat{y_{R_j}}$ is the mean response for the training obervations within the jth box. It is computationally infeasible to consider every possible partition of the feature space into $J$ boxes. So we take a top-down greedy approach known as recursive binary splitting. It is greedy because at each step of the tree-building process, the best split is made at that particular step, rather than looking ahead and picking a split that will lead to a better tree in some future step.
To perform the recursive binary splitting, first select the predictor $X_j$ and the cutpoint $s$ such that splitting the predictor space into the regions ${X|X_j < s}$ and ${X|X_j \geq s}$ leads to the greatest possible reduction in RSS.
For any $j$ and $s$, we define the pair of half-planes

\begin{equation}
R_1(j,s) = {X|X_j < s} , R_2(j,s) = {X|X_j \geq s},
\end{equation}

and we seek the value of $j$ and $s$ that minimize the equation
\begin{equation}
\sum_{i:x_i \in R (j,s)} {(y_i -\hat{y_{R_j}})}^2 + \sum_{i:x_i \in R (j,s)} {(y_i -\hat{y_{R_j}})}^2
\end{equation}

So here we have two $\hat{y}_R$ which is mean response for the training observations in $R_1(j,s)$, and $R_2(j,s)$.
We repeat this process, looking for the best predictor and best cutpoint. However this time instead of splitting the entire predictor space, we split one of the two previously identified regions. This process is repeated until a stopping criterion is reached.

### Tree Pruning
The process above might yield a good prediction on the training set but likely overfits the data due to the resulting complex tree.
A smaller tree might lead to a lower variance and better interpretation at the cost of a little bias.
You can do this -> use thresholding to build the tree so long but then this might give you a short-sighted tree since a seeminly worthless split might be followed by a good split! So a better way is this : grow a very large tree and then prune it back in order to obtain a subtree. The goal is to select a subtree that leads to the lowest test error rate.
Given a subtree we can estimate its stest error using cross-validation approach. But again estimating the cross-validation for every possible subtree is computationally expensive. Cost complexity pruning (aka weakest link pruning) gives a better way to do this.
