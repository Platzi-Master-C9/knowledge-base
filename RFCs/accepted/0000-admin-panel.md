- Start Date: 2022/02/23
- Members: Maided Hernandez
- RFC PR: (leave this empty)

# Summary
How can be organized admin, user and places information in a table.

# Motivation
We may do this in order to the next requirements:
- In order to organize the information of the users, admins and places.
- How can we identify if we are admins, super admins o just users
- In case of being admins or super admins, how can we know this. 
- How can we add more admins.
- For point one, we can design a table with 3 columns. 
- First column have Admins
- Second for users
- Third for places
Every column will have its own searcher and filter.
Also, every column will have a button. That button depends on what the column is. For example.
- Admins: when we click the button a modal will appear and we can add a new admin (it button will be available just for super admins)
- Users: we click the button and we will have 3 choices:
- Edit user: this modal will allows you to edit the user
- Ban user: with this, you can ban user and send to him/her an email in order to explain why
delete user: you can send an email to the user explaining that her/him account will be deleted.
We can receive a property that specifies what is the role of the user.
To identify the admins, we can put a flag next to his/her name
As the point one says, if you are a super admin, you can invite other people to be admin or super admin.

# Drawbacks

- We can or not have super admins
- We can do another way to send emails to delete or ban users.

# Alternatives

We can go to the user profile and that profile contains a ban or delete button and when we click that button, open a modal to write an email to send why are we doing this or what happen after delete the account.
Adoption strategy

# Adoption strategy

We can make a layout in Figma to represent the design. To the code, we can use atomic design and put global styles already defined in the Figma Layout.
How we teach this

# How we teach this

All of us can have this Figma Layout and create a file in the code with the global styles.
Also, we can create a Readme putting details of what design we are working on and that design in what it consists