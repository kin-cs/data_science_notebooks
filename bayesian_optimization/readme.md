Bayesian Optimization
====================

### Reference:
- Good lecture note: https://www.iro.umontreal.ca/~bengioy/cifar/NCAP2014-summerschool/slides/Ryan_adams_140814_bayesopt_ncap.pdf
- Clear concept: https://towardsdatascience.com/a-conceptual-explanation-of-bayesian-model-based-hyperparameter-optimization-for-machine-learning-b8172278050f

Concepts
--------
- Grid/Random Search has no past evaluation saved as information for next search, which is not efficient
- Bayesian Optimization makes a probabilistic model (surrogate model) to simulate the actual objective function, which could be very computational expensive to run.

### Steps
1. Build a **surrogate probabilistic** model for **objective function**
2. Find the best hyperparameters based on a **selection function (aka acquisition function)** in surrogate model within the **domain/range of hyperparametes**
3. apply this hyperparameters in actual objective function
4. update the surrogate model with **new results**
5. repeat above until maximum round is met

Various models & Libraries
--------------

### Surrogate Model (aka Response Surface)
- Guanssian Processes [Library:  Spearmint and MOE]
- Random Forest Regression [Library: SMAC]
- Tree Parzen Estimation [Library: Hyperopt]

### Selection Function
- Expected Improvement (per second)

### Notebooks
- https://www.kaggle.com/eikedehling/tune-and-compare-xgb-lightgbm-rf-with-hyperopt

