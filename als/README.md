## ALS algorithm

### Matrix factorization for collaborative filtering problem

Matrix factorization is a common technique used in recommendation tasks. Basically, a matrix factorization algorithm tries to find latent factors that represent intrinsic user and item attributes in a lower dimension. That is,

```math
\hat r_{u,i} = q_{i}^{T}p_{u}
```

where $`\hat r_{u,i}`$ is the predicted ratings for user $`u`$ and item $`i`$, and $`q_{i}^{T}`$ and $`p_{u}`$ are latent factors for item and user, respectively. The challenge to the matrix factorization problem is to find $`q_{i}^{T}`$ and $`p_{u}`$. This is achieved by methods such as matrix decomposition. A learning approach is therefore developed to converge the decomposition results close to the observed ratings as much as possible. Furthermore, to avoid overfitting issue, the learning process is regularized. For example, a basic form of such matrix factorization algorithm is represented as below.

```math
\min\sum(r_{u,i} - q_{i}^{T}p_{u})^2 + \lambda(||q_{i}||^2 + ||p_{u}||^2)
```

where $`\lambda`$ is a the regularization parameter. 

In case explict ratings are not available, implicit ratings which are usually derived from users' historical interactions with the items (e.g., clicks, views, purchases, etc.). To account for such implicit ratings, the original matrix factorization algorithm can be formulated as 

```math
\min\sum c_{u,i}(p_{u,i} - q_{i}^{T}p_{u})^2 + \lambda(||q_{i}||^2 + ||p_{u}||^2)
```

where $`c_{u,i}=1+\alpha r_{u,i}`$ and $`p_{u,i}=1`$ if $`r_{u,i}>0`$ and $`p_{u,i}=0`$ if $`r_{u,i}=0`$. $`r_{u,i}`$ is a numerical representation of users' preferences (e.g., number of clicks, etc.). 

### Alternating Least Square (ALS)

Owing to the term of $`q_{i}^{T}p_{u}`$ the loss function is non-convex. Gradient descent method can be applied but this will incur expensive computations. An Alternating Least Square (ALS) algorithm was therefore developed to overcome this issue. 

The basic idea of ALS is to learn one of $`q`$ and $`p`$ at a time for optimization while keeping the other as constant. This makes the objective at each iteration convex and solvable. The alternating between $`q`$ and $`p`$ stops when there is convergence to the optimal. It is worth noting that this iterative computation can be parallelized and/or distributed, which makes the algorithm desirable for use cases where the dataset is large and thus the user-item rating matrix is super sparse (as is typical in recommendation scenarios). A comprehensive discussion of ALS and its distributed computation can be found [here](http://stanford.edu/~rezab/classes/cme323/S15/notes/lec14.pdf).