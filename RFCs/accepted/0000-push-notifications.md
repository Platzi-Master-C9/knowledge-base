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

In this case we plan to use SEE (Server-Sent Events) to send notifications to the client.

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

C4 Model Placement Diagram 

![C4 Model Places!](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6e636099-4162-46db-b49a-232f34ac3cf4%2Fc4-notificationsTeam.png?table=block&id=52cfaea3-b036-400f-86ef-097f0efdacef&spaceId=ed752afe-7a09-4db1-a4e5-a1660f831484&width=2000&userId=53d4127d-f1f4-401c-8082-755f4372089c&cache=v2)

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

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

If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries?

# How we teach this

**What names and terminology work best for these concepts and why?** Using concepts like:
- **Client:** The client that is using the notification system.
- **Server:** The server that is sending the notification.
- **Push Notification:** The information that is sent to the client.

**How is this idea best presented? As a continuation of existing C9 projects patterns?** The idea is to create a component which will be implemented for any squad to use.


**Would the acceptance of this proposal mean the C9 documentation must be re-organized or altered? Does it change how C9 is taught to new developers at any level?** Yes, there are no existing documentation about which technologies will be used for the push notification system, so it's a must to add it the documentation. 

**How should this feature be taught to existing C9 developers?** Recommending readings, and explaining the concepts, also creating a tutorial.

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?