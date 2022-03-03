# RFC 000 WIP: Data Pipeline

+	Start Date: (2022-03-02)
+	Members: Omar Orozco, Nicholás Castañeda and Luis Tapia
+	RFC PR

## Summary

The proposed pipeline will be an ETL: It will extract the data collected by the Data Monitoring team, perform transformations and calculate the corresponding metrics, and then export the results to a Postgresql database. For the reading and transformation of data, a script will be made under the Python language and various modules and libraries will be used.


## Basic Example

**1. Data Ingestion**

For reading the API created by the Data Monitoring team, it is proposed to use the Requests library. The requests library is the de facto standard for making HTTP requests in Python. It abstracts the complexities of making requests behind a beautiful, simple API so that you can focus on interacting with services and consuming data in your application.

Example


<img width="800" alt="image" src="https://user-images.githubusercontent.com/69235190/156486657-e64d4f22-40c3-4b2f-9e41-0a66fb47f2f3.png">
<img width="800" alt="image" src="https://user-images.githubusercontent.com/69235190/156486721-196a1d21-2af4-452c-b73b-c1a92d20daa7.png">
<img width="800" alt="image" src="https://user-images.githubusercontent.com/69235190/156486733-7ef7f0cf-dab2-4f70-a097-5186fbf3c1b0.png">
<img width="800" alt="image" src="https://user-images.githubusercontent.com/69235190/156486741-3be95c2b-af43-42c9-b2be-e93cf0a775df.png">


**2. Data Transformation**

For the analysis and transformation of information in tables, it is recommended to use the Pandas library, which is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and to manipulate numerical tables and time series.
Pandas has a method that allows converting the information from a JSON to a Dataframe. This step is necessary to be able to structure the information received in a table and to be able to take advantage of the functions of the library. 

Example:

We have the following JSON

<img width="500" alt="image" src="https://user-images.githubusercontent.com/69235190/156487038-4fe70006-85a0-482c-99d6-aab167cf51ca.png">

To read a JSON file via Pandas, we can use the read_json() method.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/69235190/156487083-78001d0a-bec2-4a92-b5db-014305edfb1b.png">

Once you have the dataframe, you can use the properties. For example, one of the Pandas methods allows knowing the information of the columns and the type of data they have.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/69235190/156487299-90a8fa9a-d52c-4b2a-962e-b14c1b0e3170.png">



**3.	Data Visualization**

For data visualization, it is recommended to use a library such as matplotlib.pyplot. Every pyplot function makes some change to a figure: for example, create a figure, create a plot area on a figure, draw some lines on a plot area, decorate the plot with labels, etc. For example: 

<img width="600" alt="image" src="https://user-images.githubusercontent.com/69235190/156487362-2a91e8cb-35a6-44b3-860b-c1552569e3c4.png">


In case we require a more complex and interactive graphics library, it is recommended to use Seaborn. This is a Python data visualization library based on matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics

<img width="600" alt="image" src="https://user-images.githubusercontent.com/69235190/156487479-0cad2599-2a2e-4fbd-b3e5-916f47c69375.png">

Example:


<img width="600" alt="image" src="https://user-images.githubusercontent.com/69235190/156487508-230040db-56d9-4be2-bcb0-94a9b02b4d38.png">
<img width="650" alt="image" src="https://user-images.githubusercontent.com/69235190/156487588-e7353895-baf3-48f1-b392-1117462d7b00.png">



**4.	Data Loading**

It is proposed to connect and save the information in a PostgreSQL database. This is currently recognized as one of the most powerful relational database management systems on the market. It is easily accessible, cross-platform and available for use on almost all operating systems used today without slowing down its performance.

We can integrate Postgres with Python using the psycopg2 module. psycopg2 is a Postgre database adapter for Python.



Example of a connection: 

<img width="700" alt="image" src="https://user-images.githubusercontent.com/69235190/156487668-1867b8bd-accb-4fdb-84ec-3e50e4ced819.png">



Example of a data load:

<img width="700" alt="image" src="https://user-images.githubusercontent.com/69235190/156487697-57541eff-f418-4e3d-b481-3bb5815dc39e.png">


## Motivation

The main purpose is to be able to prepare and fix the data to calculate the business metrics of the Booking System application. On the other hand, choosing an adequate data pipeline will allow the creation of an adequate data processing process that can collect information from different squads, process it in real time and transform it so that it can be analyzed without compromising user security or performance. of processing.




## Detailed Design


<img width="800" alt="image" src="https://user-images.githubusercontent.com/69235190/156487933-18d70390-c4a5-4cf3-b99d-be00ae252c1d.png">


There are 3 phases: Extraction (1), transformation (2) and loading (3)


**1. Extraction**

Consists of collecting the information from the API developed by the Data Monitoring team. In this phase we expect to receive the following tables with the following columns:

●	**Users Table**

-	User type (host or guest)
-	User creation date
-	Coordinates or location
-	Age
-	Type of property (If he is a host, it is the type of property he owns / If he is a guest, it is the type of property he likes to rent)
-	Status (If the account is active or not)


● **Reservations Table**

-	Site location
-	Status (Confirmed, pending or rejected)
-	Date
-	Host user
-	Guest user
-	Price


● **Propertys Table**

-	Building status (Available or not)
-	Qualification
-	Square meter
-	Number of rooms
-	Property type
-	Number of bathrooms
-	Description of the bathroom
-	Kitchen
-	Balcony
-	Terrace
-	Climate
-	Cell phone coverage
-	Internet coverage
-	Price per night

● **Searches Table**

-	Search date
-	User who made it

● **Sessions Table**

-	Login date
-	Login User


● **Conversation Table**

-	Host User
-	Guest User
-	Messages sent to the host
-	Messages sent to the caller





**2.	Transformation**

Phase II consists of data transformation. With the collected tables, the following variables will be filtered and extracted:
-	Searches made with date
-	Sessions started with date
-	Location or coordinates of each reservation
-	Reservations confirmed with date
-	Reservations or requests not confirmed with date
-	Register of users created with date / Register of sessions started with date
-	Number of accommodations
-	Number of registered users
-	Accountless user sessions
-	Location of users
-	Age of the hosts
-	Age of the guests
-	Type of property owned by the Hosts
-	Type of property that guests like
-	Daily booking notifications
-	Number of chats or conversations started
-	Messages sent by users (To do sentiment analysis)
-	Rating of accommodation
-	Property specifications: square meters, number of rooms, type of property, number of bathrooms, description of the bathroom, if it has a balcony, if it has a terrace, climate, cellular network coverage, internet coverage, etc.
-	Accommodations made by Hosts
-	Accommodations requested by Guests
-	Deactivated accounts with their date
-	Accommodations made with price and dates
-	Number of active reservations
-	Total reservations (cancelled and active)
-	And other useful variables that may arise


**3.	Loading** 

Phase III consists of loading these variables into a PostgreSQL database. These are the variables necessary to perform the calculation of metrics required by the BI team. When these variables are saved in a database, they will be available for the calculation of metrics and visualization of the information generated.



## Drawbacks

The problems that can occur are:
-	Data on aspects of a different nature and format
-	Data that is constantly generated and must be collected in real time
-	Data generated by different squads and therefore come from various sources
-	Huge amount of data to process
-	Data on confidential information
-	Slow reading, transformation and loading of data
-	If the data is not accurate, reliable and robust, we will end up with incorrect or misleading results.


## Alternatives

Our own Pipeline design might fall short in some respects, have performance issues, or have inadequate structure and control. In case a more complex and specialized system is required, there is the Apache Airflow framework, which is an open source tool to manage, monitor and plan workflows. It is used to automate jobs by dividing them into subtasks and is common in automating data ingestion, regular maintenance actions, and management tasks. Airflow is also quite useful for managing ETL processes (Extract, Transform, Load), integrates a simple user interface, allows backups, generate reports and metrics.

A big disadvantage of using this tool is its high learning curve. DevOps knowledge is probably required to manage the entire process due to how customizable and complex it can become.

## Adoption strategy

It is necessary to learn concepts of ETL, handling of APIs with Python, SQL databases and the use of libraries such as Pandas, Requests, Matplotlib.Pyplot, Seaborn and any other library that can help solve problems that arise.

## How we teach this

All the libraries and resources proposed are Open Source. All have resources, support and contributions from thousands of users who have collaborated in the development and teaching of these resources. In addition, they all have a website where you can find their official documentation.

The Plazi platform also has courses and tutorials on them. In addition, any questions that arise can be consulted in the slack channel so that the rest of the team can help solve them.

## Unresolved questions

It is necessary to define if the appropriate database is PostgreSQL. It is also necessary to coordinate with the Data Monitoring team to know how to connect to their API and what variables they can export to us. Finally, it is also necessary to define where and how the metrics that will be calculated with the generated information will be displayed.
