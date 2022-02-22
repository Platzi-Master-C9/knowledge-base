- Start Date: 2022-02-21
- Members: Yael Ramírez, Juan Alberto Solís (@juansolisctj13)
- RFC PR: (leave this empty)

# Summary

Implement an useful visualization for admin.

# Basic example

.

# Motivation

As part of data monitoring, we need to give practical information about the app performance and key parameters.This information will be displayed embedded in the app.

# Detailed design

Deliver practical data viz in accordance with the C9 team. For this purpose we are going to use libraries that can be embedded in the app. When the displayed metrics are defined we will define the respective visualization.
The options are:

- Visx: JS components library for airbnb.
- streamlit.io: Python library.
- Nivo: JS components library.

# Drawbacks

For this topic we are going to discuss about the language the library is build.

In the case of visx and nivo, both are built in JS and works with react and D3. Drawbacks for this:

- The knowledge base for this squad apparently is more suited to use Python tecnologies and could be a time to master the libraries.

In the case of Streamlit, drawbacks are:

- The app will be developed in JS and this feature is in Python.

# Alternatives

There are plenty of alternative libraries for this purpose but this 3 options were the most mentioned in the first meetings.

# Adoption strategy

The frontend teams will have to work with this d3 and react components in their views for the respective user. For a correct adoption of this feature we will have to give them not only the general purpose graph but the customized viz for the view, including the respective group of tests. 
The backend team will have to give us recommendations for embedding the viz without affecting the app performance.

# How we teach this

This feature will be named data and metrics visualization and the respective reading of the graphs will be explained in workshops. 

# Unresolved questions

Almost everything in this feature is TBD.
