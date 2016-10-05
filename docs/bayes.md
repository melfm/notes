# Bayesian Classifier
In theory we would like to predict qualitative response using the Bayes classifier. But for real data, we don't know the conditional distribution of Y given X and so computing the Bayes classifier is impossible. The Bayes classifier serves as an unattainable gold standard against which to compare other methods.

Some notation :
- Density is $f_k(x) = P(X = x| Y=k)
- Prior probability of class k is $\pi_k$

# Naive Bayes
Naive Bayes methods are a set of supervised learning algorithms based on applying Bayes' theorem with the 'naive' assumption of independence between every pair of features. Given a class variable $y$ and a dependent feature vector $x_1$ through $x_n$ Bayes' theorem states the following relationship:

\begin{equation}
P(y |x_1,...,x_n) = \frac{P(y)P(x_1,...,x_n|y}{P(x_1,...,x_n}
\end{equation}

Different naive Bayes classifiers differ by assumptions they make regarding the distribution of $P(x_i | y).
Due to decoupling of the class conditional feature distribution it means each distribution can be independetly estimated as a one dimensional distribution. Not only its fast it also helps to alleviate problems stemming from the curse of dimensionality.

Although they are known as descent classifier, they are bad at estimation problems.
