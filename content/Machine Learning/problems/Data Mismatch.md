----

In cases where a large amount of training data is available but may not be perfectly representative of the data used in production, it is crucial to ensure that the validation set and the test set are as representative as possible of the production data. The **validation set and the test set should consist exclusively of representative pictures**, with no duplicates or near-duplicates in both sets.

To address the potential mismatch between the web pictures (used for training) and the pictures taken with the mobile app, Andrew Ng proposed the use of a **train-dev set**. This set contains some training pictures that are held out separately. After training the model on the training set, the model's performance can be evaluated on the train-dev set. If the model performs poorly on the train-dev set, it indicates **overfitting** of the training set, suggesting the need to simplify or regularize the model, acquire more training data, or clean up the training data.

If the model performs well on the train-dev set, it can be evaluated on the **dev set**. If the performance on the dev set is poor, the problem is likely due to the data mismatch. In such cases, **preprocessing the web images** to resemble the pictures taken by the mobile app can help address the issue. The model can then be retrained with the modified web images. Once a model performs well on both the train-dev set and the dev set, a final evaluation on the **test set** provides an estimation of its performance in production.

In summary, ensuring that the validation set and test set are representative of the production data is crucial when the training data may not perfectly match the data used in production. The use of a train-dev set helps diagnose overfitting, while preprocessing the web images can address data mismatch issues. Evaluating the model on the test set provides a final assessment of its performance in a production-like setting.

![[datamismatch.png]]