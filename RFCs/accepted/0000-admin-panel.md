- Start Date: 2022/02/23
- Members: Maided Hernandez
- RFC PR: (leave this empty)

# Summary
How can be organized admin, user and places information in a table.

# Motivation
We may do this in order to the next requirements:
1. In order to organize the information of the users, admins and places.
2. How can we identify if we are admins or super admins
3. How can we add more admins.

# Detailed design

Last week the team and I defined how the information will be organized.
The information was like this:
On the side of the screen will be four sections:

|   |
| ------------ |
|  Métricas |
|  Usuarios |
|  Administradores |
| Alojamientos |


Each section will have its own table. Each table will be in order to have a better organization of the information. Based on this organization, every admin can have better control, for example, who’s verified?
I’ll focus on sections after metrics.


#### Users

|  Nombre | Tipo  | Estado  | Validación  | Fecha  |   |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| Nombre del usuario  | Validado  |  Activo | Sí  | Fecha  | Manejar  |


Here we can see table for users. The filters of this table will be “Tipo”, “Estado”, “Validación” and “Fecha”

These will help us to find the information faster. If you clicked:

- Tipo: a card will be displayed. That card will give you the option if the user that you are searching is “Anfitrión” or “Hosted”.
- Estado: you can select if her/him user is active or not. 
- Validación: you can select if the user is validated or not.
- Fecha: Finally you can find that user for the date of her/him register.

“Manejar” will display the options: Edit, validate, ban or delete.


#### Admins and super admins:

Here, things change a little bit. 
First we need to know, are we admin or super admin?
Well, for this, depending on that, we can have a badge on the frontend in order to identify this.
Second, some things will disabled to admins:
- Edit another admins or super admins
- Add more admins
- Add more super admins or an admin makes super admin.

Their table will be similar to the users, but the “Tipo” filter changes:
- Tipo: We can select if we are searching super admin or admin

“Manejar” will display the options: Edit, validate, ban or delete. Also, in this case, we can add the option “Invitar” and this will invite someone that you choose in order to be super admin and when it happens, will display a modal with the email of the person and a field to put the description (this description is to explain why we are inviting and one link).
When the person opens that link, automatically will be admin.


#### Places:

Same, the table for this case will be same as the others, but filters will change:
- Tipo: You can select if the place is an apartment or house. 
- Estado: You can see if the place has already been hosted. Also, will have for how many people are hosted.
- Validado: We can see, is this place validated?
- Fecha de inicio: This filter it's only for the places. You can see the start date of the host.
- Fecha final: This filter it’s only for the places too. And you can see the end of the host.


###### For ban
This feature it’s for anyone that does not comply with the rules of the site. When we select ban to some user or some admin, we will show a modal that has two fields.

1. Email: You need to write ban user email.
2. Description: Why are we doing this?

When we click send, the user will ban and he/she will receive that email.


###### For delete:
When we delete a user, we send an email through a modal (similar to the ban modal), but this email will notify the user that was deleted.

###### For edit user:
When we select “editar”, we can edit some fields like user name through a modal.

###### For edit admins:
Only super admins can do this and this action is similar to edit user action.

“Manejar”: Will have the same options but we can omit the ban (ban it’s just for users or admins).


# Drawbacks

- We can or not have super admins
- We can do another way to send emails to delete or ban users.

# Alternatives

We can go to the user profile and that profile contains a ban or delete button and when we click that button, open a modal to write an email to send why are we doing this or what happen after delete the account.

# Adoption strategy

We can make a layout in Figma to represent the design. To the code, we can use atomic design and put global styles already defined in the Figma Layout.

# How we teach this

All of us can have this Figma Layout and create a file in the code with the global styles.
Also, we can create a Readme putting details of what design we are working on and that design in what it consists