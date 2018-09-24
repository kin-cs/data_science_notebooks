Course 1 - Google Cloud Platform Big Data and Machine Learning Fundamentals
===========================================================================

Keys
===

- Read the details here in **https://cloud.google.com/solutions/**
- Security: **https://cloud.google.com/security/**

Datastore
---
- Cloud Datastore: NoSQL, is not a relational database, and it is not an effective storage solution for analytic data

Misc
====
- Pricing Calculator
- Cloud Launcher
  - deploy the pre-installed things

History
=======
- 2008, Google lanuched App Engine
- Now, Google Container Engine

Advantages:
-----------
- Cost effective
- Reliable
- Auto-scaling

Service:
-------
- DATAPROC: fully-managed cloud service for running Apache Spark and Apache Hadoop clusters in a simpler, more cost-efficient way
- Cloud SQL: for not so large data (GB)

Labs I've gone through
=====================

Create ML Dataset with BigQuery
--------

- Use BigQuery and Datalab to explore and visualize data
- Build a Pandas dataframe that will be used as the training dataset for machine learning using TensorFlow

### Launch Cloud Datalab
In Cloud Shell, type:

```gcloud compute zones list```
Pick a zone in a geographically closeby region.

In Cloud Shell, type:

```datalab create bdmlvm --zone <ZONE>```


Lab Exercises
===

Course 2 - Dataproc, Leveraging Unstructured Data with Cloud Dataproc on Google Cloud Platform
===================

### Lab 1: Create a Dataproc Cluster

- Prepare a bucket for cluster initialization
- Create a Dataproc Hadoop Cluster customized to use the Google Cloud API
- Enable secure access to the Dataproc cluster
- Explore Hadoop operations

- Create the source file for setting and resetting environment variables

- ports 8088 (Hadoop Job Interface) and 9870 (Hadoop Admin interface)


Course 3 - BigQuery & Dataflow, Serverless Data Analysis with Google BigQuery and Cloud Dataflow
===================

- SQL example
```sql
WITH
  commits AS (
  SELECT
    author.email,
    LOWER(REGEXP_EXTRACT(diff.new_path, r'\.([^\./\(~_ \- #]*)$')) lang,
    diff.new_path AS path,
    author.date
  FROM
    `bigquery-public-data.github_repos.commits`,
    UNNEST(difference) diff
  WHERE
    EXTRACT(YEAR
    FROM
      author.date)=2016 )
SELECT
  lang,
  COUNT(path) AS numcommits
FROM
  commits
WHERE
  LENGTH(lang)<8
  AND lang IS NOT NULL
  AND REGEXP_CONTAINS(lang, '[a-zA-Z]')
GROUP BY
  lang
HAVING
  numcommits > 100
ORDER BY
  numcommits DESC
```

Dataflow
-------

- the MapReduce process should be commutative & associative
  - using **yield** and **FlatMap** iare very important for doing this process in Python

### Lab 1
- Simple data pipeline in Python
https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/data_analysis/lab2/python/grepc.py

- using a function with **yield** to make a filter
```python
def my_grep(line, term):
   if line.startswith(term):
      yield line
## ...
# find all lines that contain the searchTerm
(p
  | 'GetJava' >> beam.io.ReadFromText(input)
  | 'Grep' >> beam.FlatMap(lambda line: my_grep(line, searchTerm) )
  | 'write' >> beam.io.WriteToText(output_prefix)
)
```

### GroupBy and Combine
- beam.GroupByKey()
- beam.Combine.perKey(sum)

### Lab 2
- Typical example of count every value as a tuple (key, 1), then use Combine.perKey(sum) to count the word/term
https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/data_analysis/lab2/python/is_popular.py

Course 4 - ML & TF in GCP
========================

some revisit
------------

### Misc:
- Try play around playground for TF
- get some negative/near samples to train a better model

### Metrics:
- For model training
  - Regression model: MSE, RMSE
  - Classification model: cross-entropy (=log loss)
- For performance (for presenting to stakeholders:

### Typical Procedure of a ML project
1. Explore
2. Create datasets for modeling
  - regression/classification
  - what is the label?
  - what are the features?
  - ML steps:
    - train the model 
    - evaluate the model (with validation set)
    - predict the model (with unseen test set)
3. Benchmark
  - use confusion matrix
    - precision
    - recall

### Lab 1
- Using datalab
  - ```gcloud compute zones list``` choose a zone, then
  - ```datalab create dataengvm --zone <ZONE>```
  - it will take ~ 5 mins to start
https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/machine_learning/datasets/create_datasets.ipynb
- use ```%sql --model <name of query>``` to create the query: example
```
%sql --module afewrecords
SELECT pickup_datetime, pickup_longitude, pickup_latitude, dropoff_longitude,
dropoff_latitude, passenger_count, trip_distance, tolls_amount, 
fare_amount, total_amount FROM [nyc-tlc:yellow.trips] LIMIT 10
```
- then use bq (import datalab.bigquery as bq) to read it as the pandas' df
```trips = bq.Query(afewrecords).to_dataframe()```

Tensorflow (revisit)
------------------

- lazy evaluation: so it separates the creation of the graphs with the execution
```python
# buil
...
c = tf.add(a, b)

# run (lazy evaluation)
session = tf.Session()
numpy_c = session.run(c, feed_dict= ...)
```
- placeholder & feed_dict : as its name
```python

aa  ==  tftf..placeholderplaceho (dtype=tf.int32, shape=(None,))  # batchsize x scalar
b = tf.placeholder(dtype=tf.int32, shape=(None,))
c = tf.add(a, b)
with tf.Session() as sess:
  result = sess.run(c, feed_dict={
      a: [3, 4, 5],
      b: [-1, 2, 3]
    })
  print(result)
## result > [2 6 8]
```

### Lab 2 - TF
https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/machine_learning/tensorflow/a_tfstart.ipynb

- Estimator API
  1. create feature_columns
  2. create input_function (it also indicate x(whole data, with y) and y(the label)
  3. choose LinearRegressor/LinearClassifier/DNNRegressor... and build the model

