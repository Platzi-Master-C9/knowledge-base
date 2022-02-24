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

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

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