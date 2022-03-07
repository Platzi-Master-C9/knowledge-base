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

### Ways to create Admins and SuperAdmin profiles


1. Sending an invitation via email
2. Giving admin or super admin permissions to an existing user from the users management table (option available from the users table or from the modal to edit the user)

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

###data for Bookings
* date of book
* place
* user name
* is_active
* from date
* end date

## End points
thi seccion details the required end points for the admin panel:


_________________________________________________________________________________________________________________________________________________________________


## User profile structure 

### Profile User:

- ID = int (Primary key - Required)
- Name, Last Na : String
- Gender = (famele,masculine)
- Email :  only mail format @
- IDentification: Dni, Passport = str
- Cellphone : Int (Optional)
- Rol: (Admin, SuperAdmin)
- Country :  str (optional)
- Password: 8 character
- Check : Boolean (True or False)
- Validate : Boolean(True or False)
- Type : (guest or host)
- Birthday : date (optional)

### ERD - User_Profile

![](https://rare-impala-2c3.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F168b4952-a2b4-49d0-955d-de6f18b6290a%2FUntitled.png?table=block&id=d635e84b-a38d-4bd0-95ff-60e6c556c3a2&spaceId=e2f2a10e-d731-451c-9ab0-489a2ba13306&width=2000&userId=&cache=v2)


### API

**Endpoints:** 

- to view profile information / GET
- to create Profile: / POST
- to update profile / PUT

![](https://rare-impala-2c3.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7f70d8cc-98d2-4221-87c7-07ddb0e26221%2FAPI_PROFILE_USER.png?table=block&id=1958fc70-7013-482b-a3e7-1f04bbdcfb4b&spaceId=e2f2a10e-d731-451c-9ab0-489a2ba13306&width=2000&userId=&cache=v2)


## User validation

- There will be an administrator by geographical region who will be in charge of validating users corresponding to that region.
- It will be used the notification via Email system
- It will be used the notification via text message system

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

# Alternatives

N/A

# Adoption strategy

N/A

# How we teach this

N/A
