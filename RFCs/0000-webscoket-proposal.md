- Start Date: 
- Members:  
--@JoseNoriegaa
--@taberoajorge
- RFC PR: 

# Summary

**c9-messaging-system-squad**

After several evaluations and research, the best way to manage a chat system is through websockets, in this RFC the implementation of the socket.IO library is proposed.


# Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

# Motivation

In this RFCs we propose the implementation of a library for the management of WebSockets in the chats system belonging to the booking system.

With the use of this library, we can:

- Maintain an open communication between the host and a user.
- Manage in the best way a chat through WebSockets to avoid the use of multiple requests between users and avoid the use of resources.

# Detailed design

Implementation of websocket and its event handling to facilitate real-time communication between a host and a user.

Use of API that implements the requests corresponding to the business logic, including the visualization and creation of records.

![](https://i.imgur.com/RLG0xqC.png)

# Drawbacks

This decision directly influences the existing data creation in our database.

# Alternatives

[websocket](https://github.com/theturtle32/WebSocket-Node/blob/HEAD/docs/index.md "websocket") library

# Adoption strategy [newbie]



# How we teach this [newbie]

The use of this library requires knowledge of how websockets work and how the implementation of websockets are suitable for the chat system.
It also requires reading the documentation for handling methods of this library.

# Unresolved questions

Relationship of websocket connection to external booking system notification system
