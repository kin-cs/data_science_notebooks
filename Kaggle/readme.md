
Kaggle
======

Kernel Ref.
-----------

- U-nets: https://www.kaggle.com/lscoelho/keras-u-net-lb-0-277-epochs-vsplit-thr

Avito Demand Prediction
-----------------------

### LightGBM hyper-parameter tuning
- Optimization software: Hyperopt, scikit-optimize, spearmint...
- num_leaves: more powerful it is
- bagging_fraction: just take part of the batch data to train
- min_data_in_leaf: another regularization, quite good to enlarge it to regularization for avoiding overfitting
- feature_fraction: just like dropout, very useful to set it like 0.5 (just like ensemble method)


### Solutions:
1. https://www.kaggle.com/c/avito-demand-prediction/discussion/59881 (LGBM)