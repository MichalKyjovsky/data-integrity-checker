# Data Integrity Checker

## Project Overview
Purpose of this project is to create a data integrity validation software, which would be capable to to connect to the data assets as deefined on input, connect to them and compare the data between them. General focus of this project is to provide support to a Big Data processing projects, which gathers data from several data sources, for instance Oracle, MSSQL, SAP HANA, Apache HIVE, Amazon Redshift, but also flat files such as Excell, CSV, or XML and compare them against the processed equivalents in either Data Warehouse or Data Lake. This use-case can be visualized in the diagram below - Use Case Architecture.  

## Use Case Architecture

![use-case-architecture](DataIntegrityChecker.svg)

Diagram above briefly visualize general process of Data Ingestion, i.e. the process when an ETL scripts or different component on PDC (Process Dispatch Center) invocation starts data gathering from several data assets to the Data Warehouse/Lake. 

## Application description

When data is being ingested and post-processed within its Data Warehouse, respectively Data Lake, a vast amount of transformation is performed. The purpose of this project is to verify, that the data integrity was persisted. Subsections below explains general and detailed usage.

### General usage 

The compiled code will reside in the Artifactory server in form of Docker Image. This will omit any installation or platform dependencies. Automated process, either Jenkins job or Github/GitLab CI will fetch the latest snapshot in order to perform the validation. Hosting environment, therefore needs only to provide Docker environment. Input of the program will be in form of configuration JSON (specification of format will be provided). The configuration will consist of database connection details (e.g. connection strings, credentials) and list of tables. Each table in the config file will be representing an object determining the tables metadata (Configuration file structure will be similar to output of SAP Power Designer). 

### Detailed usage - solution overview

The application will provide possibility to be executed in three modes:

1. **Count of record validation**
    The program will count records for each table in the tested database and compare it with the actual state on the target database.

2. **Full data integrity validation**
    The program will scan both data sources. Firstly the ***Count of record validation*** will be performed, then based on configured pool size will be data from each table fetched in the memory, transformed according the specification on the input and compared. Program does not need primary key to be defined, because it will expect that data are unordered (when primary key definition is broken). The application will then scan each table. Records from source system will be hashed and iterated in order to find the equivalent in the target. If no equivalent record is found, the record is sent to the buffer and after validation is finished will be flushed into reporting file with other invalid records. If the equivalent record is found, the actual comparison, i.e. cell after cell is being performed. In case of data discrepancy observation, the records will be handled as in case of previous example. When whole dataset is scanned, then the output archive consisting results of data comparison and summary report will be provided.

3. **Sample data integrity validation**
    If the dataset table consist of vast amount of records, the sampling will be performed. Sampling will be performed based on ANSI Z1.4 Standard (https://asq.org/quality-resources/z14-z19), hence based on the count of record will be determined number of random records to be tested. This technique strongly requires primary key definition, which will be tested for each table, before self comparison will be performed, therefore it is not meant to be used for Data Lakes architectures allowing duplicities in a single layers.     


## TODO: Provide system architecture
## TODO: Provide class diagram
