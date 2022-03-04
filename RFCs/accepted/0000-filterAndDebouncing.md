# Results filter system and debouncing

- Start Date: ( 2022-02-22)
- Members: ( @carlosbritto32, @Hermestech)
- RFC PR:

# Summary

In our proposal we want to create a filter system for the search bar, using axios to get API data and renderizing in a list that will show all results that match with users search, then we want to show this data.list in real time so we have to use debouncing to avoid an app crash when users are typing in the search bar field.

## Basic Example

- Filter system: users are going to see 3 options (price, type of room, score)under the search bar, when they click on one of them, they'll see a list with options that they are able to select a range between 2 options, or type the value that they want find. the filter system has to make a request to the API and returns the data what the users are looking for in the 3 diferent options of filter.

- Debouncing: sometimes in many apps, when you type in the filter options you get your pc or phone stop responding, or app become unresponsive, usually that happens when there are event listeners attached to the search bar, like onKeyup, or onChange, then we’re asking our computer to do this 7 times for the 7 keystrokes in the word “PEREIRA”. So when we type “P” in the search bar, our computer tries to find all the places that have the letter “P” in them. And while it’s still doing that, we ask it to look for all the cities with “PE” in them. Same thing for “PER”, etc., until we’re finished typing out “PEREIRA”.
  we have to decide to delay the first process for a given amount of time to see if our user wants to type something else, so that if they do, we’ll cancel the first one and then work on the second instead, that would be debouncing.

## Motivation

we want to develop a fast and reliable app, that show what users are looking for in a very efficent and easily way.

## Detailed design

C1
![](https://github.com/carlosbritto32/RFC-FilterAndDebouncing/blob/main/img/C1.drawio.png)

C2
![](https://github.com/carlosbritto32/RFC-FilterAndDebouncing/blob/main/img/C2.PNG)

C3
![](https://github.com/carlosbritto32/RFC-FilterAndDebouncing/blob/main/img/C3.drawio.png)

# debouncing example

```js
import { useState } from "react";
export const useFunctionDebouncer = () => {
  //we need to keep the setTimeout timer in state so we can cancel it later if needed
  const [timer, setTimer] = useState(null);

  const debounce = (dbFunc, delay) => {
    if (timer) {
      clearTimeout(timer);
    }
    setTimer(setTimeout(() => dbFunc(), delay));
  };

  const cancelDebounce = () => {
    if (timer) {
      clearTimeout(timer);
    }
    setTimer(timer);
  };

  return [debounce, cancelDebounce];
};
```

Use it like this:

```js
const [debounce, cancelDebounce] = useFunctionDebouncer();
```

Pass a function to debounce and a time delay (in ms) to debounce it by like this:

```js
debounce(() => console.log("Debounce me!"), 1000);
```

That will run

```js
console.log(...) after 1 second (1000 ms)
```

What else can I do?
If you'd like to cancel the function's execution during the debounce, run

```js
cancelDebounce();
```

## Drawbacks

Bad user experience, slow search and if we don't get a good searching code we can crash our app.

## Alternatives

- we can use fetch instead of axios.
- we can use ky instead of axios.
- we can use superagent instead of axios.

## Adoption strategy

- The search bar will be in the home page, so we are going to impact the UI team.
- The search bar are going to consume an API, so we are going to impact the data base of the places and the backend team.

## How we teach this

for the filter system we have to create a function that contains array methods(filter, map) to show the data that users are searching for.
for debouncig we have to use a react hook (useEffect) with a delay to avoid our app to renderize all the change or keyup events, that delay will give time to users to type what are they searching for without renderizing all the events, just renderize the las change or key up event.

we have to create a good documentation to teach all C9 team our filter system and how debouncing works here.

## Unresolved questions

-how will be the consistency of the data base?
-the search has to be key sensitive?
