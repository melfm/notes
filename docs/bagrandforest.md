# Bootstrap
A bootstrap sample is a sample with replacement with the same number of observations as the original.

# Bagging = Boostrap AGgregation
Make the predictor less reliant on a particular sample, this reduces variance.
This works well on learning algorithms such as trees since due to their high variance they are unstable.

# Bagging for classification
With $K$ classes, the bagged predictor is the class that receives the most votes :
\begin{equation}
\hat{G_{bag}}(x) = arg_k max \hat{f_{bag}}(x)
\end{equation}

Here the majority of votes is not used instead we average the probabilities from individual classifiers :
\begin{equation}
\hat{p_{bag}}(x) = \frac{1}{B}\sum^{B}_{b=1} \hat{p_b}(x)
\end{equation}
