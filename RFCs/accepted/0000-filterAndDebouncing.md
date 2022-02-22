# Results filter system and debouncing

- Start Date: ( 2022-02-22)
- Members: ( @carlosbritto32, @Hermestech)
- RFC PR:

# Summary

In our proposal we want to create a filter system for the search bar, using axios to get API data and renderizing in a list that will show all results that match with users search, then we want to show this data.list in real time so we have to use debouncing to avoid an app crash when users are typing in the search bar field.

## Motivation

we want to develop a fast and reliable app, that show what users are looking for in a very efficent and easily way.

## Detailed design

C1
![](https://github.com/carlosbritto32/RFC-FilterAndDebouncing/blob/main/img/C1.drawio.png)

C2
![](https://github.com/carlosbritto32/RFC-FilterAndDebouncing/blob/main/img/C2.PNG)

C3
![](https://github.com/carlosbritto32/RFC-FilterAndDebouncing/blob/main/img/C3.drawio.png)

## Metrics

Not applicable

## Drawbacks

Bad user experience, slow search and if we don't get a good searching code we can crash our app.

## Alternatives

-we can use fetch instead of axios.
-we can use ky instead of axios.
-we can use superagent instead of axios.

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
