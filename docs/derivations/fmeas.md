# F-measure


Show the following equation for the micro-average F-measure holds 


\begin{align}
	\frac{2 \sum^{n}_{i=1} \sum^{L}_{j=1} I \{y_j =1 \& \hat{y_j} = 1\}}{\sum^{n}_{i=1} \sum^{L}_{j=1} I \{y_j = 1 \} + \sum_{i=1}^{n} \sum_{j=1}^{L} I \{\hat{y_j} = 1 \}}
	= \frac{2TP}{2TP + FN + FP}
\end{align}

where $y_{ij} \in \{0,1\}$; $ i = 1, ..., n, j = 1,...,L$, $n$ is the number of observations and $L$ the number of labels.

First, we are going to decompose the following :

\begin{align}
\frac{2TP}{2TP + FN + FP}
\end{align}

Given :
\begin{align}
P = \frac{TP}{TP + FP}
\end{align}

\begin{align}
R = \frac{TP}{TP + FN}
\end{align}

Where $P$ is precision and $R$ is recall.

The traditional F-measure is the harmonic mean of the precision and recall:

\begin{align}
F_1 = 2. \frac{1}{ \frac{1}{R} + \frac{1}{P}  } = 2.\frac{P.R}{P + R} 
\end{align} 

Substituting the $P$ and $R$ :

\begin{align}
2\times \frac{1}{ \frac{1}{\frac{TP}{TP + FN}} + \frac{1}{  \frac{TP}{TP + FP}    }  } \\
= 2 \times \frac{1 }{\frac{TP + FP}{TP} + \frac{TP + FN}{TP} } \\
 2 \times \frac{1}{   \frac{2 TP + FN + FP}{TP}} \\
 = \frac{2TP}{2TP + FN + FP}
\end{align} 


Now given the lable $j$ the formula for P is :

\begin{align}
P = \frac{\sum^{n}_{i=1} I \{y_j = 1 \& \hat{y_j} = 1\}    }{\sum_{i=1}^{n} \{\hat{y_j} = 1\}}
\end{align} 


Similarly R :

\begin{align}
R = \frac{\sum^{n}_{i=1} I \{y_j = 1 \& \hat{y_j} = 1\}    }{\sum_{i=1}^{n} \{y_j = 1\}}
\end{align} 

Therefore F-measure :

\begin{align}
F-measure = 2. \frac{P.R}{P + R} \\
= \frac{2 \sum^{n}_{i=1} I \{y_j = 1 \& \hat{y_j} = 1\} }{\sum_{i=1}^{n} \{\hat{y_j} = 1\} +\sum_{i=1}^{n} \{y_j = 1\} }
\end{align} 

We can then extend this formula to multi-label so we consider the predictions from all instances across all labels :

\begin{align}
 \frac{2   \sum^{n}_{i=1} \sum_{j=1}^{L} I \{y_j = 1 \& \hat{y_j} = 1\} }{\sum_{i=1}^{n} \sum_{j=1}^{L} \{\hat{y_j} = 1\} +\sum_{i=1}^{n} \sum_{j=1}^{L} \{y_j = 1\} }
\end{align} 

Therefore :

\begin{align}
\frac{2 \sum^{n}_{i=1} \sum^{L}_{j=1} I \{y_j =1 \& \hat{y_j} = 1\}}{\sum^{n}_{i=1} \sum^{L}_{j=1} I \{y_j = 1 \} + \sum_{i=1}^{n} \sum_{j=1}^{L} I \{\hat{y_j} = 1 \}}
= \frac{2TP}{2TP + FN + FP}
\end{align}
