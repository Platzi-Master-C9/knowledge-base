- Start Date: 2022-02-24
- **Members**: Pedro Silva, Andrés Correa, Felipe Rodriguez, Mario Fuentes
- RFC PR:

# Summary

This RFC describes the data, its schema and type, for users, admins (and Superadmins), places and globalbooking list. It will be necessary in order to clarify which entities frondend can consume and what the formay of data is going to be. Our team will use databases created by Booking system, Users and Places but we will manage or own enpoints in order to format and simplify the work of the frontend (mejorar la redacción cuando no esté dormido)


# Motivation

Correctly defining the type of information that is going to be needed is the basis for being able to build any software solution. Once these parameters are clear, it is possible to start planning the type of architecture or the tools that are going to be used in the project.

# Detailed design

## Admin profiles

There will be 2 administrator profiles (admin and SuperAdmins). This allows to give the system more flexiblity. The description of this profiles are:

##### Admin:
* Can manage users, It means validate, edit, delete and ban (each one of this terms are explaned in the Glosary seccion)
* Has access to the user table, places and global bookings table
* Can use all the filters avalible in the Filter seccion except the ones in the admin table

##### SuperAdmin:
* Can perform all the previous actions
* Can create Admins and SuperAdmins (through invitation or changing the user profile of a regular user)
* Can delete Admins and SuperAdmins (Except its own profile)
* Can Edit Admins and SuperAdmins
* Can see the admin table

> The name of the Admin profile in the database will be `admin` and the name of the profile SuperAdmin will be `super_admin`

### Way to create Admins and SuperAdmin profiles
super admin can create admin through a modal view with the fields:
* first name (required)
* second name
* first surname (required)
* second surname
* email (required)
* phone number (required)
* profile (`admin` or `super_admin`)

### Data for Admin Profiles
* id (is necesary to perform actions like edit admin, is not visible in the interface)
* full_name (first_name + fist_surname)
* url_image
* profile

## User Profile
represent an authenticated user

### Verify Accounts
Once an admin call the endpoint to validate a user, from the backend, we will update user information an then, we will comunicate with notification team in order to send the message to user 

### Data for User Profile

* id (is necesary to perform actions like validate user, is not visible in the interface)
* full_name (first_name + fist_surname)
* url_image
* date_of_register
* status (verified, active, deleted or banned)

## Places
represent the places created by users (read only,)

### data for Places
* name
* status
* host name

## global booking
represent a list of all bookings (read only)

### data for Bookings
* date of book
* place
* user name
* status
* from date
* end date

_____________________________
## End points
thi seccion details the required end points for the admin panel

###url
the recommended url for all services is `admin_panel/api/**endpint**`

### admins:

#### list of admins
without filters, this enpoint will fetch a full list o admins and super admins

* URL: `/admins/`
* Method: `GET`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* filter **query** paramater: `profile` (**values:** `admin` or `super_admin` ) 
* search **query** parameter : `full_name`

request example:
```
GET /admin_panel/api/admins?profile=admin&full_name=jhon
```

**Responses:**

> Code 200 ok
```js
   [
    {
        "id": "BIGINT UNSIGNED NOT NULL UNIQUE",
        "full_name": "varchar NOT NULL",
        "url_image": "varchar",
        "profile": "varchar NOT NULL"
    },
    ...
   ]
```
> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable
   



#### get an admin data

* URL: `/admins/:id_admin`
* Method: `GET`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes

request example:
```
GET /admin_panel/api/admins/123
```

**Responses:**

> Code 200 ok
```js
    {
        "id": "BIGINT UNSIGNED NOT NULL UNIQUE",
        "full_name": "varchar NOT NULL",
        "url_image": "varchar",
        "profile": "varchar NOT NULL"
    }
```
> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 404 Not Found`
   Not admin found
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable
   

#### created an admin

* URL: `/admins`
* Method: `POST`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* Body form-data format:
```js
    {
        "first_name": "varchar(100) NOT NULL",
        "second_name": "varchar(100)",
        "first_surname": "varchar(100) NOT NULL",
        "second_surname": "varchar(100)",
        "profile": "varchar(11) NOT NULL"
    }
```

request example:
```
POST /admin_panel/api/admins/
```

**Responses:**

> `Code 201 ok`
   The user admin was created
   
> `Code 400 Bad Request`
   The user with email already exist
   
> `Code 401 Unauthorized`
   It means that Auth token was not provided
 
> `403 Forbidden`
   the user is not allowed to create admins/super admins
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable
   

### Users:

#### list of Users
without filters, this endpoint will fetch a full list of users

* URL: `/users/`
* Method: `GET`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* filter **query** paramater: `status` (**values:** `verified`, `active`, `deleted` or `banned` ) 
* search **query** parameter : `full_name`

request example:
```
GET /admin_panel/api/users/?status=active&full_name=jhon
```

**Responses:**

> Code 200 ok
```js
   [
    {
        "id": "BIGINT UNSIGNED NOT NULL UNIQUE",
        "full_name": "varchar NOT NULL",
        "url_image": "varchar",
        "date_of_register": "varchar"
        "status": "ENUM"
    },
    ...
   ]
```

> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable


#### get an user data

* URL: `/users/:id_user`
* Method: `GET`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes

request example:
```
GET /admin_panel/api/users/123
```

**Responses:**

> Code 200 ok
```js
    {
        "id": "BIGINT UNSIGNED NOT NULL UNIQUE",
        "full_name": "varchar NOT NULL",
        "url_image": "varchar",
        "date_of_register": "varchar"
        "status": "ENUM"
    }
```
> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 404 Not Found`
   Not user found
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable

#### Edit an User

* URL: `/users`
* Method: `PATCH`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* Body form-data format:
```js
    {
        "first_name": "varchar(100) NOT NULL",
        "second_name": "varchar(100)",
        "first_surname": "varchar(100) NOT NULL",
        "second_surname": "varchar(100)",
        "email": "varchar(100) NOT NULL"
        "phone":"varchar(12) NOT NULL"
        "url_image": "varchar(200)"
    }
```

request example:
```
PATCH /admin_panel/api/users/
```

**Responses:**

> `Code 200 ok`
   The user was updated
   
> `Code 400 Bad Request`
   You have to include all required fields
   
> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable
   
   
 #### Change User status

* URL: `/user_status`
* Method: `PATCH`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* Body form-data format:
```js
    {
        "status": "ENUM",
    }
```

request example:
```
PATCH /admin_panel/api/user_status/
```

**Responses:**

> `Code 200 ok`
   The user was updated
   
> `Code 400 Bad Request`
   You have to include all required fields
   
> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable

### Places:

#### list of Places


* URL: `/places/`
* Method: `GET`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* filter **query** paramater: `status` (**values:** `active` or `inactive` )
* search **query** parameter : `name`, `host_name`

request example:
```
GET /admin_panel/api/places/?status=active&name=fake hotel
```

**Responses:**

> Code 200 ok
```js
   [
    {
     "name": "varchar",
     "status": "ENUM",
     "host_name": "varchar"
    },
    ...
   ]
```

> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable
   

### Booking:

#### list of Booking


* URL: `/bookings/`
* Method: `GET`
* Content-type: `Json`
* headers: `Authorization` (example `Authorization: Bearer a5sdf544s5df44f4sd...`)
* Auth required: yes
* filter **query** paramater: `date_of_book`,`status` 
* search **query** parameter : `place`, `user_name`

request example:
```
GET /admin_panel/api/bookings/?status=active&place=fake hotel
```

**Responses:**

> Code 200 ok
```js
   [
    {
     "date_of_book": "varchar",
     "user_name": "varchar",
     "status": "ENUM",
     "from_date":"varchar"
     "end_date":"varchar"
    },
    ...
   ]
```

> `Code 401 Unauthorized`
   It means that Auth token was not provided
   
> `Code 500 Internal Server Error`
   Unhandled error
   
> `Code 502 Bad Gateway`
   Any of the service we are connected with is no avaliable
   
> `Code 503 Service Unavailable`
   Our service is not avaliable

__________________________________


# Glosary
## user actions:

ban:  Prohibit a user from accessing the platform for having performed an action that is not permitted
edit: update user information
delete: update user status to `deleted`. it will denied  
validate: 

status de los usuarios

# Drawbacks

- no hay un formato definido aún para los perfiles (nombre de los perfiles), este RFC hace asunciones
- no tengo muy claro que significa validate, es decir, que puede o no puede hacer un usuario validad
- no se ha definido completamente el propósito de la tabla de places y booking, no hay accionables
- los accionables para estas tablas deberían ser editar y borrar
- los accionables para reservar deberían ser 
- no hay una clara diferencia entre buscador y filtro 
- no hay campos para banear, eliminar o verificar usuarios en la db de users
- solo los usuarios autheticados pueden crear usuarios?
- la comnunicación con el equipo de autenticación
- en el rfc del equipo encargado de autorización habla de un header Authorization pero los requerimientos dicen que este se debe hacer a tarvez de cookies

# Alternatives

N/A

# Adoption strategy

N/A

# How we teach this

N/A
