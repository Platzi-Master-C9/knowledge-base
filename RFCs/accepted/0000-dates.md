- Start date: 2022-02-21
- Members: Roberto Niño y Martin Chiquillo.
- RFC PR: 


# Summary

Managing dates is a little tricky due to the different timezones between countries.
It's important to declare how them will be treated during the development of the project.

We'll propose how to solve this problem is creating the API from scratch to have all the control of users and
the database.

# Motivation

When we are developing a booking system, the essential part of it will be the processes which
are supporting all the solutions to the problems. We believe the most important thing is to
design and follow a guide to manage the cleanest way dates, so, in the future, when this system has to be
implemented, there won't be any disruption and mismatches.

# Detailed design

This method stablishes create a Date object. (Not all parameters are required).

``` js
var myDateObj = new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds);

//Also we can set it individual attributes with:

setFullYear(), setMonth(), setDate(), setHours(), setMinutes(), setSeconds()

//This method is very useful because it allows to return the date in a the receiver's timezone format and language.

myDateObj.toUTCString(); // "Sat, 13 Jun 2020 18:30:00 GMT"
```

# Drawbacks 

- The success depends of designing this core system very well. It means that we have to solve the initial problems of timezones and dates, so with this solution, the booking system won't have any mismatch problem.
- The efficiency could be a problem if the app has a lot of petitions.
- We have to guarantee users data without compromising it.

# Alternatives

If we are having some trouble creating the system from zero, there is a web app and API called Booking.js (PONER LINK), which it's objective is to
simplify all the development and encapsulate it on a dashboard.

# Adoption strategy

It is important to make this a library so any project can use it depending on its structure, making the development
this way will help to understand and to improve code constantly. This system must be in constant communication with other
teams. We propose this as a SDK.
Our team could use this with a library managed by any package manager that could let them use the latest version we develop.

# How we teach this

This have to be taught to existing C9 developers because it will be made from scratch by our booking squad, so the other developers
would need to know how to use the library. The C9 documentation now should include all the information about this SDK, so it'll be
easier to anyone in the team to work with this (when we refer as anyone in the team, that person should be part of the booking squad).
