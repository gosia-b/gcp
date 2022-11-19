# 🔍 BigQuery ML
BigQuery ML enables users to create and execute ML models in BigQuery using SQL queries.  
The goal is to:
* democratize ML (because SQL is easy)
* increase development speed by eliminating the need for data movement

# Create a model
```sql
#standardSQL
CREATE OR REPLACE MODEL `dataset_name.sample_model` 
OPTIONS(model_type='logistic_reg') AS
SELECT
  IF(totals.transactions IS NULL, 0, 1) AS label,
  IFNULL(device.operatingSystem, "") AS os,
  device.isMobile AS is_mobile,
  IFNULL(geoNetwork.country, "") AS country,
  IFNULL(totals.pageviews, 0) AS pageviews
FROM
  `bigquery-public-data.google_analytics_sample.ga_sessions_*`
WHERE
  _TABLE_SUFFIX BETWEEN '20160801' AND '20170631'
LIMIT 100000;
```

Notice there is a `label` column.

# Model info & training statistics
Click on model name to get information about it.  
Under Details, you should find some basic model info and training options used to produce the model.  
Under Training Stats, you should see a table similar to this:

# Reference
[Codelabs - Getting started with BigQuery ML](https://codelabs.developers.google.com/codelabs/bqml-intro)  
