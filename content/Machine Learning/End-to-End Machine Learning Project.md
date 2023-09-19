#machinelearning

- [f] **Level:** #Basic 
----
# Working with Real Data

## Main steps of ML Projects

### Look at big picture.
1. Define the objective in business terms.
2. How will your solution be used?
3. What are the current solutions/workarounds (if any)?
4. How should you frame this problem (supervised/unsupervised, online/offline, etc.)?
5. How should performance be measured?
6. Is the performance measure aligned with the business objective?
7. What would be the minimum performance needed to reach the business objective?
8. What are comparable problems? Can you reuse experience or tools?
9. Is human expertise available?
10. How would you solve the problem manually?
11. List the assumptions that have made so far.
12. Verify assumptions if possible
### Get the data.
1. List the data you need and how much you need.
2. Find and document where you can get that data.
3. Check how much space it will take.
4. Check legal obligations, and get authorization if necessary.
5. Get access authorizations.
6. Create a workspace (with enough storage space).
7. Get the data.
8. Convert the data to a format you can easily manipulate (without changing the data itself).
9. Ensure sensitive information is deleted or protected (e.g., anonymized).
10. Check the size and type of data (time series, sample, geographical, etc.).
11. Sample a test set, put it aside, and never look at it (no data snooping)
### Explore and visualize the data to gain insights.
1. Create a copy of the data for exploration (sampling it down to a manageable size if necessary).
2. Create a Jupyter notebook to keep a record of your data exploration.
3. Study each attribute and its characteristics:
	- Name
	- Type (categorical, int/float, bounded/unbounded, text, structured, etc.) 
	- % of missing value
	- Noisiness and type of noise (stochastic, outliers, rounding errors, etc.)
	- Usefulness for the task
	- Type of distribution (Gaussian, uniform, logarithmic, etc.)
1. For supervised learning tasks, identify the target attribute(s).
2. Visualize the data.
3. Study the correlations between attributes.
4. Study how you would solve the problem manually.
5. Identify the promising transformations you may want to apply.
6. Identify extra data that would be useful (go back to “[[#Get the data.]]”).
7. Document what you have learned.
### Prepare the data for machine learning algorithms.
***Notes:***
- Work on copies of the data (keep the original dataset intact).
- Write functions for all data transformations you apply, for five reasons:
	- So you can easily prepare the data the next time you get a fresh dataset
	- So you can apply these transformations in future projects
	- To clean and prepare the test set
	- To clean and prepare new data instances once your solution is live
	- To make it easy to treat your preparation choices as hyperparameter
----
1. Clean the data:
	- Fix or remove outliers (optional).
	- Fill in missing values (e.g., with zero, mean, median…) or drop their rows (or columns).
2. Perform feature selection (optional):
	- Drop the attributes that provide no useful information for the task.
3. Perform feature engineering, where appropriate:
	- Discretize continuous features.
	- Decompose features (e.g., categorical, date/time, etc.).
	- Add promising transformations of features (e.g., $log(x), sqrt(x), x^2$, etc.).
	- Aggregate features into promising new features
4. Perform feature scaling:
	- Standardize or normalize
### Select a model and train it (Shortlist Promising Models)
***Notes:***
- If the data is huge, you may want to sample smaller training sets so you can train many different models in a reasonable time (be aware that this penalizes complex models such as large neural nets or random forests).
- Once again, try to automate these steps as much as possible.
----
1. Train many quick-and-dirty models from different categories (e.g., linear, Naïve Bayes, SVM, random forest, neural net, etc.) using standard parameters.
2. Measure and compare their performance:
	- For each model, use N-fold cross-validation and compute the mean and standard deviation of the performance measure on the N folds.
3. Analyze the most significant variables for each algorithm.
4. Analyze the types of errors the models make:
	-  What data would a human have used to avoid these errors?
5. Perform a quick round of feature selection and engineering.
6. Perform one or two more quick iterations of the five previous steps.
7. Shortlist the top three to five most promising models, preferring models that make different types of errors
### Fine-tune your model.
***Notes:***
- You will want to use as much data as possible for this step, especially as you move•
toward the end of fine-tuning.
- As always, automate what you can
----
1. Fine-tune the hyperparameters using cross-validation:1.
	-  Treat your data transformation choices as hyperparameters, especially when you are not sure about them (e.g., if you’re not sure whether to replace missing values with zeros or with the median value, or to just drop the rows.)
	- Unless there are very few hyperparameter values to explore, prefer random search over grid search. If training is very long, you may prefer a Bayesian optimization approach (e.g., using Gaussian process priors, as described by [Jasper Snoek et al.](https://arxiv.org/abs/1206.2944)
2. Try ensemble methods. Combining your best models will often produce better performance than running them individually.
3. Once you are confident about your final model, measure its performance on the test set to estimate the generalization error
**Warning** Don’t tweak your model after measuring the generalization error:
you would just start overfitting the test set.
### Present your solution
1. Document what you have done.
2. Create a nice presentation:
	- Make sure you highlight the big picture first.
3. Explain why your solution achieves the business objective.
4. Don’t forget to present interesting points you noticed along the way:
	- Describe what worked and what did not.
	- List your assumptions and your system’s limitations.
5. Ensure your key findings are communicated through beautiful visualizations or easy-to-remember statements (e.g., “the median income is the number-one predictor of housing prices”)
### Launch, monitor, and maintain your system
1. Get your solution ready for production (plug into production data inputs, write unit tests, etc.).
2. Write monitoring code to check your system’s live performance at regular intervals and trigger alerts when it drops:
	- Beware of slow degradation: models tend to “rot” as data evolves
	- Measuring performance may require a human pipeline (e.g., via a crowdsourcing service).
	- Also monitor your inputs’ quality (e.g., a malfunctioning sensor sending random values, or another team’s output becoming stale). This is particularly important for online learning systems.
3. Retrain your models on a regular basis on fresh data (automate as much as possible).