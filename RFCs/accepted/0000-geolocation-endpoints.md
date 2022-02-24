# API contracts (endpoints, endpoint types, etc.) [RFC]

- Start Date: 2022-02-20
- Members: @cetherdev[C09], @Edilberto Vazquez Luna [C9]
- RFC PR: (leave this empty)

# **Summary**

Endpoints design for the communucation bettween places service team and front-end geolocation team.

# **Basic example**

1. When a place is created, places service notify to API-geolocation that a place has been created and geolocation service store the coordinates in database.
2. When a user makes a request for a place, the API-geolocation returns places availables in the area with their costs.
3. When a user focused in a specific stay, the API-geolocation returns the approximate location of that palce.

# **Motivation**

Why are we doing this?

The front-end team needs to know the places that users select for show them in the map. REST API is an efficient way to comunicate with front-end, databases and other services in the application. Currently there is no project or application that does not have a REST API for the creation of professional services.

What use cases does it support? 

- Store the coordinates of places
- Provide stays in an especific area
- Return the coordinates of an especific accomodation

What is the expected outcome?

Provide methods that are available to the geolocation front-end team and places team that allows comunicate with geolocation service and have high availability with requests and responses.

# **Detailed design**

```jsx
// Endpoints from geolocation service to places service

// This edpoint allows to places service communicate and send data for store the geolocation
Endpoint
/geolocation/notify-place
Type: POST
// The parameters required are placeId and placeName, address
// address allows geocoding
Parameters: { placeId, placeName, address }
Response: {status: 200, response: placeId}
// Body example
/*
	{
		"placeId": "sdh398lsdjkfs",
		"placeName": "New loft Parque",
    "address": "1600 Amphitheatre Parkway, Mountain View, CA"
	}
*/

// This enpoint allow to places service update the place stored in database
Endpoint
/geolocation/update-place
Type: PUT
// placeId allows a more efficient search in the database
Parameters: {placeId, placeName, address}
Response: {status: 200, response: placeId}
// Body example
/*
	{
		"placeId": "sdh398lsdjkfs",
		"placeName": "Parque las marias",
    "address": "1700 Parkway, Mountain View, CO"
	}
*/
```

```jsx
// Endpoint when user make a reaquest
Endpoint
/geolocation/get-places
Requests
Req: GET
Type: Query
// This parameters espcify the quadrant for search places that the user request.
// The parameters required in the query are north_lat, south_lat, west_lng, east_lng
QueryParams: {north_lat,south_lat,west_lng,east_lng}
Response: {status: 200, places: [{placeId,lat,lng},{placeId,lat,lng},{placeId,lat,lng}]}
// Query example
// /geolocation/get-places?north_lat=19.51&south_lat=19.29
//												&west_lng=-98.97&east_lng=-99.32
```

```jsx
// This Endpoint return a specific place with its Id, latitude and longitude
Endpoint
/geolocation/get-location
Req: GET
Type: Query
// For make a request needs the placeId 
QueryParams: {placeId}
response: {status: 200, place: {placeId,lat,lng}}
// Query example
// /geolocation/get-location?placeId="idufhyg8723"
```

# **Drawbacks**

Why should we *not* do this? Please consider:

- If we change the name of any endpoint the other teams must make changes to their code.
- If front-end does not need all data that the endpoint returns, front-end needs consume all data or we need to change the query to return that specific data.

# **Alternatives**

GraphQL: This allow expose methods without endpoint and front-end can consume the data that they require.

Fastify: This framework provides full encapsulation for plug-ins, automatically parses JSON with relatively faster rendering, and provides quick routing. Among other benefits, Fastify also has a cleaner syntax for writing async code in controllers.

# **Adoption strategy**

We need to write the documentation on how to use the REST API and we need to coordinate with other teams, like front-end about the data they need and places service about the information they will send us for store in database

# **How we teach this**

1. Include A README file that contains
    - A brief description of the project
    - Installation instructions
    - A short example/tutorial
2. Allow issue tracker for others
3. Write an API documentation
    - What a function do
    - What the function's parameters or arguments are
    - What a function returns
4. Document the code
5. Apply coding conventions, such as file organization, comments, naming conventions, programming practices, etc.
6. Include information for contributors
7. Include citation information
8. Include licensing information
9. Link to our e-mail address at the end
10. List all the version of the files along with the major edits we did in each version

# **Unresolved questions**

What does each endpoint return and how?.

How many requests does the the API make?.

How does the REST API communicate with places service?.

Will the places service team send data to us in real time?.