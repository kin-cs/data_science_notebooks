# data_science_notebooks

## Freq Use

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

```

# Kaggle
### Kernel Ref.

- U-nets: https://www.kaggle.com/lscoelho/keras-u-net-lb-0-277-epochs-vsplit-thr
