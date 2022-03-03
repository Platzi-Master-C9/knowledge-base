# API contracts (endpoints, endpoint types, etc.) [RFC]

- Start Date: 2022-02-20
- Members: @cetherdev[C09], @Edilberto Vazquez Luna [C9]
- RFC PR: (leave this empty)

# **Summary**

Endpoints design for the communucation bettween places service team and front-end geolocation team.

# **Basic example**

Some examples how to use this enpoints

### “/geolocation/place” (POST)

When a place is created, places service notify to API-geolocation that a place has been created and geolocation service store the coordinates in database.

### Example

This example assume that the places service team is using JavaScript for backend

```jsx
// Endpoint URL
const URL = "http://booking/api/v1/geolocation/place";
// Data to send
let place = {
  placeId: "df564gdf65g4d",
  placeName: "New york, central park",
  placeAddress: "1600 Amphitheatre Parkway, Mountain View, CA",
  lat: "41.5646546",
  lon: "47.1654646",
};
// Define the configuration for post method
const settings = {
  method: "POST",
  mode: "cors",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data), // pass data that will be send
};
// Function that calls enpoint place with the post method
async function getPlaces(url, settings) {
  try {
    const response = await fetch(url, settings);
    return response;
  } catch (error) {
    return error;
  }
}
// Call function
const response = getPlaces(URL, settings);

console.log(response); // response contains the status code and message
```

### “/geolocation/places” (GET)

When a user makes a request for a place, the API-geolocation returns places availables in the area with their costs. This enpoint will be used for front-end team and it is assumed that the team is using NextJS, this example uses useEffect and useState.

The reson we need latitude and longitude is because we made a Query with `2dsphere` Index in MongoDB or with a relation database, for a example see [https://docs.mongodb.com/manual/tutorial/query-a-2dsphere-inde](https://docs.mongodb.com/manual/tutorial/query-a-2dsphere-index/)

### Example

```jsx
const App = () => {
  const URL = "http://booking/api/v1/geolocation/places";
// places are given an array and that is why the the state start with an empty array
  const [places, setPlaces] = useState([]);
	const [lat, setLat] = useState("");
	const [lon, setLon] = useState("")

  useEffect(() => {
    fetch(`${URL}?lat=${lat}&lon${lon}`)
      .then((res) => res.json())
// Set places with the response data
      .then((res) => {
        setPlaces(res.places);
      })
      .catch((error) => {
        console.log("Cannot set places", error.message);
      });
  }, [setPlaces]);

  return (
      ...
  );
};
```

### “/geolocation/location” (GET)

When a user focused in a specific stay, the API-geolocation returns the approximate location of that palce. The same form that Endpoint “/geolocation/places” (GET), it is assumed that the team is using NextJS

```jsx
const App = () => {
  const URL = "http://booking/api/v1/geolocation/location";
// place is given an object and that is why the state start with a empty object
  const [location, setLocation] = useState({});
	const [placeId, setPlaceId] = useState("")

  useEffect(() => {
    fetch(`${URL}?placeId=${placeId}`)
      .then((res) => res.json())
// Set location with the response data
      .then((res) => {
        setPlace(res.location);
      })
      .catch((error) => {
        console.log("Cannot set places", error.message);
      });
  }, [setPlace]);

  return (
      ...
  );
};
```

# **Motivation**

Why are we doing this?

The front-end team needs to know the places that users select for show them in the map. REST API is an efficient way to comunicate with front-end, databases and other services in the application. Currently there is no project or application that does not have a REST API for the creation of professional services.

### What is REST API?

API REST, is an application program interface (API or Web API), which fits within the limits of the REST architecture (representational state transfer). When the client sends a request through the REST API, it passes a representation of the state of the requested resource to the requester. The information is given through HTTP. Headers and and parameters are importants as they contain important information like cookies, authorization, cache, etc. There are headers for request and response, and eche one has its codes to indetify it.

What use cases does it support?

- Store the coordinates of places
- Provide accomodations in a specific area
- Return the coordinates of an especific accomodation
- Return the address of a specific latitude and longitude

What is the expected outcome?

Provide methods that are available to the geolocation front-end team and places team that allows comunicate with geolocation service and have high availability with requests and responses.

# **Detailed design**

### How we think the flow should be when creating a place

![Untitled](https://i.pinimg.com/originals/a3/eb/22/a3eb22a46a2365248660fad6b642920b.jpg)

The design of the endpoints is detailed below for each specific case that we belive needs to be supported

## (POST) /geolocation/place

Endpoint for the places service to notify that a new place has been created

### Parameters

### place

**Description:** Place object that needs to be added to the DB

**(body)**: place **(Object,** **\*Required)**

- **Model**
  ```json
  CreatePlace{
  	placeId*	string // required
  		maxLength: 20
  		minLength: 10
  		example: "4f7w4d4s43"
  	placeName*	string // required
  		maxLength: 15
  		minLength: 8
  		example: "New loft Parque"
  	placeAddress*	string // required
  		maxLength: 50
  		minLength: 10
  		example: "1600 Amphitheatre Parkway, Mountain View, CA"
  	lat*	number($float64)
  		example: 45.16546
  	lon*	number($float64)
  		example: 47.16546
  }
  ```

**Parameter content type:** application/json

### **Example Value**

```json
{
  "placeId": "4f7w4d4s431",
  "placeName": "New loft Parque",
  "placeAddress": "1600 Amphitheatre Parkway, Mountain View, CA",
  "lat": 45.16546,
  "lon": 47.16546
}
```

### Responses

**Responses content type:** application/json

### **Code:** 200

### E**xample value**

```json
{
  "placeId": "4f7w4d4s43",
  "message": "successful operation"
}
```

### **Code:** 405

### E**xample value**

```json
{
  "message": "Invalid input"
}
```

## (PATCH) /geolocation/place

Endpoint for the places service that allow upte a specific place, we only allow modify place name for our business rules. If we change direction we assume that it is another place, if it is another place the lat and lon is different in that case is better to create a new place.

### Parameters

### place

**Description:** Place object that needs to be updated to the DB

**(body)**: place **(Object,** **\*Required)**

- **Model**
  ```json
  UpdatePlace{
  	placeId*	string // required with id we search in data base
  		maxLength: 20
  		minLength: 10
  		example: "4f7w4d4s43"
  	placeName*	string // required
  		maxLength: 15
  		minLength: 8
  		example: "New loft Parque"
  }
  ```

**Parameter content type:** application/json

### **Example Value**

```json
{
  "placeId": "4f7w4d4s431",
  "placeName": "New loft Parque"
}
```

### Responses

**Responses content type:** application/json

### **Code:** 200

### E**xample value**

```json
{
  "placeId": "4f7w4d4s43",
  "message": "successful operation"
}
```

### **Code:** 400

### E**xample value**

```json
{
  "message": "Invalid ID supplied"
}
```

### **Code:** 404

### E**xample value**

```json
{
  "message": "Place not found"
}
```

### **Code:** 405

### E**xample value**

```json
{
  "message": "Validation exception"
}
```

## (DELETE) /geolocation/place

Remove a specific place from database

### Parameters

### **placeId**

**Description:** Id required for search and delete in DB

**(query)**: placeId **(String,** **\*Required)**

**constraints:** maxLength[20], minLength[10]

### **Example Value**

```json
(query) /geolocation/place?placeId="asd78wadad2"
```

### Responses

**Responses content type:** application/json

### **Code:** 200

### E**xample value**

```json
{
  "placeId": "asd78wadad2",
  "message": "place deleted from geolocation data base"
}
```

### **Code:** 400

### E**xample value**

```json
{
  "message": "Invalid ID supplied"
}
```

### **Code:** 404

### E**xample value**

```json
{
  "message": "Location id not found"
}
```

### **Code:** 405

### E**xample value**

```json
{
  "message": "Validation exception"
}
```

## (GET) /geolocation/places

Return multiple places with their latitude and longitude

### Parameters

The reson we need latitude and longitude is because we made a Query with `2dsphere` Index in MongoDB or with a relation database, for a example see [https://docs.mongodb.com/manual/tutorial/query-a-2dsphere-inde](https://docs.mongodb.com/manual/tutorial/query-a-2dsphere-index/)

### lat

**Description: (lat)** Latitude for make a Point within a Circle Defined on a Sphere with mongo DB

**(query)**: lat **(Number,** **\*Required)**

**constrainst:** number($float64)

### lon

**Description:** **(lon)** Longitude for make a Point within a Circle Defined on a Sphere with mongo DB

**(query)**: lon **(Number,** **\*Required)**

**constrainst:** number($float64)

### **Example Value**

```json
(query) /geolocation/places?lat=45.16546&lon=46.14786
```

### Responses

**Responses content type:** application/json

### **Code:** 200

### E**xample value**

```json
{
  "places": [
    {
      placeId: "4f7df24s43",
      placeName: "New loft Parque 1",
      lat: 45.12346,
      lon: 47.35332,
    },
    {
      placeId: "09d8fwdf2",
      placeName: "New loft Parque 2",
      lat: 31.89201,
      lon: 32.16765,
    },
    {
      placeId: "98asd791d",
      placeName: "New loft Parque 3",
      lat: 11.54765,
      lon: 12.56736,
    },
  ];
}
```

### **Model**

```json
GetPlaces{
	placeId*	string // required
		maxLength: 20
		minLength: 10
		example: "4f7w4d4s43"
	placeName*	string // required
		maxLength: 15
		minLength: 8
		example: "New loft Parque"
	lat*	number($float64) // required
		example: 45.16546
	lon*	number($float64) // required
		example: 47.16546
}
```

### **Code:** 400

### E**xample value**

```json
{
  "message": "Invalid lat and lon values"
}
```

### **Code:** 405

### E**xample value**

```json
{
  "message": "Validation exception"
}
```

## (GET) /geolocation/location

Return a specific location with their latitude and longitude

### Parameters

### **placeId**

**Description:** Id required for search in DB

**(query)**: placeId **(String,** **\*Required)**

**constraints:** maxLength[20], minLength[10]

### **Example Value**

```json
(query) /geolocation/location?placeId="asd78wadad2"
```

### Responses

**Responses content type:** application/json

### **Code:** 200

### E**xample value**

```json
{
  "location": {
    "placeId": "4f7w4d4s43",
    "placeName": "New loft Parque",
    "placeAddress": "1600 Amphitheatre Parkway, Mountain View, CA",
    "lat": 45.16546,
    "lon": 47.16546
  }
}
```

### **Model**

```json
GetLocation{
	placeId*	string
		maxLength: 20
		minLength: 10
		example: 4f7w4d4s43
	placeName*	string
		maxLength: 15
		minLength: 8
		example: New loft Parque
	placeAddress*	string
		maxLength: 50
		minLength: 10
		example: 1600 Amphitheatre Parkway, Mountain View, CA
	lat*	number($float64)
		example: 45.16546
	lon*	number($float64)
		example: 47.16546
}
```

### **Code:** 400

### E**xample value**

```json
{
  "message": "Invalid ID supplied"
}
```

### **Code:** 404

### E**xample value**

```json
{
  "message": "Location not found"
}
```

### **Code:** 405

### E**xample value**

```json
{
  "message": "Validation exception"
}
```

## (GET) /geolocation/address

Get a specific address with the provided coordinates (latitude and longitude). The backend using reverse geocoding for provide the address and place name.

### Parameters

### lat

**Description: (lat)** Latitude to do reverse geocoding

**(query)**: lat **(Number,** **\*Required)**

**constrainst:** number($float64)

### lon

**Description:** **(lon)** Longitude to do reverse geocoding

**(query)**: lon **(Number,** **\*Required)**

**constrainst:** number($float64)

### **Example Value**

```json
(query) /geolocation/address?lat=45.16546&lon=46.14786
```

### Responses

**Responses content type:** application/json

### **Code:** 200

### E**xample value**

```json
{
  "address": {
    "placeName": "New loft Parque",
    "placeAddress": "1600 Amphitheatre Parkway, Mountain View, CA"
  }
}
```

### **Model**

```json
GetAddress{
	placeName*	string
		maxLength: 15
		minLength: 8
		example: "New loft Parque"
	placeAddress*	string
		maxLength: 50
		minLength: 10
		example: "1600 Amphitheatre Parkway, Mountain View, CA"
}
```

### **Code:** 400

### E**xample value**

```json
{
  "message": "Invalid lat and lon values"
}
```

### **Code:** 405

### E**xample value**

```json
{
  "message": "Validation exception"
}
```

# **Drawbacks**

Why should we *not* do this? Please consider:

- If we change the name of any endpoint the other teams must make changes to their code.
- If front-end does not need all data that the endpoint returns, front-end needs consume all data or we need to change the query to return that specific data.

# **Alternatives**

GraphQL: This allow expose methods without endpoint and front-end can consume the data that they require.

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
11. A documentation fo the API in POSTMAN

# **Unresolved questions**

What does each endpoint return and how?.

How many requests does the the API make?.

How does the REST API communicate with places service?.

Will the places service team send data to us in real time?.

In reverse geocoding, we provide the latitude and longitude or we will receive the latitude and longitude in the parameters?. For example `/geolocation/address?lat=45.15646&lon=47.15446`

Reverse geocoding will be used for our team or places service team for store in database?

Where is this Data saved (name, address)? in places service or geolocation service?
