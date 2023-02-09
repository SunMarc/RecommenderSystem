## 1 Truncated SVD model

The truncated SVD model algorithm is the real mathematical SVD performed on a matrix where the missing values are replaced by 0. 

In the definition of SVD, an original matrix A is can be factorized as a product A = UΣV* where U and V have orthonormal columns, and Σ is non-negative diagonal.

 Unlike regular SVDs, truncated SVD produces a factorization where the number of columns can be specified for a number of truncation. For example, given an n x n matrix, truncated SVD generates the matrices with the specified number of columns, whereas SVD outputs n columns of matrices.

By calculating UΣ, we will get our item features. From this point, we can compute the correlation matrix of UΣ to obtain the similarity between the items. The correlation matrix uses Pearson's Product-Moment Correlation.

Then, we propose similar items with the highest correlation value.


