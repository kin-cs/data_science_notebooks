### In Datalab, reading file from Google Cloud Storage

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

# if it's not csv, but pickle, them
# import pickle
# df = pickle.load(BytesIO(data))
```

### In Datalab, writing file in GCS 
1. after saving it into the datalab's disk, then:
```python
!gsutil cp 'text.csv' 'gs://path-to-your-bucket/test.csv'
```
2. using Dask to save it in GCS

Creating/generating API in GCP
--------------------------
- https://cloud.google.com/endpoints/docs/frameworks/python/get-started-frameworks-python

Datalab
------
- the path of datalab content is: ```/media/root/mnt/disks/datalab-pd/content/datalab``` if in root by toolbox or ```/mnt/disks/datalab-pd/content/datalab``` if directly in its SSH
- Look all shortcuts: press esc to enter command mode, then press H.

Tips
---
- Download file from VM to local:
  - In GCP console, ssh into the vm and on top right corner there is a settings button, there you will find the download file option just enter the path of file. if it is folder then first zip the folder then download it. [ref](https://stackoverflow.com/questions/44982313/how-to-copy-files-from-google-compute-engine-to-local-directory)


## IAM
- 3 Names: Identity, Role, Resource
  - Go to your project
  - Go to IAM
  - assign the role for your user
