# Helper Functions

```python
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

# value_counts
def value_counts(df_column, dropna=False):
  print(df_column.value_counts(dropna=dropna))
  print(df_column.value_counts(dropna=dropna, normalize=True))
  df_column.value_counts(dropna=dropna).plot(kind='bar')
```
