----
Say you are visiting a foreign country and the taxi driver rips you off. You might be
tempted to say that all taxi drivers in that country are thieves. *Overgeneralizing* is
something that we humans do all too often, and unfortunately machines can fall into
the same trap if we are not careful. In machine learning this is called *overfitting*: it means that the model *performs well on the training data, but it does not generalize
well.*

![[overfitting.png]]

In machine learning, complex models like deep neural networks have the ability to identify intricate patterns in data. However, if the training dataset is noisy or too small, it introduces *sampling noise*. In such cases, the model may *end up identifying patterns within the noise* itself, which are unlikely to generalize to new instances.

For example, if a life satisfaction model is fed with additional attributes, including uninformative ones like the country's name, a complex model might detect patterns such as all countries with a "w" in their name having a life satisfaction greater than 7 (e.g., New Zealand, Norway, Sweden, and Switzerland). However, it is not reasonable to assume that this pattern holds true for countries like Rwanda or Zimbabwe. This pattern might have occurred in the training data purely by chance, and the model cannot differentiate between real patterns and noise in the data.

----

To mitigate the risk of overfitting and make the model simpler, *regularization techniques are employed*. Regularization involves constraining the model's complexity.

For instance, in a linear model with parameters $\theta_0$ and $\theta_1$, if $\theta_1$ is forced to be zero, the model becomes overly simple and unable to fit the data accurately. On the other hand, allowing $\theta_1$ to be modified but constraining it to remain small strikes a balance between a too simple and too complex model. Finding the right balance between fitting the training data and maintaining model simplicity is crucial for ensuring good generalization performance.

![[Overfitting 2.png]]

The amount of regularization to apply during learning can be controlled by a hyper‐
parameter. A [[Hyperparameter Tuning and Model Selection|hyperparameter]] is a *parameter of a learning algorithm* (not of the
model). As such, it is not affected by the learning algorithm itself; it must be set
prior to training and remains constant during training. 

If you set the [[Hyperparameter Tuning and Model Selection|regularization hyperparameter]] to a very large value, you will get an almost flat model (a slope close to zero); the learning algorithm will almost certainly not overfit the training data, but it will be less likely to find a good solution.

----

In summary, complex models can detect patterns in data, but noisy or small training datasets introduce sampling noise that can lead the model to identify patterns in the noise itself. Constraining the model's complexity through regularization helps prevent overfitting and ensures a balance between accurate fitting of the training data and generalization to new instances.