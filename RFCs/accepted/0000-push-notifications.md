- Start Date: 2022-02-23
- Members: Luis Gama - Brandon Verdeja 
- RFC PR: 

# Summary

Investigate strategies and tools to implement push notifications in the booking system proyect such as: 
* Long polling
* Short polling
* Sockets
* Server sent event (SSE)

Also consider if the notifications must be sent in real time and if they should have security measures.

# Basic example

In this case we plan to use WebSockets to send notifications to the clients.
[Documentation](https://developer.mozilla.org/es/docs/Web/API/WebSocket), [Configuration](https://admantium.medium.com/javascript-how-to-implement-a-websocket-backend-784ac8a56dac)

```js
// Create WebSocket connection.
//*  connect.js (Frontend) *//
import io from 'socket.io-client'
export default io(API, { cookie: false })

import websocket from './globals/connect.js'
function init () {
  websocket.emit('system:healthcheck', 'ok?')
  websocket.on('system:healthcheck', msg => {
    console.log(msg)
  })
}
init()

import websocket from '../globals/connect.js'
export default class SearchApiAction extends Action {
  action (cb) {
    websocket.emit('app:api-search-action', 'dummy')
    websocket.on('app:api-search-action', json => {
      cb(json)
    })
  }
}
```	

```js
/* Server example */

//*  index.js *//
const express = require('express')
const websocketConnection = require('./connect.js')
app = express()
const httpServer = app.listen(3000, () => {
  console.log(`BOOTING | api-blaze-backend v0.0.1`)
})
websocketConnection(httpServer)

//*  connect.js *//
const websocket = require('socket.io')
const handleConnection = require('./handler.js')
function websocketConnection (httpServer) {
  const io = websocket(httpServer, {
    serveClient: false
  })
  io.on('connection', socket => handleConnection(socket))
}
module.exports = websocketConnection

//*  handler.js *//
const { apiSearchAction } = require('./actions')
const clients = {}
function handleConnection (socket) {
  console.log(`+ client ${socket.id} has connected`)
  clients[socket.id] = { connected: true }
  socket.on('system:healthcheck', msg => {
    console.log(msg)
    socket.emit('system:healthcheck', 'healthy')
  })
  socket.on('app:api-search-action', keyword => {
    console.log('app:api-search-action', keyword)
    socket.emit('app:api-search-action', apiSearchAction(keyword))
  })
}
module.exports = handleConnection

//*  action.js *//
const apiInventory = require('./spec/inventory.json')
function apiSearchAction (keyword) {
  const regex = new RegExp(keyword, 'ig')
  var res = []
  for (let [name, definition] of Object.entries(apiInventory)) {
    const occurences = JSON.stringify(definition).match(regex)
    const score = (occurences && occurences.length) || 0
    res.push({ name, score, definition })
  }
  return res.sort((a, b) => b.score - a.score)
}
```

# Motivation

Why are we doing this? Because we want to be able to send push notifications to the client to keep them updated with the status of the booking or any other importat event.

What use cases does it support? When the user is in the booking system and the booking is confirmed, or if the booking was cancelled, or if the booking was modified, the something related to the payment, etc. 

What is the expected outcome? The client will receive a notification with that information.

# Detailed design
### In progress...
Model C4 Placement Diagram

![C4 Model Places](https://raw.githubusercontent.com/BrandonArgel/knowledge-base/main/c4-notificationsTeam.png)

To implement this tool, we need the user to have an active login, later the implementation of the notifications will be done automatically depending on what the user is looking for and what is of interest to them.

I think that in order to carry out the project we can use Web Sockets although.

# Drawbacks

### **Why should we not do this?**

- **Implementation cost, both in term of code size and complexity:** With web sockets we can have a lot of clients connected to the server and we can have a lot of notifications to send to the clients, since they do not consume much resources.

- **Cost of migrating existing React applications (is it a breaking change)?:** It depends on the type of implementation, we can use the native implementation of the browser or we can use a library such as [Socket.io](https://socket.io/).

**Others considerations:**
* WebSockets don’t automatically recover when connections are terminated – this is something you need to implement yourself, and is part of the reason why there are many client-side libraries in existence.
* Browsers older than 2011 aren’t able to support WebSocket connections - but this is increasingly less relevant.

# Alternatives
### **What other designs have been considered?**
- **Short polling:** It is the worst practice, because it makes a new request to the server in a certain period of time.

- **Long polling:** It is not the best practice, but this technique always has a connection with the server, listening to the changes.

- **Server sent event (SSE):** This is one of the best techniques and it's a recent technology. In comparison with web sockets, this technology is unidirectional, so the servers are just sending the new information to the client.

- **Web Sockets:** This technique is one of the best, but it is not scalable, and also it creates a bidirectional connection with the server.

### **What is the impact of not doing this?**

If we don't use this technique, we will have to implement a new logic using SSE, or long polling.

# Adoption strategy

The fact of the notifications has repercussions for some other teams of the project, I think it is essential that the front-end and the back-end work together to be able to do a good practice.

An intelligent architecture and a correct communication will help that.

# How we teach this

**What names and terminology work best for these concepts and why?** Using concepts like:
- **Client:** The client that is using the notification system.
- **Server:** The server that is sending the notification.
- **Push Notification:** The information that is sent to the client.

**How is this idea best presented? As a continuation of existing C9 projects patterns?** The idea is to create a component which will be implemented for any squad to use.

**Would the acceptance of this proposal mean the C9 documentation must be re-organized or altered? Does it change how C9 is taught to new developers at any level?** Yes, there are no existing documentation about which technologies will be used for the push notification system, so it's a must to add it the documentation. 

**How should this feature be taught to existing C9 developers?** Recommending readings, and explaining the concepts, also creating a tutorial.

# Unresolved questions

What development alternatives will be the most suitable?

Will our team be able to implement it?

How much will notifications affect other teams and parts of the project?

What we will use to make the project safe and provide a good user experience

# Feedback
___
1. **This requires a HTTP host?** Yes, it requires a HTTP host, but it could be added in the current API.
2. **To create an event listener in the front we use the same API?** Yes, we use the same API.
3. **How we will propagate the information throughout the app?** We will be using react context.
4. **How it will be consumed in the components that require it?** Using the current state in the context.
5. **How we will persist the information over the event?** Saving the information in the context, and also in the REST API.
6. **Why we need to use a login?** To have the concret user that is using the notification system.
7. **Does this use a protocol to send information?** HTTP protocol.
8. **How do we restore the connection of long polling? Do we send a token?** We can use a library, or create or own logic.
10. **Why doing requests would be something bad?** It is not bad to do requests, but if we saturate the server with a technique like short polling, it will be a problem.
11. **Why web sockets are not scalables?** Researching a little bit, they are very scalable if the server is properly configured. [Blog Post](http://goroutines.com/10m), [StackOverflow](https://stackoverflow.com/questions/47268038/websockets-and-scalability/47269221#47269221)