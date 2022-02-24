- Start Date: 2022-02-23
- Members: Saúl Regalado
- RFC PR: (leave this empty)

# Summary

Use the faker.js library to mock data, since it has several properties that generate data similar to what is expected in everyday use of the system.


# Basic example

- faker.name.firstName() ---->  Cameron

- faker.phone.phoneNumber() —-->  +1 291-299-0192

- console.log(
    faker.fake('{{name.lastName}}, {{name.firstName}} {{name.suffix}}')
  );



# Motivation

In order to guarantee the correct develope of all data processing, the need arises to test the implementations, with data as close as reality we can generate:

- Check if it is the expected data type.
- The correct process is applied to each of the data.
- Measure the performance of the application, if the process is applied effectively.



# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.


# Drawbacks

Its implementation is limited solely to testing the development's ability to process the required information, however, with this proposal we cannot measure software performance


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
