# AI/ML
- [Cross Validation](#cross_validation)
- [Decision Tree](#decision_tree)
- [K-fold cross-validation](#k-fold_cross_validation)
- [K-means clustering](#k-means_clustering)
- [K-Nearest Neighbors](#k-nearest-neighbors)
- [Linear Regression](#linear_regression)
- [Moments](#moments)
- [PCA](#pca)
- [Percentile](#percentile)
- [Polynomial Regression](#polynomial_regression)
- [R-squared](#r-squared)
- [Random Forest](#random_forest)
- [Recommendation Systems](#recommendation_systems)
- [SVC](#svc)
- [XGBoost](#xgboost)

## Cross Validation <a name="cross_validation"></a>
Cross Validation is a technique for evaluating a model’s performance by repeatedly splitting the data into training and testing sets to assess how well the model generalizes to unseen data. For exmaple (k-fold cross validation):

You have 100 data samples and set k = 5.  
You split the data into 5 parts of 20 samples each.  
In the first step, you train the model on 80 samples (parts 2, 3, 4, and 5) and test it on 20 samples (part 1).  
In the second step, you train on parts 1, 3, 4, and 5, and test on part 2, and so on.  
At the end, you average the results from these 5 tests to get the final evaluation.

## Decision Tree <a name="decision_tree"></a>
Supervised algorithm (data has a target value) used for classification (assigning to a group/category) or regression (predicting a numerical value). It is easy to interpret thanks to its visual tree structure but prone to overfitting.

## K-fold cross-validation <a name="k-fold_cross_validation"></a>
This technique divides the data into K folds and, in each iteration, uses one fold as the test set and the remaining K−1 folds as the training set. This process is repeated K times, so that each fold is used as the test set exactly once. 

## K-means clustering <a name="k-means_clustering"></a>
K-means is a popular unsupervised algorithm used for clustering data. Its goal is to partition a dataset into K clusters, where each data point is assigned to the nearest cluster centroid (center).
![alt text](/__images/image.png)

## K-Nearest Neighbors <a name="k-nearest-neighbors"></a> 
KNN (K-Nearest Neighbors) is a supervised learning algorithm used for classification (spam detection), regression (predicting house prices), anomaly detection (identifying outliers), and recommendation systems (suggesting similar movies or games). For each new point, it calculates the distance between that point and all stored training points, selects the K nearest neighbors, and then makes a decision: in classification, it chooses the most common class among the neighbors, and in regression, it computes the average value.

## Linear Regression <a name="linear_regression"></a> 
Fits a straight line to a data set of observations, it can be used to predict new values.

## Moments <a name="moments"></a>
- first moment - mean
- second moment - variance
- third moment - skew -  measures the asymmetry of a probability distribution, indicating whether data tails off more to the left (negative skew) or right (positive skew)
- fourth moment - kurtosis - how thick is the tail, and how sharp is the peak. Higher peaks have higher kurtosis

## PCA <a name="pca"></a>
PCA (Principal Component Analysis) is a dimensionality reduction technique that aims to preserve as much variance in the data as possible. For example, in the Iris dataset, where the lengths and widths of sepals and petals are correlated, reducing four features to two dimensions still allows for a good representation of the data. PCA transforms the original features into new variables, called principal components, which are linear combinations of the original variables. These new components are ordered by decreasing variance, so the first few retain most of the information present in the data.
The reasons why we do PCA can be the following:
 - Speed up model training – fewer features mean fewer computations, leading to faster training and prediction.
- Reduce the risk of overfitting – fewer features lower the chance that the model learns noise instead of true patterns.
- Make data visualization easier – 2D or 3D data can be easily visualized on plots.
- Reduce memory requirements – fewer features mean less space needed for data and the model.

## Percentile <a name="percentile"></a>
Percentiles indicate how a particular value compares to the rest of a dataset by showing the percentage of values below it. For instance, being in the 75th percentile means your result is higher than 75% of all other results.

## Polynomial Regression <a name="polynomial_regression"></a>
A more curved version of linear regression (operating on higher powers of the variables), for example: ax² + bx + c. 
```python
x = np.array(pageSpeeds)
y = np.array(purchaseAmount)

p4 = np.polynomial.Polynomial.fit(x, y, 4)
```

Higher degrees provide more flexible fitting but also increase the risk of overfitting.

## R-squared <a name="r-squared"></a>
Is a statistical measure that indicates how well the regression line fits the data. It is commonly used in linear regression to assess the quality of the model. (range 0-1, 0 bad, 1 good)

## Random Forest <a name="random_forest"></a>
Collection of multiple decision trees built on random subsets of the data (with replacement — some samples may appear multiple times or not at all in a given tree). Each tree works independently, and the final prediction is based on majority vote (for classification) or average (for regression). It produces more accurate and stable results than a single decision tree.

## Recommendation Systems <a name="recommendation_systems"></a>
Recommendation Systems methods and algorithms
- use `corrwith` to find correlations between users/items

## SVC <a name="svc"></a>
Support Vector Classifier(SVC) is a supervised machine learning algorithm. It is suitable for solving binary and multiclass classification problems, especially in complex, high-dimensional tasks.

## XGBoost <a name="xgboost"></a>
XGBoost is a supervised learning algorithm mainly used for classification and regression tasks. It is usually well-suited for many purposes but requires hyperparameter tuning to achieve the best results.