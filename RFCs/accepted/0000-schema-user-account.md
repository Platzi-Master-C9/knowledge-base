- Start Date: (2022-02-23)
- Members: (Francisco Rojas - Marlon Ramirez)
- RFC PR: https://github.com/Platzi-Master-C9/knowledge-base/pull/65/commits
# Summary

Architecture Database Design for Account User and selection of what Database we should use.

# Basic example

In the following image is displayed the basic information that must be in our Database at least, more information will be added.

![image](https://user-images.githubusercontent.com/4333910/157151928-dfab5252-8954-49fe-b6e0-c66e61378336.png)

# Motivation

## Why are we doing this? 

One of the main objectives of making a DB scheme is to be able to create endpoint structures so that users can later interact with the application.

![image](https://user-images.githubusercontent.com/4333910/157153239-742341d9-4db1-4918-bd21-df3bf64b9dc4.png)

## What use cases does it support? 
Huge and success systems have had a well organized schema and applied the CAP theorem to select what Database is necessary for their project.

## What is the expected outcome? 
Having users personal information organized in a schema will help us to build a well structured database. It also will help us to scalate our product easily. We also expected that the Database chose by us is going to be enough to support the needs of our booking system.

# Detailed design

![image](https://user-images.githubusercontent.com/4333910/157153476-0376bfaa-bbb8-401a-bccb-e20150781729.png)

Since there's now a schema to follow. It's necessary to choose which Database is the most useful and efficient for our project. This's why we need the CAP Theorem to help us choose depending on which characteristics are needed in the user account (profile).

We decided our database should be CA (Consistensy and Availability) . First, Consistensy our users have to be able to see the same data no matter which node they connect to on the system. Second, Availability because our users have to see their data whenever thay woudl like to.

We decide to follow a relational BD due to we have identifiers in the previous schema that we allows to do a relation between tables, and we can use the SQL language for manipulating data.

## Why a relational Database was chosen?

### Non-relational databases: 
They are preferable to choose when the nature of our development’s structure would vary in the database.

### Relational databases: 

When there’s a clarity of the structure and relationship of the data, without the need for change

We bet on PostgreSQL as the relational database management system (RDBMS) in our project considering the following table of comparisons between the three most popular MySQL, PostgreSQL and SQL Server.

![image](https://user-images.githubusercontent.com/4333910/155855217-de363fe7-cbe9-43a0-a8d5-ada7e8cb7387.png)

Here they are the main PostgreSQL's characteristics:

High concurrence: It is capable of dealing with many clients at the same time and delivering the same information from its tables, without blocking.

Support for multiple data types natively. It offers the usual data types in management systems, but also many others that aren’t available in other competitors, such as IP addresses, MAC addresses, Arrays, decimal numbers with configurable precision, geometric figures, etc.

### Trigger support. 
It allows defining events and generating actions when they are triggers.

### Working with views.
This means that they can query the data in a different way than the way it is stored.

###  Object-relational. 
Another of its main features, allows you to work with your data as if they were objects and offers object-oriented mechanisms, such as table inheritance.

### Support for distributed databases.
Where working with transactions ensures that these will be successful when they have been able to be carried out in all the systems involved.

###  Support for a large number of languages.
PostgreSQL is capable of working with internal functions, which are executed on the server, written in various languages such as C, C++, Java, PHP, or Python. In addition, it offers interfaces for ODBC and JDBC, as well as programming interfaces for many programming languages.


# Drawbacks

## Why should we *not* do this? Please consider:

- Official Support

- PostgreSQL is not good when it comes to performance in comparison with the other Databases. PostgreSQL is often criticized for being slow and unsuitable for large-scale enterprise applications.

- Increasing horizontal scaling is complex, but PostgreSQL may have a solution for all replicas to accept operations.

- No column re-ordering and better data compression are required.

# Alternatives

MYSQL it can be a good option due to performance on inserts and updates

# Adoption strategy

It's necessary to understood the basic concepts in SQL Languajes like Joins and Querys 

# How we teach this

## What names and terminology work best for these concepts and why?

Schema = Show database using graphics, this way make it easy to understand how is data organized without looking at the code.

CAP theorem = The best proven way to select databases for projects. It gives you the exact answer of why you really need for your project (Consistency, Availability, Partition Tolerance)

## How is this idea best presented? 
It could be present in a short meeting. One of us could explain it.

## How should this feature be taught to existing C9 developers? 
It has two topics to explain. Topic # 1 (Schema of DB) and topic #2 (Why did we choose PostgreSQL?)

# Unresolved questions

This document doesn't include what Management Tools we are going to use with PostgreSQL 
