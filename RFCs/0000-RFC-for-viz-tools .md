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


# Drawbacks

The main drawback for this library is that the squad is mainly python-oriented, and the adoption inside the squad could take time. 
Other drawbaks related with the first one are that this libraries use react and this is also not well known by almost everyone.

# Alternatives

One of the alternatives could be some libraries in Python like Streamlit.io. 

# Adoption strategy

The frontend teams will have to work with this d3 and react components in their views for the respective user. For a correct adoption of this feature we will have to give them not only the general purpose graph but the customized viz for the view, including the respective group of tests. 
The backend team will have to give us recommendations for embedding the viz without affecting the app performance.

# How we teach this

This feature will be named data and metrics visualization and the respective reading of the graphs will be explained in workshops. 

# Unresolved questions

We need to know what metrics we are going to provide to the rest of the teams and the format they are going to 

