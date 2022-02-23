- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Members: (fill me with the names of the RFC creators)
- RFC PR: (leave this empty)

# Summary

- Priorizar 2FA con correo electrónico
- En caso de incrementar el scope del proyecto, agregar 2FA por SMS

<!-- # Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable. -->

# Motivation

- Importancia de un 2FA?
- ¿Por qué escogimos email para priorizar?

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
