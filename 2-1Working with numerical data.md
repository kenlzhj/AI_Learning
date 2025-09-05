    Numerical data: How a model ingests data using feature vectors

Wouldn't a model produce better predictions by training from the actual values in the dataset than from altered values? Surprisingly, the answer is no.

You must determine the best way to represent raw dataset values as trainable values in the feature vector. This process is called feature engineering, and it is a vital part of machine learning. The most common feature engineering techniques are:

Normalization: Converting numerical values into a standard range.
Binning (also referred to as bucketing): Converting numerical values into buckets of ranges.

Every value in a feature vector must be a floating-point value. However, many features are naturally strings or other non-numerical values. 
Consequently, a large part of feature engineering is representing non-numerical values as numerical values.


