-   Start Date: 2022-02-23
-   Members: @higueraDev
-   RFC PR:

# Summary

The Booking System must have a Notification System to alert users about reservations and places of interest.

-   Notification of reservations: a notification that the place has been reserved should be sent to the host of the place and also to the user who has just booked indicating that the reservation was successful.

-   When a guest indicates interest in an place, a notification of interest should be sent to the place host.

-   In the profile section of the navigation menu, the sum of notifications and conversations with messages pending to be read should be displayed.
-   When the profile menu is displayed, the messages and notifications section should show that there are items pending review.
-   In the notification view, notifications should can be deleted or opened.


# Motivation

Building the dashboard of notifications:

The user profile avatar on navigation bar + avatar menu.

-   What components does it use?

-   Should the Notifications System squad have ownership over some of them?

-   Over which ones?

# Detailed design

- Notifications dashboard layout

    ![Dashboard](https://i.imgur.com/1EX7Swa.png)
    The notification inbox in this design requires consuming the Notification System's own data and providing users with a user-friendly interface.

- User profile avatar

    ![Avatar](https://i.imgur.com/uZAcH8Z.png?1)

    The navigation bar + avatar menu is a shared component throughout the system. So the requirement for the notification system comes down to bringing a signal into the existing component. That should be built by the team in charge of the Landing page (Search Engine) or the User Account team. With the intention of maintaining a standard design.

- User profile avatar Menu

    ![Avatar Menu](https://i.imgur.com/DzmGp8V.png)

    In this menu also we should find messages, favorites, and account links, so this should be the same case that for the user profile avatar ownership.


