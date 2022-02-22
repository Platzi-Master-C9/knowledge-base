- Start Date: 2022-02-19
- Members: Paulina Ignacio, Edwin Páez
- RFC PR: 

# Summary

Generate QR code to visualize the digital ticket from booking.

# Basic example

<!-- If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable. -->

# Motivation

Sharing information about the client's booking for they or their guests. 
In case, the client or the person who booked decide to go with others. 
Therefore, when the person who scan the QR code would obtain the booking information (date, hour, location, phone, e-mail, etc.)

# Detailed design

<!-- This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here. -->

Cuál, cómo, y por qué implementamos

# Drawbacks

<!-- Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here. -->

¿Qué podría salir mal?

# Alternatives

<!-- What other designs have been considered? What is the impact of not doing this? -->

Share booking information by email.
Enviar la información de la reserva por medio de correo electrónico.

Podemos facilitar la implementación de esta funcionalidad por medio de librerias como
1. [qrcode](https://www.npmjs.com/package/qrcode)
2. [qrcode-with-logos](https://www.npmjs.com/package/qrcode-with-logos)
3. [easyqrcodejs](https://www.npmjs.com/package/easyqrcodejs)
4. [react-qr-code](https://www.npmjs.com/package/react-qr-code)

# Adoption strategy

<!-- If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries? -->

# How we teach this

<!-- What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing C9 projects patterns?

Would the acceptance of this proposal mean the C9 documentation must be
re-organized or altered? Does it change how C9 is taught to new developers
at any level?

How should this feature be taught to existing C9 developers? -->

¿Cómo funcionan los QR Codes?

# Unresolved questions

<!-- Optional, but suggested for first drafts. What parts of the design are still
TBD? -->

¿Qué información se debería mostrar en la factura?
¿En qué formato se daría esta factura?
