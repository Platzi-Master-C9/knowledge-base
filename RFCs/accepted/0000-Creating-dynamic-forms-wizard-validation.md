Start Date: 2022-02-23
Members: Andrés F. Gallegos- @andresfgz, Jorge Torres - @jorgettor.
RFC PR: 

# Summary
 - Adding dynamic forms using wizard validation to help new hosts register their places for accomodation

# Basic example
-If a user wants to become a new host in Booking system this dynamic form will guide the user in the process of posting the new place with all the required information using a step by step process 

# Motivation
-Implementing the dynamic form using Wizard Validation will reduce all common mistakes made by the user  guiding them through the process step by step, helping them follow the sequence and facilitate the registration process of accomodations using the wizard form.
 
This Form Validation is the most stable and reliable plugin used, could be customized to the users needs and offers integration with other stacks


# Detailed design
C4 Model Placement Diagram 

![C4 Model Places!](https://raw.githubusercontent.com/JorgeTTor/rfc-forms/main/c2-placesTeam.png)

-Implementing the JavaScript Wizard form in our website will improve good user experience, delivering a more intuitive interface to fill information to make new accomodations registrations possible. 
 
 
Dynamic Form Flow Chart

![Dynamic Form Diagram !](https://raw.githubusercontent.com/JorgeTTor/rfc-forms/main/Flowchart-Validation.Form.jpeg)

Layer 2 Form Validation Diagram
This form will guide the user through the whole registration accomodation process and besides the login information will ask for more information such as:
Type of place: Hotel, Home, Apartment, Country House
Guests: Number of guest per accommodation
Services: Amenities availables at accomodation for the guest to use.
Pictures: This form will ask the user/host to post pictures of accomodation.
 
This form Validation offers integration with all different stacks.


# Drawbacks
-Constant Updating to fix bugs also it is important to determine how the information will be stored if the user does not complete the process. 
It will be very helpful to keep the information on hold until the user fulfills the complete form.


# Alternatives
There are another form design interaction patterns available to use like “Steps Left”, “Completenes Meter” or “Inline Help Box).


# Adoption strategy
If we implement this proposal, how will existing C9 developers adopt it? Is this a breaking change? Can we write a codemod? Should we coordinate with other projects or libraries?

# How we teach this
-To ensure that implementing this form validation will be successful we must collaborate effectively with Search Team, Data Monitoring team, User team, Geolocation team and Admin Team. 

# Unresolved questions
How are we going to keep the information on hold if the user does not complete the process?
Are we going to use  local storage ?
How is it going to be connected to the website database?
