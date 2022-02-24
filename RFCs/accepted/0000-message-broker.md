- Start Date: 2022-02-23
- Members: Chiristian López, Leo Licona, Johanna Reyes Rojas
- RFC PR: 

# Summary
In this document we describe the Message Broker proposal for processing asynchronous notifications from the Booking System, we fundamentally answer the following questions: what providers are there? How do they work? What should the flow be? reception of an event? How will we persist the history of the events, NoSQL? SQL? We will talk about our motivations, why we want to implement it and what results we wait?, we will approach the details of the design, the drawbacks, we will list some market alternatives and we will describe the strategy that we will adopt for its implementation. 

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
What is a message broker?
They are a technology that allows interdependent systems, applications and services to communicate with each other and exchange information even if they were written in another programming language or implemented on different platforms. Specifically, it performs this function by translating messages between formal messaging protocols.

Message brokers are message-oriented middleware (MOM) software modules. It has the ability to validate, store, route and deliver messages to the right destinations, allowing senders to send messages without knowing where receivers are, whether they are active or not. They are based on a component called a message queue that stores and sorts messages in the exact order in which they were transmitted and remains in the queue until the applications that consume them acknowledge receipt and can process them.

Message brokers use a type of asynchronous communication that guarantees that messages will be delivered once (and only once) in the correct order relative to other messages. This allows systems to continue operating even in the face of intermittent latency or connectivity issues common on public networks, thus preventing the loss of valuable data. To handle interactions between multiple message queues, they rely on queue managers, as well as services that provide data routing, message conversion, persistence, and client state management functions.

Message Broker Models
They offer two basic message distribution patterns:

Peer-to-Peer Messaging: Used in message queues with a one-to-one relationship between sender and recipient. Each message in the queue is sent to a single recipient and is consumed only once. In these systems, both senders and receivers need a guarantee that each payment will be sent once and only once.

Publish and Subscribe: The producer of each message publishes it to a topic, and various message consumers subscribe to topics about which they want to receive messages. All messages posted to a topic are distributed to all subscribed apps.

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