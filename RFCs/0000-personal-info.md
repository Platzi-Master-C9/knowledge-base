
- Start Date: 2022-03-10
- Members: Mauricio Perera
- RFC PR:

# Summary

This function generates a view of the current user's personal information where he can see and edit it.

# Basic example

![image](https://user-images.githubusercontent.com/4333910/157151928-dfab5252-8954-49fe-b6e0-c66e61378336.png)

# Motivation

The user need see and update your personal info.

# Detailed design

![image](https://i.ibb.co/mB8jbxx/Screenshot-2022-03-10-at-20-53-11-Editing-knowledge-base-0000-personal-info-md-at-main-Mauricio-Pere.png)

This feature take a single view and work with element states to get and show the data. We use individual data to make a component to show or edit the info.

![image](https://i.ibb.co/njLYvz2/Screenshot-2022-03-10-at-20-59-08-Editing-knowledge-base-0000-personal-info-md-at-main-Mauricio-Pere.png)

When a user pick on any "Editar" button only the respective data change to an editable input.

![image](https://i.ibb.co/yNgrkqy/Screenshot-2022-03-10-at-21-06-25-Code-Sandbox.png)

![image](https://i.ibb.co/jRX9rrB/Screenshot-2022-03-10-at-21-16-19-Code-Sandbox.png)

And when a user selects the "Guardar" button, the editable input returns to its original state preserving the changes made.

![image](https://i.ibb.co/Xt3vS3T/Screenshot-2022-03-10-at-21-23-11-Code-Sandbox.png)

![image](https://i.ibb.co/ZdgvhPH/Screenshot-2022-03-10-at-21-25-04-Code-Sandbox.png)

# Drawbacks

The function is really minimalistic and functional if you have an idea of how to use it. But if you are a new user you may have some problems starting to use this, use a single form to edit all the data is another possibility.

# Alternatives

A single form to edit all the data is another possibility

# Adoption strategy

The proposal is continued whith the style of the site, its a clean, intuitive and modern design. About the functionality, our users ar humans, this change of city, country, documentation, and ideas, we need take this in concideration and set a functionality where they can set your data and update this in the future.

This function need connect to the user data and make a updates based on the user data changes. By security we need validate only afect the current user data and never make changes on others.

# How we teach this

We need predefined what its the specific user data what we need in the sistem and ho we claim this data to the user.

For example we can use a single input to set the fullname, or an iput to names, and other to surnames. If wee need change the user data structure in the DB its probably we need upgrade this function

# Unresolved questions- How can i validate for example the identification when this change between countries.

- Does the user need to edit the identification number? The identification is unique for any person forever, I believe that this data will never need to change
- If the user pick on edit button and after in save button without changing the data value wee send this info to db or need validation when data is changed.
- How I notify the user when the DB not can accept their info, or if we have any other trouble similar.
- We need add an input to user change the profile photo on this form?
- To validate the address we can use a geolocation service, for example Google Maps and use an autocomplete function. You think if this it's necessary or not?
