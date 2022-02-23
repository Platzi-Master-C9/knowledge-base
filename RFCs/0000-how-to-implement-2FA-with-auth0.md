- Start Date: (2022-02-21)
- Members: [Cristian Diaz](https://github.com/ItsCrisDiaz), [Saul Zamora](https://github.com/G-zeus)
- RFC PR: (leave this empty)

# Summary

After evaluate types of **2FA**, it is proposed to implement **Email Token** as a priority over **SMS Token** . In case of project scope get bigger, **SMS Token** will be a priority too for more security in authentication of users.

<!-- # Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable. -->

# Motivation

The growth of internet and its systems has required more security for users and his identities, therefore techniques have been created like 2FA consisting of requiring a user to verify their identity in two unique ways before they are granted access to the system.

Two Factor Authentication gives the user and system administrator a peace of mind as it ensures that even if the users password is compromised the account cannot be accessed without also knowing not only the method used as the second factor but also having access to the second factor such as a dynamically generated.


In this case we sugest implement  **Email Token** in tha begining of life for the application becouse is easyer for the user and provides necesary confidence.

<!-- # Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here. -->

# Drawbacks

Even considering having a reduced scope for the sake of MVP, email 2FA implementation has some disadvantages:

- **Failing of being delivered:** there are some scenarios where e-mails can be failed to be delivered. Events like email going to spam, being bounced by server, having a delay in delivery can cause some issues. This could be solved with giving enough time to users to add the 2FA code (to mitigate the impact of delay in delivery) and recommending users to check for spam folder just in case (to avoid the fact that email going to spam can cause problems).
- **Security:** emails can be intercepted by 3rd parties and tokens compromised.
- **Redundancy:** it's possible that if a 3rd party gains access to user's account, they _can_ gain access to user's email as well, and thus easily get the token.

# Alternatives

Another alternative we highly encourage to use if scope can be increased is adding a **SMS 2FA**, it has some advantages like being user friendly, having a low cost of setup and maintenance, and being widely available.

However, it has some disadvantages we took into consideration to decide we should prioritize email 2FA:

- **Connectivity:** cell signal, reception and country availability are required to receive tokens. This last point is important because in the case one of our target countries is not available, it'd harm project's reach.
- **Security:** SMS messages can be intercepted by 3rd parties.
- **Hardware:** physical device required so if phone is lost or stolen the user cannot authenticate.

<!-- # Adoption strategy

If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries? -->

<!-- # How we teach this

What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing C9 projects patterns?

Would the acceptance of this proposal mean the C9 documentation must be
re-organized or altered? Does it change how C9 is taught to new developers
at any level?

How should this feature be taught to existing C9 developers? -->

# Unresolved questions

- Detaile design
- Adoption strategy
- How we teach this?
