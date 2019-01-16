CART (Classification and Regression Trees)
==========================================
from: https://www.youtube.com/watch?v=LDRbO9a6XPU (with code)
- each split node will split based on one of the feature 
- unmix the label on the leaves
- quantify how much a question unmixed the labels by a node
  - **Gini impurity** - the amount of uncertainty of correct unmixed label
  - **Information gain** - how much a node to help reduce the uncertainty
- each node generates a list of questions, iterate through the features of all rows to decide these questions. And it creates the thresholds based on the features' values.

### How it works (Information Gain)
1. try iterate a list of the questions
2. check the **Weighted Avg Impurity** of the split nodes
3. subtract the parent node with the split nodes ==> Information Gain
4. take the largest Information Gain's question as the best split for this node


Bagging and Boosting - Decision Tree Ensembles
============================================
from: https://towardsdatascience.com/decision-tree-ensembles-bagging-and-boosting-266a8ba60fd9

Problem of one tree: You will have a large bias with simple trees and a large variance with complex trees.

### Bagging (Bootstrap Aggregation)
- it is used when our goal is to reduce the variance of a decision tree. Here idea is to create several subsets of data from training sample chosen randomly with replacement. (= ensembling trees with different subset)

### Random Forest (Bagging + Randomly Feature selecting)
- it is an extension over bagging. It takes one extra step where in addition to taking the random subset of data, it also takes the random selection of features rather than using all features to grow trees.
- Best Code Tutorial (with RandomizedSearchCV):
  - https://towardsdatascience.com/hyperparameter-tuning-the-random-forest-in-python-using-scikit-learn-28d2aa77dd74
- Code Highlights:
```python
{'bootstrap': True, # bagging
'max_depth': None, # confine the max depth
'max_features': 'auto',  # confine the max features to conside
'max_leaf_nodes': None,  
'min_impurity_decrease': 0.0,
'min_impurity_split': None,
'min_samples_leaf': 1,
'min_samples_split': 2,
'min_weight_fraction_leaf': 0.0,
'n_estimators': 200, # ** num of trees
'n_jobs': -1, # parallellization of CPU
'oob_score': True, # use out of bag
'random_state': 42,
'verbose': 0,
'warm_start': False}
```

### Boosting
- When an input is misclassified by a hypothesis, its weight is increased so that next hypothesis is more likely to classify it correctly. By combining the whole set at the end converts weak learners into better performing model.

### Gradient Boosting (Gradient Descent + Boosting)
- It uses gradient descent algorithm which can optimize any differentiable loss function.

**Advantages of using Gradient Boosting technique:**

    Supports different loss function.
    Works well with interactions.

**Disadvantages of using Gradient Boosting technique:**

    Prone to over-fitting.
    Requires careful tuning of different hyper-parameters
