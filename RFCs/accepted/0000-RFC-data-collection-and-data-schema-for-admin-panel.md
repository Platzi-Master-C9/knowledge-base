- Start Date: 2022-02-24
- **Members**: Pedro Silva, Andrés Correa, Felipe Rodriguez, Mario Fuentes
- RFC PR:

# Summary

This RFC describes the data, its schema and type, for users, admins (and Superadmins), places and globalbooking list. It will be necessary in order to clarify which entities frondend can consume and what the formay of data is going to be. Our team will use databases created by Booking system, Users and Places but we will manage or own enpoints in order to format and simplify the work of the frontend (mejorar la redacción cuando no esté dormido)

# Basic example

(Pending)

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

### Data for User Profile

* id (is necesary to perform actions like validate user, is not visible in the interface)
* full_name (first_name + fist_surname)
* url_image
* date_of_register
* is_verified
* is_active
* is_delete

## Places
represent the places created by users (read only,)

### data for Places
* name
* is_active
* host name

## global booking
represent a list of all bookings (read only)

### data for Bookings
* date of book
* place
* user name
* is_active
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
        "first name": "varchar(100) NOT NULL",
        "second name": "varchar(100)",
        "first surname": "varchar(100) NOT NULL",
        "second surname": "varchar(100)",
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
_________________________________________________________________________________________________________________________________________________________________


## User profile structure 

### Profile User:



### API

**Endpoints:** 

- to view profile information / GET
- to create Profile: / POST
- to update profile / PUT

- If the user is not validated, an alert icon will be displayed in the table view next to their user picture
- non-validated users will have relevance in the order of the users table (they will appear first)

## User Management

**Data**
- Valid user/User to be validated
- User name
- User picture
- Date of registration and last modification (only show last modification in the table)

**Actions**
- ban
- edit
- delete
- validate (if applicable)

## Administrator login

- It will have a unique login view for both types of administrators. For instance: → [bookingsystem.com/admin](http://bookingsystem.com/admin)
- It is recommended that it can only be accessed through the url so that other users have no way of seeing it. (not links to it)

**Data for login**
- email
- password
- **Nice to have** ✨ → 2factor Authentication

## Admins and Super Admins Management

**Data**
- type of profile (admin/superadmin)
- name
- user picture
- date of registration and last modification (only show last modification in the table)

**Actions**
- edit
- delete
- **Nice to have** ✨ → an addicional table to manage admins and super admins pending invitations

## Filter Options

The views have filters by:
- date of creation
- last modification
- user name (for user table only)
- admin name (for admin table only)
- just for the admins table it is possible to filter by profile too

# Glosary
(pending)

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
