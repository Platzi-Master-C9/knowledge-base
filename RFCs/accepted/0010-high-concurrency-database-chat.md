- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Members: (fill me with the names of the RFC creators)
- RFC PR: (leave this empty)

# Summary

Brief explanation of the feature.

# Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

# Motivation

Why are we doing this? What use cases does it support? What is the expected
outcome?

Please focus on explaining the motivation so that if this RFC is not accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind.

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

# Drawbacks

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)

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

Optional, but suggested for first drafts. What parts of the design are still
TBD?


https://openwebinars.net/blog/mongodb-vs-redis/

Hi team, I hope you had a great Monday. This is our sprint 0 and I want to set clear goals for the following two weeks (each sprint is 2 weeks long btw) so, we have been in a lot of sessions learning a lot (and panicking a little) in the last week, so based on some of that knowledge we need to accomplish the following:
Read all the documentation related to the project in Notion and make any questions you may have. Make sure you understand what we are building.
Based on the business rules we need to create the RFCs necessaries to the  domain this squad will cover…..
Aquí tienen un recurso para estudiar sobre RFCs
Remember, in a RFC we expose a problem and a possible solution. Start by learning about RFCs and create your own, identify features, things to solve. Tomorrow we will do pairs to work these RFCs, for now start by your own.
Platzi on Notion
Request for comments - RFC
Descripción


 you are currently working in a specific RFC that’s great (I know some of you are) let me know and add them also to the repository as a WIP (follow this instructions). We may implement more RFCs on the future, remember is a tool for taking decisions, the most important part is the discussion this “requests” generates.
Here is more information about the topics (in spanish so everyone gets it):
Websocket technology proposal to use with nodejs
El problema es: necesitamos mantener una conexión abierta y de rápida respuesta entre dos usuarios.
How to keep privacy in chats.
El problema es: es muy importante que las conversaciones privadas no puedan filtrarse o ser consultadas por nadie más que los participantes de la misma.
¿Cómo encriptamos la información? ¿Cómo la guardamos en base de datos? ¿Qué esquema de datos deberías usar?
What database is better to handle a high concurrency chat
Recuerden los conceptos de ACID y BASE
¿Qué es lo que más necesitamos aquí?
Vamos a guardar cache?
Usamos redis, usamos mongo?
UI flow on how to uses the messaging system
Take in consideration the current UI for messages.
Toma en consideración las UIs que ya tenemos en figma para los mensajes.
¿Cómo se integra este sistema con el resto de la aplicación? es algo como lo que vemos en linkedin?

https://www.cometchat.com/blog/chat-application-architecture-and-system-design


https://neo4j.com/blog/acid-vs-base-consistency-models-explained/