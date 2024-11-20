# SVD and Eigen Decomposition for Dimensionality Reduction: Implementation and Comparison

This repository is a learning exercise where I explore two approaches to performing dimensionality reduction with PCA: eigen decomposition and SVD.

### Two Methods to Show PCA:
Both methods are based on the fact that `X^T X` captures the relationships and variances of our features (the covariance matrix), and PCA uses this to project the data onto new axes of maximal variance.

1. **Direct Eigenvalue Decomposition**:
   - Compute `X^T X` (the feature covariance matrix).
   - Extract eigenvectors and eigenvalues from `X^T X`.
   - Use the top 3 (for example) eigenvectors to project the data onto a reduced-dimensional space for visualization.

2. **SVD-Based PCA**:
   - Perform SVD on `X`: `X = U Σ V^T`.
   - Relate `X^T X` to SVD: `X^T X = (V Σ^T U^T)(U Σ V^T) = V Σ^2 V^T`. (Because U is orthogonal => `U^T T = I`)
   - Based on the definition of SVD:
     - `V`: Matrix of **right singular vectors**, which are the **eigenvectors of X^T X**.
     - `Σ`: Diagonal matrix where `Σ^2 = eigenvalues of X^T X`.

      a. Eigenvalue decomposition of a squared matrix `M` is `M = Q Λ Q^-1`.

      b. When `Q` is orthogonal, `Q^T = Q^-1`.

      From a and b, we can say `M = Q Λ Q^T` is the eigenvalue decomposition of an orthogonal matrix.

   - This confirms that the decomposition: `V Σ^2 V^T = V Λ V^T` matches the eigenvalue decomposition of `X^T X`.

### Why SVD is Better?
- **Numerical Stability**: SVD avoids direct computation of `X^T X`, reducing numerical instability for large or poorly conditioned matrices.
- **Efficiency**: SVD works directly on non-square matrices and extracts principal components without needing covariance matrix computation.

### Interesting Note:
The **Spectral Theorem** ensures that symmetric matrices like `X^T X` can always be diagonalized with real eigenvalues and orthogonal eigenvectors. This property is fundamental to PCA and shows why `X^T X` provides a clear way to represent feature variance in a new orthogonal basis.

### Final Note:
**As a final note, the purpose of this project wasn’t to analyze the pros and cons of each method but to convince myself, step-by-step, that both approaches yield similar results—at least with the Iris dataset. 😊**
