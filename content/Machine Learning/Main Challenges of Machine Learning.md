 #Basic
----
# Introduction

Machine learning faces challenges such as overfitting, underfitting, data quality and quantity, feature selection, handling missing data, computational complexity, and ethical considerations. Proper understanding of these challenges and the appropriate application of techniques and algorithms help address them and build robust machine learning models.

----
# Problems

## Data Problems

## [[Insufficient Quantity of Training Data]]

## [[Nonrepresentative Training Data]]

## [[Poor-Quality Data]]

## [[Irrelevant Features]]

## Algorithm Problems

## [[Overfitting the Training Data]]

## [[Underfitting the Training Data]]



# How can we detect the problems?

## Testing and Validating

The only way to know how well a model will generalize to new cases is to actually *try it out on new cases*. One way to do that is to *put your model in production* and
monitor how well it performs. This works well, but if your model is horribly bad,
your users will complain—not the best idea😭.

A better option is to split your data into two sets: ***training set*** and ***test set***.
The model is trained on the training set, and its performance is assessed using the test set. The generalization error, which measures the model's error rate on new instances, can be estimated by evaluating the model on the test set.

If the model achieves a *low error rate* on the **training set** but a *high error* rate on the **test set**, it indicates that the model is overfitting the training data. Overfitting occurs when the model becomes too specialized to the training data and *fails to generalize* well to new instances.

A common practice is to allocate approximately 80% of the data for training and reserve the remaining 20% for testing. 
However, the split ratio can vary depending on the dataset's size. For instance, if the dataset contains millions of instances, holding out just 1% can provide a sufficiently large test set to obtain a reliable estimate of the generalization error. The key is to strike a balance between having enough data for training and having a representative test set to evaluate the model's performance accurately.

# Hyperparameter

## [[Hyperparameter Tuning and Model Selection]]

# No Free Lunch
Theorem serves as a reminder that *there is no universally superior machine learning algorithm*. Different algorithms have strengths and weaknesses, and their performance is context-dependent. It underscores the need for thoughtful selection and customization of algorithms based on the specific problem and data characteristics.

The only way to know for sure which model is best is to evaluate them all. Since
this is not possible, in practice you *make some reasonable assumptions about the
data and evaluate only a few reasonable models*. For example, for simple tasks you
may evaluate linear models with various levels of regularization, and for a complex
problem you may evaluate various neural network