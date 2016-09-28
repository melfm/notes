#K-Nearest Neighbors
Many classifiers attempt to estimate the conditional distribution of Y given X, and then classify a given observation to the class with the highest estimated probability, KNN being one. KNN is memory-based and requires no model to fit.
,./Given a positive integer $K$ and a test observation $x_0$, the KNN classifier first identifies the $K$ points in the training data that are closest to $x_0$, represented by $\mathrm{N}_{0}$.
It then estimates the conditional probability for class $j$ as the fraction of points in $ \mathrm{N}_{0}$ whose response values equal $j$:

\begin{equation}
Pr(Y = j| X = x_0) = \frac{1}{K}\sum_{i \in \mathrm{N_0}} I(y_i = j).
\end{equation}

KNN applies Bayes rule and classifies the test observation $x_0$ to the class with the largest probability.
Clearly the choice of $K$ has a drastic effect. Usually $K = 1$ is overly flexible and finds patterns in the data that don't correspond to the Bayes decision boundary. This corresponds to a classifier that has low bias but very high variance and this is because it uses only one training point closest to the query point. As $K$ grows, the method becomes less flexible and produces a decision boundary that is close to linear. This corresponds to a low-variance but high-bias classifier. Similar to regression, there is no strong relationship between the training error rate and test error. With $K = 1$ the KNN training error rate is 0, but the test error may be quite high!

Think of finding the maximum probability as classifying by majority vote. Options when classification tires arise:
- Break tie at random
- Increase k until tie is broken
- Use 1NN as a tie breaker

Methods like cross-validation can help to estimate the best value of a tuning parameter.

## Variabe Standardization
We first standardize each of the features to have zero mean and variance 1 since it is possible that they are measured in different units. A typical standardization could be :
\begin{equation}
x^{std}_i = \frac{x_i - \bar{x}}{sd(x)}
\end{equation}
As computer scientists, we just take the range of [0,1], either is fine.


## Similarity
Any distance metric can be turned into a similarity metric. e.g.

\begin{equation}
s(x_0, x_1) = \frac{1 - d(x_0, x_1)}{d_{max}}
\end{equation}
where $d_{max}$ is the largest distance observed in the data. In text mining, $cosine(x_0,x_1)$ is also often used.



## Invariant Metrics and Tangent Distance
In some problems, the features are invariant under certain natural transformations. KNN can exploit such invariances by incorporating them into the metric used to measure the distances between objects. Consider the problem of MNIST classification. We wish to remove the effect of rotation in measuring distances between two digits of the same class. We could then generate variations of '3' say by applying rotations. Consider the set of pixel values of the orignal '3' and its rotate version. You can draw this as a one-dimensional curve, and through each image we draw the curve of the rotate version, this is called 'invariance manifolds'. Now instead of using the usual Euclidean distance, we use the shortest distance between the two curves. This distance is called 'invariant metric'. The limitations: difficult to calculate, secondly it allows large transformations that lead to poor performance, like taking 6 and rotating it which would be 9, hence need to restrict attention to small rotations.

The use of 'tangent distance' solves the above issues. The tangent can be computed by by estimating the direction vector from small rotations of the image and if you take a large rotation, the tangent image no longer looks like a 3 which removes the large transformations issue. To classify an image, we compute its invariant tangent line, find the closest line to it among the lines in the training set. Simpler way to achieve this? Just add rotated versions of images to the training set and then just use a standard KNN. Other transformations include translation (two direction), scaling (two direction), sheer and character thickness.

## Time Complexity
One obvious drawback of KNN is the computational load both in finding the neighbors and storing the entire training set in memory. With $N$ observations and $p$ predictors, it requires $Np$ operations to find the neighbors. There are faster algorithms for finding the nearest-neighbors. Reducing storage is more difficult. The idea is to isolate a subset of the training set that suffices for the prediction and throw away the rest. So you keep the training points that are near the decision boundaries and discard the far points from the boundaries.
