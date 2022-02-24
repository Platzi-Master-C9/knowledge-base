- Start Date: (2021-02-22)

- Members: (Yair E. Riascos, Jhon Isnober Diaz, Nelson Loyola)

- RFC PR: 

  

# Summary

In this RFC we're going to discuss the way to build a data pipeline from scratch, which involves the extraction of the data from the booking and places databases and then transform the information in order to load it into a data warehouse.

  

# Motivation

Data treatment is a critical issue for enterprises or companies that have to deal with big volumes of information. In this cases they must assure at least the V3 principels of the big data (volume, variety and velocity) which involve a big challenge for building a robust solution that assure integrity, consistency and availabilty on the data pipelines.

Having all this well supported makes easier the data visualization and finding insights that reflects predictive behavior at the future (All this would be very handy for data analyzers and decision takers).

** Agregar caso de uso ***
- Soporte al area de administracion para la toma de decisiones de infraestructura, contando con las metricas de performance

  

# Detailed design

According to the C4 model proposal we need to extract the information from 2  sources (booking and places containers).
 
The main tool for the pipeline development is going to be **Python** and its most common libraries. 

- Numpy.
- Pandas.
- Seaborn.
- Mathplotlib.

Tools for extracting the information:

 - Apache Airflow using batch processing.
The reason for this choice is based on Airflow scheduler, which allows you to separate the tasks from crons and easily scale them independently. 

The resources for staging may vary due to the type of database implemented by other teams. 

- **Postgress**: is suitable in this case because is an open-source RDBMS  and it's easy way to create data warehouse for initial proyects.

The outcome of all this will be delivered via API REST service, so there'll be endpoints that allows other teams read all the curated information.

- Node.js, 
- Express.js as a backend library.
- Sequelize as an ORM for modeling the results coming from the DB.


