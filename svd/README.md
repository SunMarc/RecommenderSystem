## Matrix factorization algorithm

The SVD model algorithm is very similar to the ALS algorithm. The two differences between the two approaches are:

- SVD additionally models the user and item biases (also called baselines in the litterature) from users and items.
- The optimization technique in ALS is Alternating Least Squares (hence the name), while SVD uses stochastic gradient descent.

### The SVD model

The method usually referred to as "SVD" that is used in the context of recommendations is not strictly speaking the mathematical Singular Value Decomposition of a matrix but rather an approximate way to compute the low-rank approximation of the matrix by minimizing the squared error loss. A more accurate, albeit more generic, way to call this would be Matrix Factorization.  It is important to note that the "true SVD" approach had been indeed applied to the same task years before, with not so much practical success. Billsus & Panzani, for example, described already in 1998 how to use this approach (see Page on aaai.org).

In ALS, the ratings are modeled as follows:
```math
\hat r_{u,i} = q_{i}^{T}p_{u}
```
SVD introduces two new scalar variables: the user biases $`b_u`$ and the item biases $`b_i`$. The user biases are supposed to capture the tendency of some users to rate items higher (or lower) than the average. The same goes for items: some items are usually rated higher than some others. The model is SVD is then as follows:

```math
\hat r_{u,i} = \mu + b_u + b_i + q_{i}^{T}p_{u}
```

Where $`\mu`$ is the global average of all the ratings in the dataset. The regularised optimization problem naturally becomes:

```math
\sum(r_{u,i} - (\mu + b_u + b_i + q_{i}^{T}p_{u}))^2 +     \lambda(b_i^2 + b_u^2 + ||q_i||^2 + ||p_u||^2)
```

where $`\lambda`$ is a the regularization parameter.


### Stochastic Gradient Descent

Stochastic Gradient Descent (SGD) is a very common algorithm for optimization where the parameters (here the biases and the factor vectors) are iteratively incremented with the negative gradients w.r.t the optimization function. The algorithm essentially performs the following steps for a given number of iterations:


```math
b_u \leftarrow b_u + \gamma (e_{ui} - \lambda b_u)
```
```math
b_i \leftarrow b_i + \gamma (e_{ui} - \lambda b_i)
```  
```math
p_u \leftarrow p_u + \gamma (e_{ui} \cdot q_i - \lambda p_u)
```
```math
q_i \leftarrow q_i + \gamma (e_{ui} \cdot p_u - \lambda q_i)
```

where $`\gamma`$ is the learning rate and $`e_{ui} =  r_{ui} - \hat r_{u,i} = r_{u,i} - (\mu + b_u + b_i + q_{i}^{T}p_{u})`$ is the error made by the model for the pair $`(u, i)`$.