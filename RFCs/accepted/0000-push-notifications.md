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

In this case we plan to use SSE (Server-Sent Events) to send notifications to the client.
[Documentation](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)

```js
const evtSource = new EventSource("API_URL");

// Once the instance of the event source is created, we can listen to the events.
evtSource.onmessage = function(e) {
    // Do something with the event.
}

// We also should notify if there is an error.
evtSource.onerror = function(e) {
  alert("EventSource failed.");
};
```	

```js
/* Server example */
date_default_timezone_set("America/New_York");
header("Content-Type: text/event-stream\n\n");

$counter = rand(1, 10);
while (1) {
  // Every second, sent a "ping" event.

  echo "event: ping\n";
  $curDate = date(DATE_ISO8601);
  echo 'data: {"time": "' . $curDate . '"}';
  echo "\n\n";

  // Send a simple message at random intervals.

  $counter--;

  if (!$counter) {
    echo 'data: This is a message at time ' . $curDate . "\n\n";
    $counter = rand(1, 10);
  }

  ob_flush();
  flush();
  sleep(1);
}
```

# Motivation

Why are we doing this? Because we want to be able to send push notifications to the client to keep them updated with the status of the booking or any other importat event.

What use cases does it support? When the user is in the booking system and the booking is confirmed, or if the booking was cancelled, or if the booking was modified, the something related to the payment, etc. 

What is the expected outcome? The client will receive a notification with that information.

# Detailed design

Model C4 Placement Diagram

![C4 Model Places](https://raw.githubusercontent.com/BrandonArgel/knowledge-base/main/c4-notificationsTeam.png)

To implement this tool, we need the user to have an active login, later the implementation of the notifications will be done automatically depending on what the user is looking for and what is of interest to them.

I think that in order to carry out the project we can use Server sent event (SSE) although we debate among ourselves that there is a disadvantage. [Server sent event (SSE)](https://javascript.info/server-sent-events)

# Drawbacks

### **Why should we not do this?**

- **implementation cost, both in term of code size and complexity:** In code we have to implement the logic, which is not very complex, about the cost, the more customers we have, more ports we need to keep open, unless we combine with this with the polling technique, or even using a server like nginx, which handles multiple connections.
[More about this topic](https://stackoverflow.com/questions/14225501/server-sent-events-costs-at-server-side)

- **cost of migrating existing React applications (is it a breaking change?):** No, because SSE is a native technology, it works with JavaScript.

**Others considerations:**
* SSE is limited to UTF-8, and does not support binary data.
* SSE is subject to limitation with regards to the maximum number of open connections. This can be especially painful when opening various tabs as the limit is per browser and set to a very low number (6).
* SSE is mono-directional

# Alternatives
### **What other designs have been considered?**
- **Short polling:** It is the worst practice, because it makes a new request to the server in a certain period of time.

- **Long polling:** It is not the best practice, but this technique always has a connection with the server, listening to the changes.

- **Web Sockets:** This technique is one of the best, but it is not scalable, and also it creates a bidirectional connection with the server, which is not necessary whit push notifications.

- **Server sent event (SSE):** This is also one of the best and it's a recent technology. In comparison with web sockets, this technology is unidirectional, so the servers are just sending the new information to the client.

### **What is the impact of not doing this?**

If we don't use this technique, we will have to implement a new logic using web sockets, or long polling.

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
3. **How we will propagate the information throughout the app?** Using the singleton pattern desing with a library to handle the state, such as Redux, redux-saga or redux-thunk.
4. **How it will be consumed in the components that require it?** Using the current state in the redux.
5. **How we will persist the information over the event?** Saving the information in redux state.
6. **Why we need to use a login?** To have the concret user that is using the notification system.
7. **Does this use a protocol to send information?** HTTP protocol.
8. **How do we restore the connection of long polling? Do we send a token?** Yes, in case of combining long polling with SSE we will use a token.
9. **In which part of the information flow enter nginx?** Since we open the initial connection to the server.
10. **Why doing requests would be something bad?** Because it affects the performance of the server, and the client.
11. **Why web sockets are not scalables?** Because they need the connection open all the time, but is almost the same as SSE.