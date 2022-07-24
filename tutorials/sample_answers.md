Prereq:
- After `merge`, is the local and remote now synced? Why or why not?
    - No. You have created a new `commit` when merging the two `branches`.

Tutorial 1:
- Select the first 10 records for `passenger_count` and `trip_distance`.
  - A: `sdf.select(["passenger_count", "trip_distance"]).limit(10)`
- Write code to retrieve all non-zero passenger counts and all non-zero trip distances using `.where()`
  - `sdf.where((F.col('passenger_count') > 0) & (F.col('trip_distance') > 0)).limit(5)`

Tutorial 3:
- What is formula of $f_{\beta}(x)$, $\ell(\cdot, \cdot)$ for linear regression?
  - $f_{\beta}(x) = x\beta$
  - $\ell(\cdot, \cdot) = (y - \hat y) (y - \hat y)^\intercal$
- Extension:
  - $f_{\beta}(x) = x\beta$
  - $\ell(\cdot, \cdot) = (y - \hat y) (y - \hat y)^\intercal + \lambda  ||\beta||_1$
- Why? Can you explain this mathmatically? (Tip: consider a pair of positive coefficient $\beta=[1, \epsilon], \epsilon < 1$, and think about what happens to $||\beta||_2^2$ when you subtract $\delta \leq \epsilon$ from each element $\beta$)
  - Refer this [answer](https://stats.stackexchange.com/a/45644)
- How would you implement optimizer for the above objectives (LASSO, Ridge, Elastic Net)?
  - Gradient descent
  - [Closed form solution](https://stats.stackexchange.com/questions/17781/derivation-of-closed-form-lasso-solution)
  - [Iteratively weighted gradient descent (IRLS)](https://en.wikipedia.org/wiki/Iteratively_reweighted_least_squares)
  - [Newton's Method](https://en.wikipedia.org/wiki/Newton%27s_method_in_optimization)

- Do you need to standardize the input data? Why?
  - Yes, different magnitudes in the features might result in unfair penalization for different parameters.
- Is the following pseudo-code correct? Why or why not?
  ```
  mu <- mean(X)
  sigma <- std(X)
  X_std <- (X - mu) / sigma
  X_train, X_test, y_train, y_test <- split(X_std, y)
  model <- fit(y_train ~ X_train)
  y_pred <- predict(model, X_test)
  loss <- MSE(y_test, y_pred)
  ```
  - No. The standardization is carried out before the train-test split. This leaks information from validation set to model training.
- What happens when input matrix is not full rank?
  - Resulting $\beta$ is not unique.