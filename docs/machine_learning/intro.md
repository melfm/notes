## Intro
- It is difficult to draw pattern from hard-coded knowledge.
- A simple machine learning algorithm such as naive Bayes can separate email from spam.
- Each piece of information included in the representation of data is known as a feature.
- When designing an algorithm for learning features, the goal is to separate the $\textbf{factors
of variation}$ that explain the observed data.
    - In this context, ''factors'' refer to separate sources of influence
    - Such factors may exist as unobserved pattern that affect observable quantities
    - This may exists in the human mind that provides simlifying explanations or inferred causes of the
    observed data
    - Can think of these as abstractions in the data (e.g. in an object, color, angle etc)

## Supervised Learning

Learning is useful whenever we want a computer to perform a function or procedure so intricate that it cannot be programmed
by conventional means.
For example it is simply not clear how to directly write a computer program that recognizes cats.
However given large amount of data it is possible to approximate the input-output relationship
implied by the training examples.

Let $X$ be an input space, $Y$ an output space, $D$ the data distribution over $X \times Y$ that describes
the data that we tend to observe.
For every drawn $(x,y)$ from $D$, the variable $x$ is a typical input and $y$ the desired output.
The goal of supervised learning is to use a training set consisting of $n$ of i.i.d. samples,
in order to find a function $f: X \rightarrow Y$ whose test error

\begin{equation}
  Test_D(f) \equiv E_{(x,y) \approx D} [L(f(x);y)]
\end{equation}

is as low as possible. Here $L(z;y)$ is a loss function that measures the loss that we suffer whenever we
predict $y$ as $z$. Once we find a function whose test error is small enough for our needs, the learning is
solved. Although it would be ideal to find the global minimizer of the test error

\begin{equation}
  f^* =  {arg min} Test_D(f)
\end{equation}

doing so is fundamentally impossible. We can approximate the test error with the training error

\begin{equation}
  Train_S(f)  \equiv E_{(x,y) \approx S} [L(f(x);y)] \approx Test_D(f)
\end{equation}

We define $S$ as the uniform distribution over training cases counting duplicate cases multiple times and find a
function $f$ with a low training error, but it is trivial to minimize the training error by memorizing
the training cases.

## Generalization
- Making sure that good performance on the training set translates into good performance on the test set
- Conceptually easy to solve by restricting the allowable function $f$ to a relatively small class of
functions $F$ :

\begin{equation}
  f^* = \underset{f \in F}{arg min} Train_S(f)
\end{equation}

Restricting $f$ to $F$ solves the generalization problem. This lets us focus on the algorithmic problem
of minimizing the training error while being almost certain that the test error will be approximately
minimized as well.

As the size of the training set grows with $F$, we want $F$ to be as small as possible.
At the same time, we want $F$ to be as large as possible to improve the performance of its best function.

