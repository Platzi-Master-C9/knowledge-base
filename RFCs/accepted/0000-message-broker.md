- Start Date: 2022-02-23
- Members: Chiristian López, Leo Licona, Johanna Reyes Rojas
- RFC PR: 

# Summary
In this document we describe the Message Broker proposal for processing asynchronous notifications from the Booking System, we fundamentally answer the following questions: what providers are there? How do they work? What should the flow be? reception of an event? How will we persist the history of the events, NoSQL? SQL? We will talk about our motivations, why we want to implement it and what results we wait?, we will approach the details of the design, the drawbacks, we will list some market alternatives and we will describe the strategy that we will adopt for its implementation. 

# Basic example

When make an order in an online shop, the system genre the guide of send, for report to his buyers the information of his order and when will arrive. If the system has many orders these accumulate. In occasions, these orders should validate and sent in a specific order. The messages brokers, allow make these process asynchronous, for don't affect the process of buy.

# Motivation

We need to ensure the reception of messages in short response times, establishing the priority of sending and simplifying the writing of the code.

# Detailed design

### What is a message broker?
They are a technology that allows interdependent systems, applications and services to communicate with each other and exchange information even if they were written in another programming language or implemented on different platforms. Specifically, it performs this function by translating messages between formal messaging protocols.

Message brokers are message-oriented middleware (MOM) software modules. It has the ability to validate, store, route and deliver messages to the right destinations, allowing senders to send messages without knowing where receivers are, whether they are active or not. They are based on a component called a message queue that stores and sorts messages in the exact order in which they were transmitted and remains in the queue until the applications that consume them acknowledge receipt and can process them.

Message brokers use a type of asynchronous communication that guarantees that messages will be delivered once (and only once) in the correct order relative to other messages. This allows systems to continue operating even in the face of intermittent latency or connectivity issues common on public networks, thus preventing the loss of valuable data. To handle interactions between multiple message queues, they rely on queue managers, as well as services that provide data routing, message conversion, persistence, and client state management functions.

### Components of a Message Broker

Producer: Refers to the endpoint that sends any type of data to the message broker.

Consumer: Refers to the endpoint that requests messages from the message broker and consumes them.

Queue: Queues store messages until a consuming service processes them under the FIFO scheme, first in, first out.

Exchanger: In addition to queues, which tells the message broker to create some kind of pool, in which consumers can listen to messages they receive or producers can write to send messages.

### Message Broker Models

They offer two basic message distribution patterns:

Peer-to-Peer Messaging: Used in message queues with a one-to-one relationship between sender and recipient. Each message in the queue is sent to a single recipient and is consumed only once. In these systems, both senders and receivers need a guarantee that each payment will be sent once and only once.

### Use Cases of Message Brokers

They are widely used in software development. Some use cases are illustrated below:

1. To develop a payment processing system, mesaage brokers ensure payment information is not lost or duplicated and provide proof of receipt.

2. To send data to various applications without making direct use of their API

# Drawbacks

### What are the disadvantages?

So far we have described how a message broker works, in this section we will address the disadvantages of implementing such a system:

- We depend on a service from an external provider for which the financial side has to be evaluated
- The team does not have previous experience in the use of message brokers, so they have to invest in learning


# Alternatives

1. **Celery**

Is a distributed task manager develop in python. Is a tool of disponibility and load high and also recommended when we consider that the load is going to increase progressively and we are going to incorporate new machines little by little to our initial cluster.
Celery is similar to RabbitMQ and Apache Kafka but much easier to implement.

**Advantages**
- Scalability.
- Efficiency.
- Guaranteed transaction order.
- Failure resistance.
- Enduring spikes in messages.
- Designed in one of the most powerful languages.

2. **RabbitMQ** 

The software Open source more widespread. It is easy to use, supports many development platforms, and multiple servers can be combined into one logical broker.
Implements the application layer messaging protocol AMQP (Advanced Message Queuing Protocol), which is focused on the communication of asynchronous messages with guaranteed delivery, through message receipt confirmations from the broker to the producer and from the consumers to the broker.

**Advantages**
- It is a software that adapts very well to Cloud environments.
- Fast message delivery.
- High availability.
- Reliability.
- Ease of scaling out the solution.
- 
**Disadvantages**
- Performance is an order of magnitude lower than other tools.

# Adoption strategy

The objective is to choose a tool that is more suitable for what is needed, is easy to implement and is coupled to the other components. It is important to emphasize the advantages it offers and the benefits of the application. It must be a solution with high availability, performance and understanding, to build trust in the team and facilitate its adaptation.

**If we implement this proposal, how will current C9 developers adopt it?**

This solution is related to the push and email type notification processes, since the message broker is an intermediary program between the notification systems and it is important to determine its inputs and outputs.

**Is this a sea change?**

No, because it does not interfere with any system module and the alternative solutions are easy to implement and connect.

**Can we write a codemod?**

To automate some validations on the messaging that is received.

**Should we coordinate with other projects or libraries?**

Yes, with the push and email type notification equipment, since the message broker is the intermediary in sending and receiving messages.

# How we teach this

Initially we must teach the basic concepts of how a messages broker tasks, taking into account that there are different roles in the team. It is important to use appropriate language, so that it is easier to understand.

**Messages brokers:** It is an intermediate program that is responsible for receiving messages in a queue and ensures that the recipient receives it following a series of criteria, such as priority, order of arrival, among others.

**Queue:** Data structure that contains a sequence of elements, which have an identifier. It has an injection operation and an extraction operation.


# Unresolved questions

- What effect can the chosen alternative have on the notification systems (email type and push type)?

- Is there a budget for the project or will it work with free software?

- What validations should be included when configuring the message broker tasks to establish the priority of the messaging - response?

- What programming language is the best?
