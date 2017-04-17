# RNNs with LSTM Cells

## Notation
Let subscripts denote timesteps and superscripts denote layers. All states are n-dimensional.
Let $h_t^l \in {\mathbb{R}}^n$ be a hidden state in layer $l$ in timestep $t$.
Let $T_{n,m}: {\mathbb{R}}^n \rightarrow {\mathbb{R}}^m$ be an affine transform ($Wx+b$).
Let $\otimes$ be element-wise multiplication and $h_t^0$ input vector.

## Long-Short Term Memory Units
The RNN dynamics can be described using deterministic transitions from previous to current 
hidden states. The deterministic state transition is a function.

\begin{equation}
    RNN : h_t^{l-1}, h_{t-1}^l \rightarrow h_t^l
\end{equation}

For classical RNNs this function is given by 
\begin{equation}
     h_t^{l} = f(T_{n,n} h_t^{l-1} + T_{n,n} h^l_{t-1}), where \quad f \in {sigm,tanh}
\end{equation}

LSTM has complicated dynamics that enable it to ''memorize'' information for an extended number of timesteps.
The long term memory is stored in a vector of memory cells $c_t^l \in  {\mathbb{R}}^n$.
LSTM can decide to overwrite the memory cell, retrieve it or keep it for the next time step.
Following is an example of LSTM architecture equations

\begin{equation}
    LSTM : h_t^{l-1}, h_{t-1}^l, c_{t-1}^l \rightarrow h_t^l, c_t^l
\end{equation}

\[
\begin{bmatrix}
     i \\
     f \\
     o \\
     g
\end{bmatrix}
=
\begin{bmatrix}
     sigm \\
     sigm \\
     sigm \\
     tanh
\end{bmatrix} T_{2n,4n}
\begin{bmatrix}
     h_t^{l-1} \\
     h_{t-1}^l\\
\end{bmatrix}
\]

\begin{align}
    c_t^l = f \otimes c_{t-1}^l + i \otimes g \\
    h_t^l = o \otimes tanh(c_t^l)
\end{align}


### References
[Zaremba2015] : https://arxiv.org/pdf/1409.2329v5.pdf
