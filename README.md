# AWS Glue (ETL)

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/AWS-Glue.png" alt="AWS Glue" width="200">
    </td>
    <td>
      AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy to prepare and load data for analytics.
    </td>
  </tr>
</table>


## Setting up the notebook environment
### Access Management (IAM)

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/IAM.png" alt="IAM" width="200">
    </td>
    <td>
      Define the IAM role and connections first. This enables AWS Glue to access and interact with other AWS services securely.
    </td>
  </tr>
</table>



```python
%iam_role arn:aws:iam:<your_iam_role>
%connections
```
### System Management Libraries

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/PySpark.png" alt="PySpark" width="200">
    </td>
    <td>
      Import PySpark and other libraries next. These are crucial for managing systems, data, and AWS services.
    </td>
  </tr>
</table>


```python
import sys
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from pyspark.sql import SQLContext
from awsglue.context import GlueContext
from awsglue.job import Job
from pyspark.sql import SparkSession
import os
import datetime
import pytz
import numpy as np
import pandas as pd
from pandas import DataFrame
import boto3
import s3fs
from itertools import product
from glob import glob
import json
```

Initialize SparkContext and GlueContext to interact with AWS Glue and Spark. Also, initialize a Job, which is a logical unit of work in AWS Glue.

```python
sc = SparkContext.getOrCreate()
glueContext = GlueContext(sc)
spark = glueContext.spark_session
job = Job(glueContext)
```

###### (If you want to learn more about Data Manipulation with PySpark en Python and its functionalities, check out the my project on : [Data Manipulation with PySpark](https://github.com/CatelloTheDataProjectManager/data_manipulation_with_pysapark/blob/main/README.md).)

### S3

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/S3.png" alt="S3" width="200">
    </td>
    <td>
      Use the s3fs library to interact with the S3 file system. This allows you to read and write data to and from S3 buckets securely and efficiently.
    </td>
  </tr>
</table>


```python
s3 = s3fs.S3FileSystem(anon=False)
```
### Accessing secrets from Secrets Manager

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/AWSSM.png" alt="AWS Secrets Manager" width="200">
    </td>
    <td>
      Use AWS Secrets Manager to store and retrieve sensitive data securely. This helps maintain the security and compliance of your ETL pipelines.
    </td>
  </tr>
</table>


```python
session = boto3.session.Session()
client = session.client(
    service_name='secretsmanager',
    region_name='eu-west-1')

get_secret_value_response_ymo = client.get_secret_value(
    SecretId='secret_name')
```
