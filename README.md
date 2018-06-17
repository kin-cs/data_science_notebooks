# data_science_notebooks

## Freq Use

## Pandas
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
import sklearn

%matplotlib inline

pd.options.display.max_columns = 999  # VERY IMPORTANT!!!

from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"

# using .eq('something')
df[df['col_A'].eq('some_term')]

# using .quary('some quary')
df.query("col_A == 'some_term'")

# using .isin( a_list )
df['col_A'].isin(a_list_of_terms)

# using 'hello'.replace('o','a')  # replacing the string of o with a

# using 'hello2222'.strip('2')  # return 'hello'

# using in print() function, using argument file=file_object to write in a file

# checking NaN and return Boolean
df['col_A'].isnull() 

# making bins columns
age_bins = np.arange(0, 80, 5)
pd.cut(df['col_age'], age_bins, right=False)

# unpacked multi items when using apply
df[['sum', 'difference']] = df.apply(lambda row: pd.Series(add_subtract(row['a'], row['b'])), axis=1)

```

# Kaggle
### Kernel Ref.

- U-nets: https://www.kaggle.com/lscoelho/keras-u-net-lb-0-277-epochs-vsplit-thr

## Avito

### LightGBM hyper-parameter tuning
- Optimization software: Hyperopt, scikit-optimize, spearmint...
- num_leaves: more powerful it is
- bagging_fraction: just take part of the batch data to train
- min_data_in_leaf: another regularization, quite good to enlarge it to regularization for avoiding overfitting
- feature_fraction: just like dropout, very useful to set it like 0.5 (just like ensemble method)
