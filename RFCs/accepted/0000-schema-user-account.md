- Start Date: (2022-02-23)
- Members: (Francisco Rojas - Marlon Ramirez)
- RFC PR: (leave this empty)

# Summary

Aruitecture Database Design for Account User process

# Motivation

## Why are we doing this? 
We are doing a schema because users from our Booking need to fill in their basic information and our booking system can storage that information.

## What use cases does it support? 
Huge and success systems have had a well organized schema and applied the CAP theorem to select what Database is necessary for their project.

## What is the expected outcome? 
Having users personal information organized in a schema will help us to build a well structured database. It also will help us to scalate our product easily. We also expected that the Database chose by us is going to be enough to support the needs of our booking system.

# Detailed design

![image](https://user-images.githubusercontent.com/4333910/156262140-4d3c777c-f9ba-4d16-b767-f0629e89b769.png)

We decided our database should be CA (Consistensy and Availability) . First, Consistensy our users have to be able to see the same data no matter which node they connect to on the system. Second, Availability because our users have to see their data whenever thay woudl like to.

We decide to follow a relational BD due to we have identifiers in the previous schema that we allows to do a relation between tables, and we can use the SQL language for manipulating data.

We bet on PostgreSQL as the relational database management system (RDBMS) in our project considering the following table of comparisons between the three most popular MySQL, PostgreSQL and SQL Server.

![image](https://user-images.githubusercontent.com/4333910/155855217-de363fe7-cbe9-43a0-a8d5-ada7e8cb7387.png)

Our goal is to prioritize flexibility, cost-effectiveness and innovation, so our choice is an open source solution like PostgresSQL or MYSQL, but PostgreSQL excels at data querying and offers clear organization and temporary tables if we want to have a complex process, it also supports JSON. files which, being able to index these files, allows us to communicate with external data sources


# Drawbacks

## Why should we *not* do this? Please consider:

- Official Support

- PostgreSQL is not good when it comes to performance in compairisión with the another ones.

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

# Unresolved questions

This document doesn't include what Management Tools we are goint to use with PostgreSQL 
