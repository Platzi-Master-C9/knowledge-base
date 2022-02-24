- Start Date: 2022-02-23
- Members: Chiristian López, Leo Licona, Johanna Reyes Rojas
- RFC PR: 

# Summary
En este docuento describimos la propuesta de Message Broker para el procesamiento 
asincrono de notificaciones del Booking System, respondemos fundamentalmente las  
sigientes preguntas ¿qué proveedores hay? ¿Cómo funcionan? ¿Cúal debe ser el flujo de 
recepción de un evento? ¿Como persisitiremos el history de los eventos, NoSQL? ¿SQL?
Hablaremos de nuestras motivaciones ¿por que queremos implementarlo y que resultados
esperamos?,abordaremos los dettalles del diseño, los drawbacks, enlistaremos algunas 
alternativas del mercado y describiremos la estrategia que adoptaremos para su
implementación. 

# Basic example

When make an order in an online shop, the system genre the guide of send, for report to his buyers the information of his order and when will arrive. If the system has many orders these accumulate. In occasions, these orders should validate and sent in a specific order. The messages brokers, allow make these process asynchronous, for don't affect the process of buy.
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
RabbitMQ implements the application layer messaging protocol AMQP (Advanced Message Queuing Protocol), which is focused on the communication of asynchronous messages with guaranteed delivery, through message receipt confirmations from the broker to the producer and from the consumers to the broker.
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