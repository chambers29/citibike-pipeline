# CITI-BIKE TRIPDATA PIPELINE

## Summary
---
This pipeline is designed to ingest, transform, and standardize all publicly available Citi Bike trip data.
>Data source: https://s3.amazonaws.com/tripdata/index.html

You can select specific years or even download all available data.
The **silver_pipeline** normalizes and stores the data in your cloud environment.
The **gold_pipeline** then processes this standardized data to produce insights.

The entire solution was built and tested on **Databricks** platform.

## Structure
---
- [data_ingestion/](data_ingestion/) - downloading and extracting raw data to bronze storage
  - [01_zip_download](01_zip_download.ipynb) - downloads monthly ZIP archives from the source
  - [02_zip_extraction](02_zip_extraction.ipynb) - extracts CSV files and prepares raw data
- [data_transformation/](data_transformation/) - main transformation logic for Silver and Gold layers
  - [silver_pipeline](silver_pipeline.ipynb) - standardizes schemas and cleans datasets
  - [gold_pipeline](gold_pipeline.ipynb) - aggregates and generates analytical outputs
  - [gold_utils](gold_utils.ipynb) - functions used by Gold transformations
- [exploration/](exploration/) - notebooks used to explore processed data
- [test/](test/) - testing before main apply

## Technologies
---
***Databricks*** – platform used to build and run the project

***Apache Spark (PySpark)*** – engine for processing and transforming big data

***Delta Lake*** – file format for storing cleaned and processed data

***Azure Data Lake Storage Gen2 (ADLS)*** – cloud storage for all data layers

***Python*** – main programming language used in the pipeline

## Run explanation
---
The pipeline runs in ***Databricks Jobs*** as a series of connected tasks:

*01_zip_download* → *02_zip_extraction* → *silver_pipeline* → *gold_pipeline*

### Data flow:

*01_zip_download* – from Citi Bike website → to downloads folder

*02_zip_extraction* – from downloads → to Bronze layer

*silver_pipeline* – from Bronze → to Silver layer

*gold_pipeline* – from Silver → to Gold layer

>You can run the whole job or execute each notebook separately.
>Some notebooks use widgets (parameters), for example:

> - *years* – select which years to process




















