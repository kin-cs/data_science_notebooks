Week 1
======

Categorical features
--------------------
- label encoding
for tree-based model
- frequency encoding
for both tree-based and non-tree-based model
- one-hot encoding

Missing values
--------------
- including NaN, empty string, -999, -1
- Plot histogram to check the distribution
- Approaches to fill NA
  - -999, -1
    - okay for tree-based
  - mean, median
  - reconstruct
  - Also, make an "Is Null" feature
- treat the outliers as missing values
- treat values which do not present in train data by creating the frequent encoding
- Usually do feature generation first (eg mean encoding) before apply fillna

Datetime and Coordinates
------------------------
### Datetime
- different between days
- weekday -> categorical

### Coordinates
- rotate latitude & longtitude

Week 2
======

EDA
---
- understand Data and find Magic Features.
- Don't model before doing EDA
- Check if the data makes sense (eg. age 336)
- understand how the data was generated

Exploring anonymized data
-----------------------
- figure out what type they are

Viz
---
- Histogram
``plt.hist(x)``
- **Index versus value**
  - ``plt.plot(x, '.')``
  - ``plt.scatter(range(len(x)), x, c=y)`` (checking with y)
- Feature statistics ``df.describe(); x.var()``
- check Nan ``x.isnull()``
- ``.value_counts()``

### feature relations
- ``plt.scatter(x1, x2)``
- `` pd.scatter_matrix(df)`` **pairs**
- **Check the target label by heatmap** with ``plt.scatter(x1, x2)``
- ``df.corr(); plt.matshow(...) ``

#### grouping wtih feature relations
  - ``df.mean().sort_values().plot(style='.')``

Data cleaning
-------------
- drop_duplicate()
- check if dataset is shuffled (using rolling avg of the target value)
![alt text](https://github.com/kin-cs/courses/raw/master/How%20to%20Win%20a%20Data%20Science%20Competition-%20Learn%20from%20Top%20Kagglers/img/2018-06-25_15-51-56.jpg)

Validation
------------
- types:
  - holdout: only one train-test split
  - k-fold: if k = 5, train 5 models with 5 diff validation set, and avg the 5 test prediction results
  - leave-out-out
- Use Stratification for balancing the target label ``sklearn.model_selection.StratifiedShuffleSplit``
- Set up the validation to mimic the train/test split of the competition

Problems occurring during validation
------------------------------------
- The validation score differ from leaderboard score
  - because we didn't mimic well the exact train/test split on the validation set
- Solution:
  - **K-fold with different random seed** & tune model on one split and evaluate score on the other
  - use LeaderBoard Probing
  - force the valid set same as the distribution of test set

Ref
===
Learn from winners
------------------
- http://blog.kaggle.com/2015/12/03/dato-winners-interview-1st-place-mad-professors/

Pandas
------
- df.T  #Transpose
