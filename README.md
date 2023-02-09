# RecommenderSystem

The table below lists the recommender algorithms that I have explored

| Algorithm | Environment | Type | Description |
| --- | --- | --- | --- |
| Alternating Least Squares (ALS) | [PySpark/Python CPU/GPU](als) | Collaborative Filtering | Matrix factorization algorithm for explicit or implicit feedback in large datasets|
| Bayesian Personalized Ranking (BPR) | [Python CPU](bpr) | Collaborative Filtering | Matrix factorization algorithm for predicting item ranking with implicit feedback |
| Simple Algorithm for Recommendation (SAR)| [Python CPU](sar) | Collaborative Filtering | Similarity-based algorithm for implicit feedback dataset |
| LightFM/Hybrid Matrix Factorization | [Python CPU](lfm) | Hybrid | Hybrid matrix factorization algorithm for both implicit and explicit feedbacks |
| Singular Value Decomposition (SVD) | [Python CPU](svd) | Collaborative Filtering | Matrix factorization algorithm for predicting explicit rating feedback in datasets that are not very large |
| Truncated SVD | [Python CPU](t_svd) | Collaborative Filtering | Matrix factorization algorithm by using the real mathematical SVD |
