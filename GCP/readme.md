```python
# For reading the data from Cloud Storage
import google.datalab.storage as storage
import pandas as pd
from io import BytesIO

mybucket = storage.Bucket('bucket_name')
data_csv = mybucket.object('file_name.csv')

uri = data_csv.uri
%gcs read --object $uri --variable data

df = pd.read_csv(BytesIO(data), sep='|')

```
