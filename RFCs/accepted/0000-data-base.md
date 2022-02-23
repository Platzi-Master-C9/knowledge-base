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



This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

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

