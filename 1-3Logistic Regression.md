a logistic regression model for spam-email detection that predicts a value between 0 and 1, representing the probability that a given email is spam. A prediction of 0.50 signifies a 50% likelihood that the email is spam, a prediction of 0.75 signifies a 75% likelihood that the email is spam, and so on.

    Confusion matrix
The probability score is not reality, or ground truth. There are four possible outcomes for each output from a binary classifier. For the spam classifier example, if you lay out the ground truth as columns and the model's prediction as rows, the following table, called a confusion matrix, is the result:

    TP: right judgement + right action / destination
True positive (TP): A spam email correctly classified as a spam email. These are the spam messages automatically sent to the spam folder.

    FP: wrong judgement + right action / destination
False positive (FP): A not-spam email misclassified as spam. These are the legitimate emails that wind up in the spam folder.

    TN: right judgement + wrong action / destination
True negative (TN): A not-spam email correctly classified as not-spam. These are the legitimate emails that are sent directly to the inbox.

    FN: wrong judgement + wrong action / destination
False negative (FN): A spam email misclassified as not-spam. These are spam emails that aren't caught by the spam filter and make their way into the inbox.

memory skill: 
TP + FN dual reverse value = true purpose



    Accuracy 准确率
Accuracy is the proportion of all classifications that were correct, whether positive or negative. It is mathematically defined as:

   Accuracy = (TP + TN)/Sum(TP, FP, TN, FN)   \
               'correct classifications \ total classifications
   
A perfect model would have zero false positives and zero false negatives and therefore an accuracy of 1.0, or 100%.




    Recall, or true positive rate 召回率
The true positive rate (TPR), or the proportion of all actual positives that were classified correctly as positives, is also known as recall.
    
    Recall(TPR) = TP / (TP + FN)
                'correctly classified actual positives / all actual positives

在垃圾邮件分类示例中，召回率衡量的是被正确分类为垃圾邮件的垃圾邮件电子邮件的比例。
因此，召回率的另一个名称是检测概率：它可以回答“此模型检测到垃圾邮件的比例是多少？”这一问题。

    False positive rate 误报率
The false positive rate (FPR) is the proportion of all actual negatives that were classified incorrectly as positives, also known as the probability of false alarm. It is mathematically defined as:

    FPR = FP  \ (FP + TN)

incorrectly classified actual negatives \ all actual negatives
在垃圾邮件分类示例中，FPR 用于衡量被错误分类为垃圾邮件的合法电子邮件的比例，或模型的误报率。 


    Precision 精确率
Precision is the proportion of all the model's positive classifications that are actually positive. It is mathematically defined as:
    
    Precision = TP \ (TP + FP)
correctly classified actual positives \ everything classified as postive
在垃圾邮件分类示例中，精确率衡量的是被归类为垃圾邮件且实际上是垃圾邮件的电子邮件所占的比例。






