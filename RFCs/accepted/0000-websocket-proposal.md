- Start Date: 
- Members:  
--@JoseNoriegaa
--@taberoajorge
- RFC PR: 

# Summary

**c9-messaging-system-squad**

After several evaluations and research, the best way to manage a chat system is through websockets, in this RFC the implementation of the socket-IO library is proposed.

For this implementation, issues such as the consistency of the data in front of the data participant were evaluated, so also in this RFC the use of a Pub/Sub is proposed for the consistent distribution of the data. For this reason, we considered the use of a Pub/Sub service for consistent data distribution. 
Redis Enterprise Cloud - Flexible plan which would adjust for the uncertain amount of requests, and meets our objective.


# Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

# Motivation

In this RFCs we propose the implementation of a library for the management of WebSockets in the chats system belonging to the booking system.

With the use of this library, we can:

- Maintain an open communication between the host and a user.
- Manage in the best way a chat through WebSockets to avoid the use of multiple requests between users and avoid the use of resources.
- In order to achieve data consistency we implemented the idea of using a pub-sub pattern, this with the use of a provider that adjusts to the amount of requests that we could have.
- In terms of consistency it allows us to have the data correctly even if our application lives in different servers where the participation of this pub-sub would be to consistently distribute the information.

# Detailed design

Implementation of websocket and its event handling to facilitate real-time communication between a host and a user.

Use of API that implements the requests corresponding to the business logic, including the visualization and creation of records.

### Flow
![flow](https://user-images.githubusercontent.com/28733681/156680962-78d27c17-df6a-4b98-ad5b-657982f3deef.png)

#### Flow Description.
- When an authenticated user starts to interact with the application, a websocket connection will be initialized providing the JWT of the current session.
- The WebSocket server will authenticate the user with the provided JWT and once it is authenticated, it will join the user to a room with the same name as its id (We are going to get the id of the decoded token). Personal room will allow us to send events to all the devices that the user is logged in.
- Once the WebSocket connection is ready, we subscribe the user to the chat events.
- If the user tries to contact to another user, we are going to send a request to open a chat room, if the chat room does not exist it will be created and a WebSocket event about the new chat is going to be send to the other user involved. Otherwise, it returns the existing chat information without sending any WebSocket events.
- If the API response with a 200 status code, we are going to request the previous messages of that conversation, and if it response with 201 we do not request the messages because is a new chat room.
- When the user creates a message into a chat room, we are going to send a POST request to the API that will store the message in the database and will send the WebSocket notification to the other user involved.

### API REST
The API Rest would be responsible of the CRUD operations of the messaging system.

#### Endpoints
##### List Chat Rooms
This endpoint returns the list of chats of a user.

- **HTTP Method**: GET
- **URL**: https://example.com/api/v1/chats
- **Content Type**: application/json
- **Authorization**: Bearer Token (JWT)

###### Response 200 (Ok)
It returns the list of chat rooms paginated to 10 elements and ordered by the most recent activity.

**Response Example**
```typescript
{
 current: 1,
 total: 1,
 results: [
   {
     id: string,
     members: string[] | number[],
     created_at: Date,
     created_by: string,
     last_message: {
       id: string | number,
       room_id: string,
       from: string | number,
       body: string,
       created_at: Date
     }
   }
 ]
}
```

###### Response 401 (Unauthorized)
This response represents a deny of service due to invalid or missing credentials.

**Response Example**
```typescript
{
  detail: string,
}
```

###### Open a chat room
This endpoint will return the chat room between two users and if it not exists it will create it. When the user creates a new chat room, the other user involved will receive a notification about the new convesation.

- **HTTP Method:** POST
- **URL:** https://example.com/api/v1/chats
- **Content Type:** application/json
- **Authorization:** Bearer Token (JWT)
- **Request Body:**
```typescript
{
  host_id: string | number,
}
```

###### Response 201/200 (Created/Ok)
After creating a new chat room (if not exists) it will return registered information.

**Response Example:**
```typescript
{
 id: string | number,
 members: string[] | number[],
 created_by: string,
 created_at: Date,
}
```

###### Response 400 (Bad request)
This response will be send when there are errors in the request data.

**Response Example:**
```typescript
{
 errors: [
   {
     location: ‘body’ | ‘headers’ | ‘query’ | ‘params’,
     msg: string,
     param: string,
   },
 ],
}
```

###### Response 401 (Unauthorized)
This response represents a deny of service due to invalid or missing credentials.

**Response Example**
```typescript
{
  detail: string,
}
```

##### List chat messages.
This endpoint will return the list of messages that belongs to a specific chat room.

- **HTTP Method:** GET
- **URL:** https://example.com/api/v1/chats/:id/messages/ 
- **Content Type:** application/json
- **Authorization:** Bearer Token (JWT)

###### Response 200 (Ok)
List of messages paginated to 10 elements.

**Response Example:** 
```typescript
{
 current: 1,
 total: 1,
 results: [
   {
     id: string | number,
     from: string | number,
     body: string,
     created_at: Date
   }
 ]
}
```

###### Response 404 (Not found)
This response will be send if the chat room does not exists.

**Response Example:**
```typescript
{
  detail: string,
}
```

###### Response 401 (Unauthorized)
This response represents a deny of service due to invalid or missing credentials.

**Response Example**
```typescript
{
  detail: string,
}
```

##### Create a new message
This endpoint will create a new message into a specific conversation.

- **HTTP Method:** POST
- **URL:** https://example.com/api/v1/chats/:id/messages
- **Content Type:** application/json
- **Authorization:** Bearer Token (JWT)
- **Request Body:**
```typescript
{
  message: String,
}
```

###### Response 201 (Created)
This request will be send when the message has been successfully created.

**Response Example:**
```typescript
{
 id: string | number,
 room_id: string,
 from: string | number,
 body: string,
 created_at: Date
}
```

###### Response 400 (Bad request)
This response will be send when there are errors in the request data.

**Response Example:**
```typescript
{
 errors: [
   {
     location: ‘body’ | ‘headers’ | ‘query’ | ‘params’,
     msg: string,
     param: string,
   },
 ],
}
```
###### Response 404 (Not found)
This response will be send when the chat room does not exists.
```typescript
{
  detail: string,
}
```

###### Response 401 (Unauthorized)
This response represents a deny of service due to invalid or missing credentials.

**Response Example**
```typescript
{
  detail: string,
}
```

### Websockets
The websocket service will implement a pub-sub pattern with redis in order to increase the scalability.

#### Architecture
![ws-architecture](https://user-images.githubusercontent.com/28733681/156296987-265aa672-c484-4f73-aeca-77b279a3d4d8.png)

### **Session store**

Redis as an in-memory data store with high availability and persistence is a popular choice among application developers to store and manage [session data](https://aws.amazon.com/blogs/developer/elasticache-as-an-asp-net-session-store/) for internet-scale applications. Redis provides the sub-millisecond latency, scale, and resiliency required to manage session data such as user profiles, credentials, session state, and user-specific personalization.

### **Chat, messaging, and queues**

Redis supports Pub/Sub with pattern matching and a variety of data structures such as lists, sorted sets, and hashes. This allows Redis to support high performance [chat rooms](https://aws.amazon.com/blogs/database/how-to-build-a-chat-application-with-amazon-elasticache-for-redis/), real-time comment streams, social media feeds and server intercommunication. The Redis List data structure makes it easy to implement a lightweight queue. Lists offer atomic operations as well as blocking capabilities, making them suitable for a variety of applications that require a reliable message broker or a circular list.


#### Events
##### New message
This event will allow users to receive updates about chat messages in real-time. The websocket server will send this event to the user with the message description attached to it.

- **Event emitter:** Server
- **Event name:** new_message
- **Payload:**
```typescript
{
 id: string | number,
 room_id: string,
 from: string | number,
 body: string,
 created_at: Date
}
```

##### New conversation
This event will notify users that a new conversation has been initialized. This event will be sent by the websocket server to the host user involved in the conversation.

- **Event emitter:** Server
- **Event name:** new_chat
- **Payload:**
```typescript
{
 id: string | number,
 members: string[] | number[],
 created_at: Date,
 created_by: string | number,
}
```

# Drawbacks
- This decision directly influences the existing data creation in our database.
- Socket-io requires to use a specific client library in order to work, this library will increase the bundle size of the application in around 80KB.
- Team members have not previous experience using redis with socket-io.
- If the number of requests is not defined, the cost of consuming services from external providers would increase significantly.

# Alternatives
- Use [websocket](https://github.com/theturtle32/WebSocket-Node/blob/HEAD/docs/index.md "websocket")
- Write our own websocket server using the native nodejs modules (`http` or  `net`)
- Fetch the messages in the application using `setInterval`
- Use a third-party service, such as twilio-chat or firebase.
- Use a third-party service, such as [Pubnub](https://www.pubnub.com)
- To use a managed database service provider, there are a variety of managed database service providers available.

# Adoption strategy [newbie]
- Team members should learn about redis, the pub-sub pattern, and how to handle sticky sessions with socket-io.

# How we teach this [newbie]
- The use of these libraries requires knowledge of how websockets work and how the implementation of websockets are suitable for the chat system. It also requires reading the documentation for handling methods of this library.

# Unresolved questions
- Websocket events could in order to fit with order RFCs proposals.
- The data structure could change to fit with any database requirement proposed in other RFCs.
- Relationship of websocket connection to external booking system notification system.
- What is the stipulated number of active users, or monthly requests, since it is understood that in order to use an external managed database service you need to foresee the above in order to choose a plan accordingly.
- We don't know how we are going to calculate the average response time of a user.
