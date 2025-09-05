The previous section presented a set of model metrics, all calculated at a single classification threshold value. But if you want to evaluate a model's quality across all possible thresholds, you need different tools.

    Receiver-operating characteristic curve (ROC)
The ROC curve is a visual representation of model performance across all thresholds. The long version of the name, receiver operating characteristic, is a holdover from WWII radar detection.


    Area under the curve (AUC)
The area under the ROC curve (AUC) represents the probability that the model, if given a randomly chosen positive and negative example, will rank the positive higher than the negative.

    AUC and ROC for choosing model and threshold
AUC is a useful measure for comparing the performance of two different models, as long as the dataset is roughly balanced. The model with greater area under the curve is generally the better one.

