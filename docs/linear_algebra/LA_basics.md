# Linear Algebra

## Properties
- Matrix Rank -> Number of independent rows and columns
	- Nonsingular = Full Rank  $\rho(A) = min(n,m)$.
	- Singular = Not full Rank $\rho(A) < min(n,m)$.

- Matrix Inverse (square A)
	- $AA^-1 = A^-1A = I$

- Nonsingular and square $=>$ Invertible

- Matrix Trace -> $tr(A) = \sum_i A_{ii}$

- Symmetric Matrix -> $A = A^T$

- Positive Definiteness (Semi-Definitness)

	- For a symmetrix $n\times n$ matrix, $A$, and for any $x$ in $R^n$
		- $x^TAX>0 \quad x^TAX \geq 0$

- Eigenvalue and Eigenvectors of a matrix
	- For a matrix $A$ the vector $x$ is an *eigenvector* of $A$ with a corresponding *eigenvalue* $\lambda$ if they satisfy the equation
		- $Ax = \lambda x$.
	- Eigenvalues of a diagonal matrix are its diagonal elements
	- The inverse of $A$ exists iff none of the eigenvalues are zero
	- Positive definite $A$ has all eigenvalues greater than zero
- Differentiation of linear matrix equation

	- $\frac{d}{dx}(Ax) = A$
	- $\frac{d}{dx}(x^TA) = A^T$
