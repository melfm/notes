# Linear Algebra

## Matrix Properties

### Linear Dependence
A set of vectors is linearly independent if NO vector in the set is
* A scalar multiple of another vector in the set
* A linear combination of other vectors in the set

\begin{align}
a = [1 \quad 2 \quad 3] \quad b=[4 \quad 5 \quad 6] \quad c = [2 \quad 4 \quad 6]
\end{align}

* Vectors a and b are linearly independent.
* Vectors a and c are linearly dependent.

### Matrix Rank
The rank is defined as the
* Maximum number of linearly independent column and row vectors

For an $r \times c$ matrix
* If $r$ is less than $c$ -> the max rank of the matrix is $r$
* If $r$ is greater than $c$ -> the max rank is $c$

The maximum number of linearly independent vectors in a matrix
is equal to the number of non-zero rows in its row echelon matrix.

### Nonsingular Matrix


### Matrix Inverse
* The inverse of a square matrix $A$, called a reciprocal matrix, is $A^{-1}$ s.t.
    * $AA^{-1} = A^{-1}A = I$

### Matrix Trace
* $tr(A) = \sum_i A_{ii}$

### Symmetric Matrix
* $A = A^T$


* Positive Definiteness (Semi-Definitness)
* For a symmetrix $n\times n$ matrix, $A$, and for any $x$ in $R^n$
    * $x^TAX>0 \quad x^TAX \geq 0$

### Eigenvalue and Eigenvectors
* For a matrix $A$ the vector $x$ is an *eigenvector* of $A$ with a corresponding *eigenvalue* $\lambda$ if they satisfy the equation
    * $Ax = \lambda x$.
* Eigenvalues of a diagonal matrix are its diagonal elements
* The inverse of $A$ exists iff none of the eigenvalues are zero
    * Positive definite $A$ has all eigenvalues greater than zero
* Differentiation of linear matrix equation
    * $\frac{d}{dx}(Ax) = A$
	* $\frac{d}{dx}(x^TA) = A^T$
