- Start Date: 2022-02-22
- Members: Omar Sánchez (@Omarsan-av), Joaquín Beltrán (@JoaquinAprendizaje) and Alejandro Cuartas (@Alejandrocuartas).

- RFC PR: (leave this empty)

# Summary

Design of Places data schema and choice of the database.

# Motivation

## Why are we doing this? 

The booking system obligatory requires a database that save the places data. The data of the places is essential for the business logic.
 
## What use cases does it support? 

- Addition of places to the Booking System
- Retrieve data of the Booking System's places

## What is the expected outcome?

- High consistency
- High availability
- Reasonable scalability 
- Learning friendly
- Quick implementation 
- Quick reading and writting operation

# Detailed design

Places schema has some models, atributes and relations taken from the requeriments and the business logic. It is also made up thinking in the communication between the diferent squads.

![Database schema](https://res.cloudinary.com/dvpcbukeh/image/upload/v1645622908/image_67172353_hqlavr.jpg)

Some tables need an user_id. This atribute is taken from the User squad database.

## data types and constraints

![datatypes and constraints](https://res.cloudinary.com/dvpcbukeh/image/upload/v1645623035/InkedWhatsApp_Image_2022-02-19_at_4.16.10_PM_LI_bgdkvb.jpg)

## flows

### User and guest flow

![user and guest flow](https://res.cloudinary.com/dvpcbukeh/image/upload/v1645620892/user_guest_flow_iwqvaz.png)

### host flow

![host flow](https://res.cloudinary.com/dvpcbukeh/image/upload/v1645620892/host_flow_aljumt.png)

# Drawbacks

- Low partition resilience
- In case of having complex queries, the reading operation would get slow 
- Struggles with concurrency peaks
- The relational databases are very inflexible

# Alternatives

We also consider to use:

- MongoDB which has more flexibility in data schema, better partitioning resilience and scalability.

- PostgreSQL which is more scalable, more flexible and has a better processing of complex queries.

# Adoption strategy

The first 12 classes of Platzi course Fundamentos de Bases de Datos have enough information about relational databases. We created the data schema with this resources. 

The next step is to learn MySQL basics watching the 13-39 classes of the same course or going directly to the documentation.

The last step is to learn about NPM library 'mysql' for managing the database from Node.js.

# Unresolved questions

