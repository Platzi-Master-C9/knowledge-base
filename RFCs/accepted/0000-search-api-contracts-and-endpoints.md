- Start Date: (2022-02-24)
- Members: (Javier Alexander Cañón, Juan Carlos Sarmiento)
- RFC PR: (leave this empty)

# Summary

API contracts in very general terms refer to the documentation of the endpoints that will be available in it and to the detailed way in which users will be able to use the API. Ideally, these contracts should be clear and very specific. to facilitate the use of our application, containing in detail the available endpoints, the response examples and the details of the errors that can be generated.

We believe that the best alternative is to make use of the standards and technologies that currently mark the design of modern APIs, for this case we have investigated and we believe that the best way is to base the work on the OpenAPI standard, relying on the Swagger tool to create the general definition of the API, because in addition to being the current standard supported by the large technology industries, it has a complete and detailed concept that favors the understanding of the operation of our application and its construction.

# Basic example

  openapi: 3.0.1
  info:
    title: Our-Booking-Api
    description: RESTful API built with node.js
    version: 0.0.1
    license:
      name: MIT
      url: 'https://our-booking-api.info'
  servers:
    - url: 'https://our-booking-api.info'


  paths
  /search/property-type:
      get:
        tags:
          - search
        description: Get all unique property types listed in the database
        responses:
          '200':
            description: OK
          '400':
            description: Client error
        servers:
          - url: 'https://our-booking-api.info'
      servers:
        - url: 'https://our-booking-api.info'

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