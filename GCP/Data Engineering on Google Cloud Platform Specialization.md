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

### Lab 1
- Simple data pipeline in Python
https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/data_analysis/lab2/python/grepc.py

- using a function with **yield** to make a filyter
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
