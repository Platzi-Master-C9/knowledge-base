- Start Date: 2022-02-23
- Members: Alejandro Pérez Olvera @AlejandroPOcz
- RFC PR: 

# **Summary**

We need to define and implement the API endpoints for the places application in the booking project [C9]. In order to define that, we suggest the endpoints in the *Basic example* section of this document.

# **Basic example**

- `/places/` **GET** - list of all places
- `/places/` **POST** - create a place
- `/places/{place_id}/` **GET** - get place
- `/places/{place_id}/` **PATCH** - update place
- `/places/{place_id}/` **DELETE** - delete place

# **Motivation**

We are building the main structure of the places app behavior. In order to acomplish this in the best way, we need to plan the nearest possible the real use of the application. Better to overplan than overfix.

# **Detailed design**

The REST standard is suggested for these contracts, due to the Resources efficiency, the simplicity and the better scalability that we find in this method. REST is a set of architectural constraints, not a protocol or a standard. API developers can implement REST in a variety of ways.

When a client request is made via a RESTful API, it transfers a representation of the state of the resource to the requester or endpoint. This information, or representation, is delivered in one of several formats via HTTP: JSON (Javascript Object Notation), HTML, XLT, Python, PHP, or plain text. JSON is the most generally popular file format to use because, despite its name, it’s language-agnostic, as well as readable by both humans and machines. 

Something else to keep in mind: Headers and parameters are also important in the HTTP methods of a RESTful API HTTP request, as they contain important identifier information as to the request's metadata, authorization, uniform resource identifier (URI), caching, cookies, and more. There are request headers and response headers, each with their own HTTP connection information and status codes.

## **Read All**

- URL: `/places/`
- Method: `GET`
- Auth required: NO
- Use: get all the registered places.


### Success Response

- Code: `200 OK`
- Content example:

```json
{
  {"id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "name": "Yellow House",
  "description": "Beautiful house near to the beach and 3 blocks away of the center of the town",
  "price": 4000,
  "currency": "USD",
  "is_active": True,
  "rating": 4.8,
  "host_id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "rooms": 4,
  "bathrooms": 3,
  "pets": True,
  "smoke": True,
  "free_cancelation": False,
  },
  ...
}
```


***
## **Read**

- URL: `/places/{place_id}`
- Method: `GET`
- Auth required: NO
- Use: get a singular registered place.


### Success Response

- Code: `200 OK`
- Content example:

```json
{
  "id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "name": "Yellow House",
  "description": "Beautiful house near to the beach and 3 blocks away of the center of the town",
  "price": 4000,
  "currency": "USD",
  "is_active": True,
  "rating": 4.8,
  "host_id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "rooms": 4,
  "bathrooms": 3,
  "pets": True,
  "smoke": True,
  "free_cancelation": False,
}
```

### Error Response

- Code: `404 NOT FOUND`
- Condition: If the provided ID doesn't exist on the database.
- Content example:

```json
{
  "detail": "Place not found."
}
```
***
## **Update**

- URL: `/places/{place_id}`
- Method: `PATCH`
- Auth required: YES
- Use: update a specific place.

### Data constraints

```json
{
  "name": "[Place name (Max 50 characters)]",
  "description": "[Place brief description (Max 100 characters)]",
  "price":"[Price(Not Negative Numbers)]",
  "currency":"Currency (Choose a valid currency)",
  "is_active": "[Check avaliabilty (No Null)]",
  "rating":"[Decimal no negative (No more than 5)]",
  "host_id": "[User ID (Valid and existing ID)]",
  "rooms": "[Number or rooms (No Null)]",
  "bathrooms": "[Number of bathrooms (No Null)]",
  "pets": "[Boolean of pets allowed (No Null)]",
  "smoke": "[Boolean of smoke allowed (No Null)]",
  "free_cancelation": "[Boolean of free cancelation (No Null)]",
}  
```
### Data example

```json
{
  "id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "name": "Yellow House",
  "description": "Beautiful house near to the beach and 3 blocks away of the center of the town",
  "price": 4000,
  "currency": "USD",
  "is_active": True,
  "rating": 4.8,
  "host_id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "rooms": 4,
  "bathrooms": 3,
  "pets": True,
  "smoke": True,
  "free_cancelation": False,
}
```
### Success Response

- Code: `200 OK`
- Content example:

```json
{
    "id": "13918333-0a7a-4835-ab76-6685127d7d3b",
    "name": "Yellow House2",
    "description": "Beautiful house near to the beach and 3 blocks away of the center of the town.",
    "rooms": 4,
    "bathrooms": 3,
    "pets": True,
    "smoke": True,
    "free_cancelation": False,
}
```
### Error Response

- Code: `401 UNAUTHORIZED`
- Conditions: Invalid token.
- Content example:

```json
{
  "detail": "Invalid Token."
}
```
- Code: `404 NOT FOUND`
- Conditions: If the provided ID doesn't exist on the database.
- Content example:

```json
{
  "detail": "Place not found."
}
```
- Code: `422 UNPROCESSABLE ENTITY`
- Conditions:
  * `name` field has more than 50 characters.
  * `name` field is null.
  * `description` field has more than 100 characters.
  * `description` field is null.
  * `rooms` field is null.
  * `bathrooms` field is null.
  * `pets` field is null.
  * `smoke` field is null.
  * `free_cancelation` field is null.
- Content example:

```json
{
  "detail": [
    {
      "loc": ["body", "name"],
      "msg": "field limited to 50 characters",
      "type": "value_error"
    },
    {
      "loc": ["body", "name"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "description"],
      "msg": "field limited to 100 characters",
      "type": "value_error"
    },
    {
      "loc": ["body", "description"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "rooms"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "bathrooms"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "pet"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "smoke"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "free_cancelation"],
      "msg": "field with no data",
      "type": "null_error"
    }
  ]
}
```
***
## **Create**

- URL: `/places/`
- Method: `POST`
- Auth required: YES
- Use: register a place.

### Data constraints

```json
{
  "name": "[Place name (Max 50 characters)]",
  "description": "[Place brief description (Max 100 characters)]",
  "price":"[Price(Not Negative Numbers)]",
  "currency":"Currency (Choose a valid currency)",
  "is_active": "[Check avaliabilty (No Null)]",
  "rating":"[Decimal no negative (No more than 5)]",
  "host_id": "[User ID (Valid and existing ID)]",
  "rooms": "[Number or rooms (No Null)]",
  "bathrooms": "[Number of bathrooms (No Null)]",
  "pets": "[Boolean of pets allowed (No Null)]",
  "smoke": "[Boolean of smoke allowed (No Null)]",
  "free_cancelation": "[Boolean of free cancelation (No Null)]",
}  
  
```
### Data example

```json
{
  "id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "name": "Yellow House",
  "description": "Beautiful house near to the beach and 3 blocks away of the center of the town",
  "price": 4000,
  "currency": "USD",
  "is_active": True,
  "rating": 4.8,
  "host_id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "rooms": 4,
  "bathrooms": 3,
  "pets": True,
  "smoke": True,
  "free_cancelation": False,
}
```
### Success Response

- Code: `201 CREATE`
- Content example:

```json
{
  "name": "Yellow House",
  "description": "Beautiful house near to the beach and 3 blocks away of the center of the town",
  "price": 4000,
  "currency": "USD",
  "is_active": True,
  "rating": 4.8,
  "host_id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "rooms": 4,
  "bathrooms": 3,
  "pets": True,
  "smoke": True,
  "free_cancelation": False,
}
```
### Error Response
- Code: `401 UNAUTHORIZED`
- Condition: Invalid token.
- Content example:

```json
{
  "detail": "Invalid Token."
}
```
- Code: `422 UNPROCESSABLE ENTITY`
- Conditions:
  * `name` field has more than 50 characters.
  * `name` field is null.
  * `description` field has more than 100 characters.
  * `description` field is null.
  * `rooms` field is null.
  * `bathrooms` field is null.
  * `pets` field is null.
  * `smoke` field is null.
  * `free_cancelation` field is null.
- Content example:

```json
{
  "detail": [
    {
      "loc": ["body", "name"],
      "msg": "field limited to 50 characters",
      "type": "value_error"
    },
    {
      "loc": ["body", "name"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "description"],
      "msg": "field limited to 100 characters",
      "type": "value_error"
    },
    {
      "loc": ["body", "description"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "rooms"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "bathrooms"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "pet"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "smoke"],
      "msg": "field with no data",
      "type": "null_error"
    },
    {
      "loc": ["body", "free_cancelation"],
      "msg": "field with no data",
      "type": "null_error"
    }
  ]
}
```
***

## **Delete**

- URL: `/places/{place_id}`
- Method: `DELETE`
- Auth required: YES
- Use: soft delete a registered place.


### Success Response

- Code: `200 OK`
- Content example:

```json
{
  "id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "name": "Yellow House",
  "description": "Beautiful house near to the beach and 3 blocks away of the center of the town",
  "price": 4000,
  "currency": "USD",
  "is_active": True,
  "rating": 4.8,
  "host_id": "13918333-0a7a-4835-ab76-6685127d7d3b",
  "rooms": 4,
  "bathrooms": 3,
  "pets": True,
  "smoke": True,
  "free_cancelation": False,
}
```
### Error Response

- Code: `401 UNAUTHORIZED`
- Conditions: Invalid token.
- Content example:

```json
{
  "detail": "Invalid Token."
}
```
- Code: `404 NOT FOUND`
- Condition: If the provided ID doesn't exist on the database.
- Content example:

```json
{
  "detail": "Place not found."
}
```

# Drawbacks

It's still missing information about users database and how it interacts with places. Also, is missing a review contemplation.

# Alternatives

Pendant

# Adoption strategy

Pendant

# How we teach this

Pendant

# Unresolved questions

What about users and reviews tables/interactions?
