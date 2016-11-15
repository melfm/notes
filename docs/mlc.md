# Multi-label Classification

Evaluation Metrics:
## Hamming loss
- Here we have more than one response variable :

\begin{equation}
 Hamming_loss = 1- \frac{1}{L} \sum^{L}_{j=1} I{y_i = \hat{y_j}
\end{equation}

Hamming loss counts the percentage of incorrect labels. No attention is paid to whether all labels of an obvervation are predicted correctly.

## 0/1 loss
loss is 0 if all predicted labels match the true labels and 1 otherwise

\begin{equation}
0/1 loss = I {y != \hat{y}}
\end{equation}

$I$ is the indicator variable, and $y = (y_1, y_2, ..., y_L)^t

## F-measure
As $y$ is an L-dimensional vector, we can use the micro-averaged F-measure.
\begin{equation}

micro-averaged F-measure = \frac{   2 \sum^{L}_{j=1} I {y_i =1 and \hat{y_j} = 1}    }{\sum^{L}_{j=1} I{y_i = 1} + \sum^{L}_{j=1} I{\hat{y_i}=1}}
\end{equation}


