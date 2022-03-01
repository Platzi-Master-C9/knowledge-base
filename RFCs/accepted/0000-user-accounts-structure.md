- Start Date: 2020-02-24
- Members: Pedro Herrera @Herdro
- RFC PR: (leave this empty)

# Summary

Segregate responsibilities (SRP) to generate clean architecture, in addition, the API endpoints will be defined for user accounts. 

<!-- Brief explanation of the feature. -->

# Basic example

Separating business logic as services, adapters and framworks and database as follows:

<a href="https://ibb.co/bKwbcBM"><img src="https://i.ibb.co/qrqJTs3/structure-sketch-v1.jpg" alt="structure-sketch-v1" border="0"></a>


- `/user/` **POST** - create user
- `/user/{user_id}` **GET** - user info
- `/user/{user_id}` **PATCH** - update user info
- `/user/{user_id}` **DELETE** - dalete user
- `/user/{user_id}/bookmark/` **POST** - Create list favorite places
- `/user/{user_id}/bookmarks/` **GET** - list user favorite places
- `/user/{user_id}/bookmark/{bookmark_id}` **GET** - favorite places details
- `/user/{user_id}/bookmark/{bookmark_id}` **PATCH** - update favorite places
- `/user/{user_id}/bookmark/{bookmark_id}` **DELETE** - Delete list favorite places



<!-- If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable. -->

# Motivation

Create the basis of the service structure for the different cases where user information is required, maintaining an organized response to the requirements for adequate scalability and maintenance in the future. 

<!-- Why are we doing this? What use cases does it support? What is the expected
outcome?

Please focus on explaining the motivation so that if this RFC is not accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind. -->

# Detailed design

My proposal for this project is to work with the following dependencies:
- sequelizer (ORM)
- joi (data schema validate)
- @hapi/boom (error handler)

separating each folder for each job to be done for example:
```
main
├── db
├── routes
│   ├── userRoute.js
├── schemas
│   ├── userSchema.js
├── services
│   ├── userService.js
```

and incorporate use cases and new functions in each of the folders.

## **Endpoints**
### **Users**
#### **Create User**

- URL: `/user/`
- Method: `POST`
- Auth required: NO
- Use: Create new user
- Json structure:
```json
{
    "email": "varchar(200) NOT NULL UNIQUE",
    "firstName": "varchar(50) NOT NULL",
    "secondName": "varchar(50)",
    "firstSurname": "varchar(50) NOT NULL",
    "seconsName": "varchar(50)",
    "birthDate": "date NOT NULL", //verification of legal age
    "gender": "enum('male', 'famele', 'not difined') NOT NULL",
    "phoneNumber": "varchar() NOT NULL" //alternative to separate the number with the area code in ("phoneNumberArea" enum(+56, +59, ...)) ("phoneNumber" integer)
}
```

*Sucess Response*

- Code: `201 CREATE`
- Example:

```json
{
    "id": "1",
    "firstName": "Juanito",
    "secondName": "",
    "firstSurname": "Perez",
    "secondSurname": "",
    "email": "j.perez@email.com",
}
```
*Error Response*

- Code: `422 UNPROCESSABLE ENTITY`
- Conditions:
    - `email`: "field is longer than 200 characters"
    - `email`: "field is null"
    - `email`: "email already used"
    - `firstName`: "field is loger than 50 characters"
    - `firstName`: "fiel is null"
    - `secondName`: "field is loger than 50 characters"
    - `firstSurname`: "field is loger than 50 characters"
    - `firstSurname`: "fiel is null"
    - `secondSurname`: "field is loger than 50 characters"
    - `birthDate`: "field is not a date format"
    - `birthDate`: "field is null"
    - `gender`: "field is not a ('male', 'famele', 'not difined') options",
    - `gender`: "field is null"
    - `phoneNumber`: "field is null"

#### **View User**

- URL: `/user/{user_id}`
- Method: `GET`
- Params:
    - `email`
    - `phone`
    - `addres`
    - `identification`
    - `passport`
    - `favorite`
- Auth required: YES
- Use: view the user information

*Sucess Response*

- Code: `200 OK`
- Example:
```json
{
    "id": "1",
    "firstName": "",
    "secondName": "",
    "firstSurname": "",
    "secondSurname": "",
    "gender": "",
    "email": "123@email.com",
    "avatar": "url(image)",
    "phoneNumber": "",
    "addres":{
        "country":"",
        "citie":"",
        "addres":"",
    },
    "identification": {
        "nationality": "",
        "idOfNationality":""
    },
    "passport":"",
    "favorites": {
        "idFavorite1": "1",
        "idFavorite2": "2",
        "idFavorite3": "3",
        ...
    }

}
```
*Error Response*

- Code: `401 UNAUTHORIZED`
- Conditions: Invalid token.
- Example:
```json
{
  "detail": "Invalid Token."
}
```

- Code: `404 NOT FOUND`
- Conditions: If the provided ID doesn't exist on the database.
- Example:
```json
{
  "detail": "User not found."
}
```

#### **Update User**

- URL: `/user/{user_id}`
- Method: `PATCH`
- Auth required: YES
- Use: Update the user information
- Json structure:
```json
{
    "email": "varchar(200) NOT NULL UNIQUE",
    "firstName": "varchar(50) NOT NULL",
    "secondName": "varchar(50)",
    "firstSurname": "varchar(50) NOT NULL",
    "seconsName": "varchar(50)",
    "gender": "enum('male', 'famele', 'not difined') NOT NULL",
    "phoneNumber": "varchar() NOT NULL",
    "avatar": "url(image)",
    "phoneNumber": "varchar(20)",
    "addres":{
        "country":"varchar(50)",
        "citie":"varchar(50)",
        "addres":"varchar(200)",
    },
    "identification": {
        "nationality": "varchar(50)",
        "idOfNationality":"varchar(50)"
    },
    "passport":"varchar(50)",
}
```


*Sucess Response*

- Code: `200 OK`
- Example:

```json

```
*Error Response*

- Code: `401 UNAUTHORIZED`
- Conditions: Invalid token.
- Example:
```json
{
  "detail": "Invalid Token."
}
```

- Code: `400`
- Example:

```json

```
#### **Delete User**

- URL: `/user/{user_id}`
- Method: `DELETE`
- Auth required: YES
- Use: Delete user

*Sucess Response*

- Code: `200 OK`
- Example:

```json
{
    "user has been deleted"
}
```
*Error Response*

- Code: `401 UNAUTHORIZED`
- Conditions: Invalid token.
- Example:
```json
{
  "detail": "Invalid Token."
}
```

- Code: `400`
- Example:

```json

```

### **User favorites**
#### **Create list favorite**
#### **View list favorite**
#### **Update list favorite**
#### **Delete list favorite**
#### **Add place a list favorite**
#### **Remove place a list favorite**



<!-- This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here. -->

# Drawbacks

to be determined.

<!-- Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here. -->

# Alternatives

<!-- - GraphQL APIs.
- Falcor APIs.
- gRPC APIs.
- JSON-Pure APIs.
- oData APIs. -->

<!-- What other designs have been considered? What is the impact of not doing this? -->

# Adoption strategy

To maintain the structure, the rule must be maintained that each responsibility must be in a single file and must only call the layers that have communication. for example, a service cannot make a direct query to the database, it must ask the ORM to manage it.

<!-- If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries? -->

# How we teach this 

I request information on how to implement a software structure, because I do not know the methods to do it.

<!-- What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing C9 projects patterns?

Would the acceptance of this proposal mean the C9 documentation must be
re-organized or altered? Does it change how C9 is taught to new developers
at any level?

How should this feature be taught to existing C9 developers? -->

# Unresolved questions

What fremworks will be used for the project, what database will be used and how will testing be performed?

<!-- Optional, but suggested for first drafts. What parts of the design are still
TBD? -->
