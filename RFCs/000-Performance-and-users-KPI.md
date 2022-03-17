- Start Date: 2022-03-03
- Members: Raúl Fernando Ruiz Ruiz @raulfruiz Jackson León @jackdanieldev
- RFC PR: 

# Summary

The RFC's aim is to gather data to analyze how well is the website performing in terms of users, bookings, profit and ratings given by users.

Another aim is to allow users, visitors and hosts, to see main statistics about the another user that maybe interested in closing a deal.

Further details about what kind of metrics should be displayed are given below.

# Basic example


# Motivation

"What is not meassured can't be improved"

Taking this quote as starting point and taking into account that data-driven
culture offers a big chance to enhance processes and profits in a company, the
data monitoring team wants to take care of some metrics that will give a detailed
view about the website performance and allow a better understanding of the user behaviour in order to make better choices that will make the business grow.

What is expected after implementing this feature is a higher chance of
success when booking a place as each user will know the other part is a 
reliable person.

# Detailed design

Taking into account the motivations given, what we propose is to meassure the following KPI:

1. Number of registered users
2. Number of accountless users navigating through the website
3. Number of acommodations
4. Number of active bookings
5. Historical bookings through time
6. Historical cancelled bookings
7. Geographical analysis where bookings are made
8. Profit charts with filters per day, month and year
9. List of best-rated amenities according to general rate given to the acommodation
10. Rate charts per acommodation for the host

For data gathering and statistic analysis the proposed tool is:
## Google Analytics

To get charts and insights from data, the selected tool is:
## Google Data Studio

These tools are some of the most complete and well-known available in the field. The idea is to use the features is offers to gather and collect the data required from the website traffic to analyze it later, create charts and get insights that lead to choices and strategies that will benefit the project.


# Drawbacks

Why should we *not* do this? Please consider:

- Availability of other free options such as frameworks or libraries intended to do so
- Usage of a third party tool that may concern user's data privacy


# Alternatives

Alternatives to data analysis:
* Streamlit (Python library): Open source, well documented and beginner-friendly

Alternatives to data visualization:
* Power BI: Widely used in industry.

# Adoption strategy


As Google Analytics is a free, ready-to-use tool intended to analyze a website 
traffic, its implementation shouldn't be a major challenge, neither its
mainteinance or integration when other C9 teams may require our performance
metrics.

The same thing happens with Google Data Studio when it comes to charts and getting insights from data visualization.


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
