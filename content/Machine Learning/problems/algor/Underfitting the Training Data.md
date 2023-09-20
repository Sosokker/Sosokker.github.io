----

As you might guess, underfitting is the *opposite of* [[Overfitting the Training Data|Overfitting]]: it occurs when your
model is *too simple to learn the underlying structure of the data*. For example, a
linear model of life satisfaction is prone to underfit; *reality is just more complex*
than the model, so its predictions are bound to be inaccurate, even on the training
examples.

Here are the main options for fixing this problem:
- Select a more powerful model, with more parameters.
- Feed better features to the learning algorithm (feature engineering).
- Reduce the constraints on the model (ex: reducing the regularization hyperparameter)