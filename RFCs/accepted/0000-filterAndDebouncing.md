# Results filter system and debouncing

- Start Date: ( 2022-02-22)
- Members: ( @carlosbritto32, @Hermestech)
- RFC PR:

# Summary

In our proposal we want to create a filter system for the search bar, using axios to get API data and renderizing in a list that will show all results that match with users search, then we want to show this data.list in real time so we have to use debouncing to avoid an app crash when users are typing in the search bar field.

## Basic Example

- Filter system: for users it's common to see a list in the search bar with places when they are typing the name of the place that they want to find, so the list have to show all of places that match with the words that they type.
  when the users type any word the search bar makes a request to the API (Endpoints places) and returns all the places that match with the search.

- Debouncing: sometimes in many apps, when you type in the search bar you get your pc or phone stop responding, or app become unresponsive, usually that happens when there are event listeners attached to the search bar, like onKeyup, or onChange, then we’re asking our computer to do this 7 times for the 7 keystrokes in the word “PEREIRA”. So when we type “P” in the search bar, our computer tries to find all the places that have the letter “P” in them. And while it’s still doing that, we ask it to look for all the cities with “PE” in them. Same thing for “PER”, etc., until we’re finished typing out “PEREIRA”.
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

```js
import cities from "cities-list";
import React from "react";

const citiesArray = Object.keys(cities);

const App = () => {
  const [filteredCities, setFilteredCities] = React.useState([]);

  const doCityFilter = (filter) => {
    if (!filter) return setFilteredCities([]);

    setFilteredCities(
      citiesArray.filter((city) =>
        city.toLowerCase().includes(filter.toLowerCase())
      )
    );
  };

  return (
    <div className="container">
      <input
        type="text"
        className="px-2"
        placeholder="search here..."
        onChange={(event) => doCityFilter(event.target.value)}
      />
      <div>
        {filteredCities?.map((city, index) => (
          <p key={index}>{city}</p>
        ))}
      </div>
    </div>
  );
};

export { App };
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
