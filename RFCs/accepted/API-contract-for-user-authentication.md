- Start Date: 2022-02-22
- Members: Jesus Velazquez & Sebastian Gonzalez
- RFC PR:

# Summary

Definition of api contract, endpoints, documentation of the apis and the necessary structure to have a good communication between front and back

# Basic example

The idea is to have a collection in postman with the necessary documentation of the flow and the apis, something like this

<img src="https://assets.postman.com/postman-docs/documentation-view-schema-docs-v9-12.jpg" alt="Postman collection documentation" />

# Motivation

Having a clear idea of what needs to be done, where you are going to start from and where you want to go is much simpler and more agile by creating documentation, being clear about the flows that are needed, the possible dependencies and the life cycle that will have every solution.

Having this clear and within everyone's reach, it is much easier to develop what is required and makes it easier to understand and integrate it for those who need to use it.

# Detailed design

- ## Why it's important to create a Sequence Diagram?
    It is important for the team to know what the development flow is like, what should be done first, what happens if something fails in any chain of APIs, how to act against possible multiple responses. know who is going to need the information, if the user must send or receive data, if a flow goes to an external provider or not.

  Having all this clear and defined avoids having gaps of ignorance between the members of the squad, being more agile and effective in the development of the requirement.

  A good way to create Sequence Diagram is to use UML, defining who interacts in the whole flow, user, database, Auth0, Api rests, etc, for example
  
  <img src='https://www.researchgate.net/profile/Kun-Ma-7/publication/272823002/figure/fig3/AS:294789619699714@1447294730609/Sequence-Diagram-of-Interaction-with-Our-OAuth2-authorization-RESTful-Feed-Sharing-Service.png' alt='api sequence diagram flow' />

- ## What technology do we use to document our APIs?
  Have a document or file with all the clear information on how to use / manipulate the apis, what parameters it receives, what method is POST?, GET? , DELETE ?, what headers do you need, do you need to receive a body, what will be its possible responses, the response codes that are expected to be obtained. all this is important for those who are going to use, modify or interact with the API's.
  
  Una opcion muy util es tener una coleccion en postman, no solo para almacenar y poder usar apis, sino que ademas se puede documentar aqui tanto la documentacion como cada uno de los servicios que estan dentro de ella, esto le permite al frontend  por ejemplo ver cual es el orden de llamado de las apis, que recibe y responde cada una y probarla ahi mismo. 
  
  <img src='https://assets.postman.com/postman-docs/documentation-pane-v9.jpg' alt='api documentation example i n postman' />

# Drawbacks

Why should we _not_ do this? Please consider:

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
