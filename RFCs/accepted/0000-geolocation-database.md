- Start Date: 1/03/2022
- Members: Emanuel Alvarado, Dilan Ariza
- RFC PR: (leave this empty)
​
# Summary
​
Database selection and data schema design for geolocation data storage in the geolocation squad.
​
# Basic example
​
If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.
​
# Motivation
​
## Why are we doing this?
- Due to the geolocation requirements we need to define a database and a data schema to storage the data required to comply with the requirements and integrate the domain with the main project.
​
## What use cases does it support?
The main use cases are related to the place geolocation data so that it can be:
- Storaged
- Read
- Updated
- Modified
​
## What is the expected outcome?
- Accesible and clean data
- Simple consultation geospatial queries such as:
    - Near places beneath a point
    - Places located beneath a defined distance
    - Filter places by type
​
​
# Detailed design
Due to the geolocation requirements we propose the usage of MongoDB as the main database for the geolocation squad. 
​
## Why MongoDB?
MongoDB, compared to other database alternatives, has built-in features that facilitate the implementation and usage of geolocation data such as Geospatial Queries. This feature is helpful whenever we have to find near places beneath a point or a defined distance in comparison to other databases where we don’t have those features and an alternative process will be required to make those “complex queries”.
​
## Data Schema
​
```json
{
  Place_id: ObjectId,
  Price: “530”,
  Location: {
    Type: “Place”,
	 coordinates: [-192792, 129200]
  },
  Country: “Mexico”,
  State: “CDMX”,
  City: “Azcapotzalco”,
  Postal_code: “02090”,
  Full_Address: “Street Name #98”,
}
​
```
​
- The place_id has to be the same one that the places database has in order to make it easier to make requests to the database.    
- We propose saving the price and full adress tag to avoid making more requests and to have all the required data in our database.
- Instead of having the geográficas data such as country, state, city and postal code normalized we propose having all of them together to make it easier to perform queries.
​
# Drawbacks
​
- We don’t know exactly the expertise the team has using MongoDB
- Impact on teaching people how to use MongoDB in case the team has no experience 
​
# Alternatives
​
- In tearm of database implementation one of our alternatives is using a relational database such as MySQL or PostgreSQL. Even tough is important to take into consideration the drawbacks of not having the geospatial queries feature. 
​
- Taking about the proposed data schema, we  
​
# Adoption strategy
​
- As this will be the first database implementation for the squad, adoption will not affect any prior squads or projects and should be easy to implement. 
​
# How we teach this
​
C9 developers can rely on:
- MongoDB documentation for geospatial queries and general MongoDB usage. 
- Platzi’s MongoDB Course
- Online resources such as forums or tutorials.
​
In case the proposal is accepted C9 documentation shouldn’t me re-organized due to the fact that it’s the first time implementing it. 
​
# Unresolved questions
- 