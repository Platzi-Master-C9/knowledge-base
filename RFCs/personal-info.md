- Start Date: 2022-03-10
- Members: Mauricio Perera
- RFC PR:

# Summary

This feature generate a view of personal info of the current user where the user can see and edit her.

# Basic example

![image](https://user-images.githubusercontent.com/4333910/157151928-dfab5252-8954-49fe-b6e0-c66e61378336.png)

# Motivation

The user need a profile page to set and update his personal info, and we need validate and check this to garantized they reserved in a secure place.

# Detailed design

![image](https://i.ibb.co/mB8jbxx/Screenshot-2022-03-10-at-20-53-11-Editing-knowledge-base-0000-personal-info-md-at-main-Mauricio-Pere.png)

This feature take a single view and work with element states to get and show the data. We use individual data to make a component to show or edit the info.

![image](https://i.ibb.co/njLYvz2/Screenshot-2022-03-10-at-20-59-08-Editing-knowledge-base-0000-personal-info-md-at-main-Mauricio-Pere.png)

When a user pick on any "Editar" button only the respective data change to an editable input.

![image](https://i.ibb.co/yNgrkqy/Screenshot-2022-03-10-at-21-06-25-Code-Sandbox.png)

![image](https://i.ibb.co/jRX9rrB/Screenshot-2022-03-10-at-21-16-19-Code-Sandbox.png)

And when a user selects the "Save" button, the editable input returns to its original state preserving the changes made.

![image](https://i.ibb.co/Xt3vS3T/Screenshot-2022-03-10-at-21-23-11-Code-Sandbox.png)

![image](https://i.ibb.co/ZdgvhPH/Screenshot-2022-03-10-at-21-25-04-Code-Sandbox.png)

# Drawbacks

The function is really minimalistic and functional if you have an idea of how to use it. But if you are a new user you may have some problems starting to use this, use a single form to edit all the data is another possibility.

# Alternatives

A single form to edit all the data is another possibility

# Adoption strategy

The proposal is continued whith the style of the site, its a clean, intuitive and modern design. About the functionality, our users ar humans, this change the siti, country, documentation, and ideas, we need take this in concideration and set a functionality where they can set your data and update this in the future.
This function need connect to the user data and need can make a update of the data changes. By security we need validate what only afect the current user data.

# How we teach this

We need predefined what its the data about the user what we need in the sistem and what we claim this data to the user.

For example we can use a single input to set the fullname, or an iput to names, and other to surnames. If wee need change the user data structure in the DB its probably we need upgrade this function

# Unresolved questions- How can i validate for example the identification when this change between countries.

- User need edit the identification number? the identification its unic fos any people forever,  i think this data never beed change
- If the user pick on edit button and after in save button whothout change the data value wee send this info to db or need validate when data is changed.
- How i notify the user when the DB not can acept there info, or if we have any other troble similar.
- We need add an imput to user change the profile photo on this form?
- To validate theaddres we can use a geolocation service, for example google maps and use an autocomplete. You think if this its necesary or not? 
