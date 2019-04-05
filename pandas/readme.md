# Pandas

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

# using in print() function, using argument file=file_object to write in a file

# checking NaN and return Boolean
df['col_A'].isnull() 

# making bins columns
age_bins = np.arange(0, 80, 5)
pd.cut(df['col_age'], age_bins, right=False)

# unpacked multi items when using apply
df[['sum', 'difference']] = df.apply(lambda row: pd.Series(add_subtract(row['a'], row['b'])), axis=1)

# rolling avg based on the previous data
# https://stackoverflow.com/questions/28642511/how-to-apply-rolling-functions-in-a-group-by-object-in-pandas
df.index = [pd.to_datetime(str(x), format='%Y%m%d') for x in df.index]
df.reset_index(inplace=True)
def avg_3_days(x):
        return df[(df['index'] >= x['index'] - pd.DateOffset(3)) & (df['index'] < x['index']) & (df['fruit'] == x['fruit'])].amount.mean()

df['res'] = df.apply(avg_3_days, axis=1)
df
'''
  ==result==
         index   fruit  amount  res
  0 2014-01-01   apple       3  NaN
  1 2014-01-02   apple       5    3
  2 2014-01-02  orange      10  NaN
  3 2014-01-04  banana       2  NaN
  4 2014-01-04   apple      10    4
  5 2014-01-04  orange       4   10
  6 2014-01-05  orange       6    7
  7 2014-01-05   grape       1  NaN
'''

# Fill na in categorical columns
df['some_col'] = df['some_col'].cat.add_categories(['new_dummy_cat'])
df['some_col'].fillna('new_dummy_cat')

# Add 2 columns together as 1 new column
df['new_col'] = df.apply(lambda x : pd.Series(x['col_A'] + x['col_B']), axis=1)

```

## Manipulate the string
```python
# replacing the string of o with a
'hello'.replace('o','a')  # return 'hella'

# strip
'hello2222'.strip('2')  # return 'hello'

# check if any characters in a string
any(c.isalpha() for c in a_string)
```

## My helper functions
```python
## Helpers

# Print available pct:
def print_avail(x, pct_threshold=75):
  x_avail = 100 - x.isnull().sum() * 100 / len(x)
  x_avail = pd.DataFrame(x_avail)
  x_avail['new'] = x_avail[0] > pct_threshold

  x_avail.columns = ['available %', 'Pass']
  print('Passing threshold is: ', pct_threshold, '\n')
  print('The size of the dataset is: {}\n'.format(len(x)))
  with pd.option_context('display.max_rows', None, 'display.max_columns', None):
      print(x_avail)

def value_counts(df_column, dropna=False):
  print(df_column.value_counts(dropna=dropna))
  print(df_column.value_counts(dropna=dropna, normalize=True))
  df_column.value_counts(dropna=dropna).plot(kind='bar')
  
def change_datatypes(dataframe, to_categ=None, to_float32=None, to_int32=None, to_dt=None, datetime_fmt="%Y-%m-%d"):
  dtypes_list = [(to_categ, 'category'), (to_float32, 'float32'), (to_int32, 'int32')]
  for a_list, data_type in dtypes_list:  
    if a_list:
      for i in a_list:
        dataframe[i] = dataframe[i].astype(data_type)
  if to_dt:
    for i in to_dt:
      dataframe[i] = pd.to_datetime(dataframe[i], format=datetime_fmt)
  print('Change success!\n===========')
  print(dataframe.dtypes)
  
def skim_df(dataframe, samples=3):
  df_samples = dataframe.sample(samples)
  col_names = df_samples.columns.tolist()
  df_samples = df_samples.append(pd.DataFrame(dataframe.dtypes, columns=['dtype']).T)
  data_types = ['object', 'category', 'datetime', 'number']
  for i in data_types:
    try:
      df_samples = df_samples.append(dataframe.select_dtypes([i]).describe())
    except:
      pass
  return df_samples[col_names]
```

## Advanced

### Using Ufuncs in groupby
(e.g. .diff, .shift, .cumsum, .cumcount, .str commands, .dt commands)
- https://towardsdatascience.com/pandas-tips-and-tricks-33bcc8a40bb9

### Using Modin to speed up Pandas
- ```pip install modin```
```python
# import pandas as pd
import modin.pandas as pd
```
