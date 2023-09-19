----

# Explanation

Evaluating a model is simple enough: just use a test set. But suppose you are hesitating between two types of models (say, a linear model and a polynomial model): how
can you decide between them? One option is to train both and compare how well
they generalize using the test set.

Now suppose that the linear model generalizes better, but you want to apply some
regularization to avoid overfitting. The question is, how do you choose the value of
the regularization hyperparameter? One option is to train 100 different models using
100 different values for this hyperparameter. Suppose you find the best hyperparameter value that produces a model with the lowest generalization error—say, just 5%
error. You launch this model into production, but unfortunately it does not perform
as well as expected and produces 15% errors. What just happened?

The problem is that you measured the generalization error multiple times on the test
set, and you adapted the model and hyperparameters to produce the best model for
that particular set. This means the model is unlikely to perform as well on new data.

To overcome this issue, some others validation method can be employed.

# Method
## Holdout Validation
Simply *hold out part of the training set to evaluate several candidate models* and select the best one. The *new held-out set* is called the *validation set* (or the development set, or dev set). More specifically, you train multiple models with various hyperparameters on the reduced training set (i.e., the full training set minus the validation set), and you select the model that performs best on the validation set. After this holdout validation process, you train the best model on the full training set (including the validation set), and this gives you the final model. Lastly, you evaluate
this final model on the test set to get an estimate of the generalization error.

----

![[holdout-validate.png| 400]]

----

## Cross-Validation
Cross-validation provides a more reliable estimate of a model's performance compared to simpler validation methods like a single train-test split.

The basic idea of cross-validation is to *divide the available data* into several subsets or *folds*. The model is trained and evaluated multiple times, with each fold serving as the validation set while the remaining folds form the training set. By systematically cycling through all the folds, each data point is used for both training and validation, ensuring comprehensive coverage of the dataset.

----


![[kfoldcross.jpg|400]]![[fold1.png|400]]

----
