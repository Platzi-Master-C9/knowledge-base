- Start Date: (2022-02-22)
- Members: (Neisser Villa, Nahomi Conde)
- RFC PR: (leave this empty)

# Summary

Implementation of Mongo DB in a high concurrency chat system with CRUD operations that needs to be viawable for users in the chat room, where messages must be push to be seen in real-time.

# Basic example

{
  "users": {
    "user-id": {
      "firstName": "Martha",
      "lastName": "Garcia",
      "headline": "Just wandering…",
      "unread-messages-count": 34
    }

# Motivation

Real-time analytics: The City of Chicago has developed the application "WindyGrid" based on Mongo DB that collects data from police, transportation and fires in addition to notifying roadworks, noise complaints etc.

# Detailed design

Chat messages and chat input are integrated into the user profile, when the user has completed username and password upon login the server queries the database to verify that this data is correct (front-end needs support from authentication team). After this validation the user can start sending messages in the chat room with other users online, and that chat room is implemented with node.js mainly with the websocket protocol where the user information and password is stored in the database and the server opens a socket port to start listening to the client’s connection, 
then the client’s browser establishes a socket connection.

# Drawbacks

Why should we *not* do this? Please consider:

- Schemaless is a concept interpreted as lack of structure and storage control although, this versatility favors in agile development environments, do not standardize keys within the documents of a collection may involve unexpected behaviors in the application, therefore a base structure should be defined in their documents together with a strategy to control the changes that are made on them.
<!-- - whether the proposed feature can be implemented in user space -->
- MongoDB has matured, and so have the resources for learning how to use the database. The docs, mailing lists and user forums are all at least three years old and are available in a number of languages. Additionally, there are community developed resources for getting started, including the Little MongoDB book. Mongo DB allows you to query and manipulate data in JSON format, therefore see all the data of an ej: user would be a very simple query.
<!-- - integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?) -->

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Adoption strategy

If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries?

# How we teach this
 
What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing C9 projects patterns?

Would the acceptance of this proposal mean the C9 documentation must be
re-organized or altered? Does it change how C9 is taught to new developers
at any level?

How should this feature be taught to existing C9 developers?

# Unresolved questions

The main question will be how to make the right conection with other teams involve in the development of this feature.