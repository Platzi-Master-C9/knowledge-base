- Start date: 2022/02/22
- Members: @Cristhian-Medina , @alberturo
- RFC PR:

# Summary

How to build a search services

# Basic example

Sometimes the user requires to find a specific information in the application that would be easier using a search bar, so the user normally writes a string as an entry in the bar

# Motivation

This service makes it easier to find information that the user is looking for, thus improving the user experience and reducing the time to value, as well as providing a very valuable source of data directly from the user.

# Detailed design

The design to build a search service is basicly: 
- Define the search index (way to collectin, parsing and storing data)
- Get the request to an API or the target data (fetching)
- Create a state for the search input
- Create the function that will handle our search functionality
- Binding the searchItems function to the Input field
- Passing the Input value to the searchItems Function
- Setting the searchInput state to the searchValue

web origin: t.ly/VUVJ

# Drawbacks

Depending on the way of collecting the search index is the complexity and requirements of the project.
Using in app filtering we can gain control over the search index and its content. Using an existing search library in the app can help. However, it also means that to change the search behavior, you often need to adjust the code manually or replace the search library with another one.

# Alternatives

there are 2 ways to integrating search into the app:
- Using an external search service and kontent webhooks
- Filtering content within your app

https://github.com/xantari/Kentico.Search.Api

The recommended approach is to use a dedicated external search service. It works for small and large projects and can scale as it goes. The search service holds the search index, performs search operations over the index, and returns results.

# Adoption strategy

The approval of this proposal means that we must agree with the hosting team (places and booking), to obtain the necessary information of the places to be shown in the search engine

# How we teach this


# Unresolved questions

