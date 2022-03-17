- Start Date: 02-23-2022
- Members: [Jhon Isnober Díaz Ruiz](https://github.com/jhonny3e7), [Yair Riascos](https://github.com/yeiror) 
- RFC PR: 
​
# Summary
​
This RFC pretends to expose the stack that we choose for the ETL pipelines to use inside the Booking System Project.
​
​
In this RFC we're going to discuss the way to build a data pipeline from scratch, which involves the extraction of the data from the booking and places databases and then transform the information in order to load it into a data warehouse.
​
​
# Basic Example
​
​
​
# Motivation
​
​
Data treatment is a critical issue for enterprises or companies that have to deal with big volumes of information. In this cases they must assure at least the V3 principels of the big data (volume, variety and velocity) which involve a big challenge for building a robust solution that assure integrity, consistency and availabilty on the data pipelines.
​
Having all this well supported makes easier the data visualization and finding insights that reflects predictive behavior at the future (All this would be very handy for data analyzers and decision takers).
​
As a startup we choose a open-source stack in order to keep the cost lower, without ignore the performance we need in order to keep growing faster.
​
## ETL Process
![ETL](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/95fd188c-0933-4c47-accb-cb9f84b673fc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220303%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220303T200430Z&X-Amz-Expires=86400&X-Amz-Signature=b94744ecf0df2585e0a073aa60203560d1612b87fd17fa718ae32e9e0d07a6b9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
​
​
**ETL** stands for **E**xtract, **T**ransform, and **L**oad, which are the three steps of the ETL process. It collects and process data from various sources into a data store (e.g. a data warehouse or a data lake), for further analysis.
​
When an ETL process is used to move data into a data warehouse, a separate layer represents each phase:
​
**Mirror/Raw layer:** This layer is a copy of the source files or tables, with no logic or enrichment. The process copies and adds source data to the target mirror tables, which then hold historical raw data that is ready to be transformed.
​
**Staging layer:** Once the raw data from the mirror tables transform, all transformations wind up in staging tables. These tables hold the final form of the data for the incremental part of the ETL cycle in progress.
​
**Schema layer:** These are the destination tables, which contain all the data in its final form after cleansing, enrichment, and transformation.
​
**Aggregating layer:** In some cases, it's beneficial to aggregate data to a daily or store level from the full dataset. This can improve report performance, enable the addition of business logic to calculate measures, and make it easier for report developers to understand the data.
​
​
### Extract
Extracting data means pull (Extract) data from one or more data sources or implement a way to receive the data sent from sources (Ingest). During the extraction phase of ETL, you may handle a variety of sources with data, such as:
​
- Relational and non-relational databases.
- Flat files (e.g. XML, JSON, CSV, Microsoft Excel spreadsheets, etc.).
- SaaS applications, such as CRM (customer relationship management) and ERP (enterprise resource planning) systems.
- APIs (application programming interfaces).
- Websites.
- Analytics and monitoring tools.
- System logs and metadata.
​
We divide ETL into two categories: **batch ETL** and **real-time ETL** (a.k.a. streaming ETL). Batch ETL extracts data only at specified time intervals. With streaming ETL, data goes through the ETL pipeline as soon as it is available for extraction.
​
We choose to implement an **API* where the application source will deliver the information.
​
**API**.  **A**pplication **P**rogramming **I**nterface, is a set of programming code that enables data transmision between one software product and another.
​
​
### *Transform*
It's rarely the case that your extracted data is already in the exact format that you need it to be. For example, you may want to:
​
- Rearrange unstructured data into a structured format.
- Limit the data you've extracted to just a few fields.
- Sort the data so that all the columns are in a certain order.
- Join multiple tables together.
- Clean the data to eliminate duplicate and out-of-date records.
- All these changes and more take place during the transformation phase of ETL. There are many types of data transformations that you can execute, from data cleansing and aggregation to filtering and validation.
​
In this part we choose **Apache Airflow**, because it works with python.
​
### Load
Finally, once the process has transformed, sorted, cleaned, validated, and prepared the data, you need to load it into data storage somewhere. The most common target database is a data warehouse, a centralized repository designed to work with BI and analytics systems.
​
In this section of the process, we choose to work with **Postgres**.
​
​
### Visualization
With the data already curated, we can use them for extract useful insights.
​
​
​
# Detailed Design
​
Based on the motivations explained, we'll list the following tools we are going to use for the data pipelines:
​
## Extract 
  - API (Ingest)
    - **Python**.  The programming language.
      - Easy and readable.
      - Asyncronous coding.
      - OOP.
      - Rich Standard library.
      - Rich ecosystem.
      - software testing.
      - Visualization options.
      - Best choice to integrate (Apache Airflow)
      - Open Source.
​
​
    - **Flask**.  The application Framework
      - Is the balanced choice between performance, flexibility, community, packages availables, among the others best options (Django, FastApi).
      - Beginner friendly.
      - Open Source.
​
## Transform
  - **Apache Airflow**
    - Use Python to create workflows and tasks.
    - Scheduler, which allows you to separate the tasks from crons and easily scale them independently. 
    - Easy to use.
    - Open Source.
​
## Load
  - **Postgress**: 
    - Open Source.
    - Integration with Heroku.
    - Can work with spatial information (PostGIS).
    - Can work with time series (TimescaleDB)
​
## Visualization
  - **Pandas, Mathplotlib and Seaborn**.
    - Python libraries.
    - D3.js
​
The outcome of all this will be delivered via API REST service, so there'll be endpoints that allows other teams read all the curated information.
​
​
## ETL Schema
![ETL Schema](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/004c5d02-0ef0-494b-a60a-c788e8702427/datawarehouse_schema.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220303%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220303T200532Z&X-Amz-Expires=86400&X-Amz-Signature=a8792d8e326eb0fad117233a04bd2b5972bf0b091ed0f12fb2cc933e0ef4374a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22datawarehouse_schema.png%22&x-id=GetObject)
​
# Drawbacks
​
Why should we *not* do this? Please consider:
​
- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)
​
​
# Alternatives
​
- Alternatives to API:
  - Apache Kafka. Message broker with integration in Heroku. https://www.redhat.com/es/topics/integration/what-is-apache-kafka
  - The API could be done with fastify framework for NodeJS.
​
- Alternatives to Python:
  - **Nodejs**. (Javascript).  Better performance.
​
- Alternatives to Flask:
  - **Django**. The most mature and the better community for python Frameworks.
  - **FastApi**. The faster option for Python Frameworks.
  - **Express.js**.  Backend framework for Node.js
  - **Fastify**.  Fast Framework for Node.js
​
​
- Alternatives to Apache Airflow:
  - **Pandas**. It easy to work with, poorly scalable.
  - **Luigi**. Better for complex pipelines.
  - **Ploomber**.
  - **Prefect**.
​
- Alternatives to PostgreSql
  - **Mongo**.
  - **Elasticsearch**.
  - **Influxdb**.
​
​
​
# Adoption strategy
​
If we implement this proposal, how will existing C9 developers adopt it? Is this a breaking change? Can we write a codemod?.  Should we coordinate with other projects or libraries?
​
​
​
# How we teach this
​
What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing C9 projects patterns?
​
Would the acceptance of this proposal mean the C9 documentation must be
re-organized or altered? Does it change how C9 is taught to new developers
at any level?
​
How should this feature be taught to existing C9 developers?
​
# Unresolved questions
​
Optional, but suggested for first drafts. What parts of the design are still
TBD?
