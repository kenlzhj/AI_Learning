Classification: Prediction bias

As mentioned in the Linear regression module, calculating prediction bias is a quick check that can flag issues with the model or training data early on.

Prediction bias is the difference between the mean of a model's predictions and the mean of ground-truth labels in the data. A model trained on a dataset where 5% of the emails are spam should predict, on average, that 5% of the emails it classifies are spam. In other words, the mean of the labels in the ground-truth dataset is 0.05, and the mean of the model's predictions should also be 0.05. If this is the case, the model has zero prediction bias. Of course, the model might still have other problems.

If the model instead predicts 50% of the time that an email is spam, then something is wrong with the training dataset, the new dataset the model is applied to, or with the model itself. Any significant difference between the two means suggests that the model has some prediction bias.

Prediction bias can be caused by:

Biases or noise in the data, including biased sampling for the training set
Too-strong regularization, meaning that the model was oversimplified and lost some necessary complexity
Bugs in the model training pipeline
The set of features provided to the model being insufficient for the task