- Start Date: 2022-02-21
- Members: Rodrigo Cabrera and Alexander Acosta
- RFC PR: 

# Summary

This RFC is intended to define the strategy that will be followed in order to create a feature that locks a place 
a user selects before to book it and sets an amount of time before blocking (if payment is completed) or 
releasing it (if payment is not completed) from locking.

# Basic example

A user wants to book a place inside the booking system, so after check in and checkout dates would have been selected,
the booking system has to lock the place on that period of time to avoid double bookings or potencial confict with overbooking

# Motivation

This feature is intended to improve the user experience by preventing conflicts with booking dates when a somebody has already selected 
a perioid of time that gets in conflict with dates that another user is trying to select.

It doesn't have to be the exact same dates to have a conflict, it could be just a couple of days or day.

Although this feature gives, the first user that picks dates, the opportunity to complete the process of booking, that doesn't mean that
place will be locked forever. In order to give an opportunity to other users a timer must be put before the place will be released from locking.

Dates will be locked when place is either booked or about to be booked.


# Detailed design

Since we are using React to develop this feature, the useState hook can be used using different states such as:

-Available: When the place isn't booked.
-Locked: When an user has selected check in and checkout dates but the booking isn't completed.
-Booked: When an user has completed the booking process and payment is verified.

When a place is locked, the system must show to the user that is in a booking process a timer with, let's say 5 minutes, to complete the booking process,
otherwise the place will be available and other users could try to book the place, and the user who hadn't completed the booking process 
will be returned to searching results.


# Drawbacks

This could be a little complex as we are working with different states that, by the time this RFC is being written, are 3 but with further planning 
and as the system grows, it might be a need to add more states leading to a sort of juggle between states and their validations.

Hooks are quite recent, there might be developers who couldn't be acquainted and could lack of expirence.

# Alternatives

*Could use redux to manage the different states in which a place could be put in.
*In the data base could exist a field, such as a check box that will be checked once the user select both dates, and it will be unchecked either timer 
runs out or the place is booked

# Adoption strategy

Hooks, useState hook in particular, are now part the stable version of React there is no need to add more libraries but what React
brings with it by default. 

Hooks are easier to reuse them and also test them.

# How we teach this

Since hooks are part of React, there are plenty resources to get used to them, such as documentation (https://reactjs.org/docs/hooks-intro.html) 
or courses to get acquainted with the use of Hooks

# Unresolved questions

Does validating state or holding a state have a considerable impact on performance?
