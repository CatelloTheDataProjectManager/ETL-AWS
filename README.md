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

### S3 system

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

### Python

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/python-logo.png" alt="Python Logo" width="200">
    </td>
    <td>
      With the AWS Glue notebook environment set up, you can now start transforming your data using Python and other AWS services.
    </td>
  </tr>
</table>

In real-life projects, AWS and Python have enabled me to perform ETL (Extract, Transform, Load) processes for various projects, such as this kind of project <a href="https://github.com/CatelloTheDataProjectManager/Customer-Segmentation/blob/main/README.md"> customer segmentation</a>.

### QuickSight

<table>
  <tr>
    <td>
      <img src="https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/amazonQuicksight.png" alt="Amazon QuickSight" width="200">
    </td>
    <td>
      After transforming the data, you can use Amazon QuickSight to visualize and analyze it. This tool helps you gain insights and make data-driven decisions.
    </td>
  </tr>
</table>


By leveraging the power of AWS Glue and other AWS services, you can build scalable, secure, and efficient ETL pipelines that enable you to extract valuable insights from your data.

#  Alternative to ETL pipelines on AWS

This project, **Cybersecurity_IA**, focuses on leveraging artificial intelligence to enhance data security. It serves as an alternative to traditional ETL pipelines on AWS, providing an efficient and flexible solution for managing and securing data. You can view an illustrative preview of my work [here](https://github.com/CatelloTheDataProjectManager/cybersecurity_IA).

In addition to this, I have worked on projects involving data encryption to ensure confidentiality and protection. To improve usability and interactivity, I utilized **Streamlit** to create a user-friendly front-end interface. For reproducibility and cross-device compatibility, I incorporated **Docker** into the workflow. This project highlights my expertise in AI, data security, and the use of modern tools to ensure reliability and scalability.

![Preview](https://github.com/CatelloTheDataProjectManager/ETL-AWS/blob/main/user_1.gif)
