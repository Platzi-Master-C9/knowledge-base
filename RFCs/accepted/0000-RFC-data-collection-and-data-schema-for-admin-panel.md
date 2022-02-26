- Start Date: 2022-02-24
- **Members**: Pedro Silva, Andrés Correa, Felipe Rodriguez, Mario Fuentes
- RFC PR:

# Summary

This RFC describes the data, its schema and type, that will be necessary for administration panel, login and user management. 

# Basic example

N/A

# Motivation

Correctly defining the type of information that is going to be needed is the basis for being able to build any software solution. Once these parameters are clear, it is possible to start planning the type of architecture or the tools that are going to be used in the project.

# Detailed design

## Perfiles de administradores

There will be 2 administrator profiles:

- **Admin**: It can validate, edit, delete and ban users and places
- **SuperAdmin**: It can validate, edit, delete and ban users and places. It can also manage profiles of admins and superadmins.

- The option to add admin will only be available for super admins.
- There will be an endpoint to verify if the session belongs to an admin or a super admin and then, enable or disable the option.


### Ways to create admin/super admin profiles

> This option is only available for **SUPERADMINS**
> 
1. Sending an invitation via email
2. Giving admin or super admin permissions to an existing user from the users management table (option available from the users table or from the modal to edit the user)

<!--## User profile structure `(pending)`-->

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

- It will have a unique login view for both types of administrators. for instance: → [bookingsystem.com/admin](http://bookingsystem.com/admin)
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

# Drawbacks

N/A

# Alternatives

N/A

# Adoption strategy

N/A

# How we teach this

N/A
