- Start Date: 
- Members:  
--@JoseNoriegaa
--@taberoajorge
- RFC PR: 

# Summary

**c9-messaging-system-squad**

After several evaluations and research, the best way to manage a chat system is through websockets, in this RFC the implementation of the socket-IO library is proposed.


# Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

# Motivation

In this RFCs we propose the implementation of a library for the management of WebSockets in the chats system belonging to the booking system.

With the use of this library, we can:

- Maintain an open communication between the host and a user.
- Manage in the best way a chat through WebSockets to avoid the use of multiple requests between users and avoid the use of resources.

# Detailed design

Implementation of websocket and its event handling to facilitate real-time communication between a host and a user.

Use of API that implements the requests corresponding to the business logic, including the visualization and creation of records.

![](https://i.imgur.com/RLG0xqC.png)

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

###### Create chat room
This endpoint will create a new chat room. When the user creates a new chat room, the host user will receive a notification about the new convesation.

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

###### Response 201 (Created)
After creating a new chat room (if not exists) it will return registered information.

**Response Example:**
```typescript
{
 id: string | number,
 members: string[] | number[],
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
The websocket service will implement a pub-sub pattern in order to increase the scalability of the websocket service with redis.

#### Architecture
![ws-architecture](https://user-images.githubusercontent.com/28733681/156296987-265aa672-c484-4f73-aeca-77b279a3d4d8.png)

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
}
```

# Drawbacks
- This decision directly influences the existing data creation in our database.
- Socket-io requires to use a specific client library in order to work, this library will increase the bundle size of the application in around 80KB.
- Team members have not previous experience using redis with socket-io.

# Alternatives
- Use [websocket](https://github.com/theturtle32/WebSocket-Node/blob/HEAD/docs/index.md "websocket")
- Write our own websocket server using the native nodejs modules (`http` or  `net`)
- Fetch the messages in the application using `setInterval`
- Use a third-party service, such as twilio-chat or firebase.

# Adoption strategy [newbie]
- Team members should learn about redis, the pub-sub pattern, and how to handle sticky sessions with socket-io.

# How we teach this [newbie]
- The use of these libraries requires knowledge of how websockets work and how the implementation of websockets are suitable for the chat system. It also requires reading the documentation for handling methods of this library.

# Unresolved questions
- Websocket events could in order to fit with order RFCs proposals.
- The data structure could change to fit with any database requirement proposed in other RFCs.
- Relationship of websocket connection to external booking system notification system
