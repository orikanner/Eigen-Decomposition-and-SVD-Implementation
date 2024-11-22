# Eigen Decomposition and SVD for Dimensionality Reduction: Implementation and Comparison

This repository is a learning exercise where I explore two approaches to performing dimensionality reduction with PCA: eigen decomposition and SVD.

### Two Methods to Show PCA:
Both methods are based on the fact that $`X^T X`$ captures the relationships and variances of our features (the covariance matrix), and PCA uses this to project the data onto new axes of maximal variance.

1. **Direct Eigenvalue Decomposition**:
   - Compute $`X^TX`$ (the feature covariance matrix).
   - Extract eigenvectors and eigenvalues from $`X^T X`$.
   - Use the top 3 (for example) eigenvectors to project the data onto a reduced-dimensional space for visualization.

2. **SVD-Based PCA**:
   - Perform SVD on `X:` $`X = U Σ V^T`$.
   - Relate $`X^TX`$ to SVD: $`X^TX = (VΣ^TU^T)(UΣV^T) = VΣ^2V^T`$. (Because U is orthogonal => $`U^TT = I`$)
   - Based on the definition of SVD:
     - `V`: Matrix of **right singular vectors**, which are the **eigenvectors of $`X^TX`$**.
     - `Σ`: Diagonal matrix where $`Σ^2`$ = eigenvalues of $`X^TX`$.

      a. Eigenvalue decomposition of a squared matrix `M` is $`M = Q Λ Q^{-1}`$.

      b. When `Q` is orthogonal, $`Q^T = Q^{-1}`$.

      From a and b, we can say $`M = QΛQ^T`$ is the eigenvalue decomposition of an orthogonal matrix.

   - This confirms that the decomposition: $`VΣ^2V^T = VΛV^T`$ matches the eigenvalue decomposition of $`X^TX`$.

### Why SVD is Better?
- **Numerical Stability**: SVD avoids direct computation of $`X^TX`$, reducing numerical instability for large or poorly conditioned matrices.
- **Efficiency**: SVD works directly on non-square matrices and extracts principal components without needing covariance matrix computation.

### Interesting Note:
The **Spectral Theorem** ensures that symmetric matrices like $`X^TX`$ can always be diagonalized with real eigenvalues and orthogonal eigenvectors. This property is fundamental to PCA and shows why $`X^TX`$ provides a clear way to represent feature variance in a new orthogonal basis.

## Final Note:
**As a final note, the purpose of this project wasn’t to analyze the pros and cons of each method but to convince myself, step-by-step, that both approaches yield similar results—at least with the Iris dataset. 😊**


---


### Clarification: The Difference Between Eigen Decomposition and Diagonalization

**Eigen Decomposition**:

- **Definition**: The process of representing a square matrix $M$ as:  
  $` M = Q \Lambda Q^{-1} `$  
  where:  
  - $Q$: Matrix of eigenvectors (not necessarily independent).  
  - $\Lambda$: Diagonal matrix of eigenvalues.  

- **Applicability**:  
  - Eigen decomposition works for any square matrix, even if the eigenvectors are not linearly independent.  
  - If there aren't enough independent eigenvectors, $Q$ won't fully span the matrix's space, but eigen decomposition can still provide eigenvalues and eigenvectors.

---

**Diagonalization**:

- **Definition**: A specific case of eigen decomposition where:  
  $`M = Q \Lambda Q^{-1} `$  
  with:  
  - $Q$: Matrix containing enough linearly independent eigenvectors to span the matrix's space (a full basis).  
  - $\Lambda$: Diagonal matrix of eigenvalues.  

- **Conditions**:  
  - The matrix must have a full rank of linearly independent eigenvectors.  
  - Symmetric and positive definite matrices satisfy this condition, which ensures diagonalization.

---

**Key Differences**:

- **Eigen Decomposition**:  
  - A general process.  
  - Works even if eigenvectors are not linearly independent.  
  - Resulting matrix $Q$ may not fully describe a basis, so $M$ cannot always be diagonalized.  

- **Diagonalization**:  
  - A stricter condition requiring enough independent eigenvectors to fully span the matrix's space.  
  - Fails if eigenvectors are dependent (e.g., defective matrices).

---

**How They Relate**:

- Eigen decomposition is a prerequisite for diagonalization.  
- Diagonalization is essentially eigen decomposition + sufficient independent eigenvectors.  
- If a matrix can be diagonalized, it means eigen decomposition produced a $Q$ that spans the full space, enabling the diagonal form. If not, eigen decomposition still provides useful information but stops short of diagonalization.
