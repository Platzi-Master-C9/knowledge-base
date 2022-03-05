- Start Date: 20/02/2022
- Members: Jeniffer Cruz & Johnathan Escalona
- RFC PR: (leave this empty)

# Summary

KPIs proposal for each of the 11 work teams

# Basic example

The “KPI (Key Performance Indicator in English) or performance indicators are factors that
measure the performance and effectiveness of a strategy or set of strategies that seek
achieve business goals. So you can use KPIs to measure the performance of
areas such as digital marketing, sales, human resources or your company in general.”

For example: 
The chrun rate -or cancellation rate according to its translation into Spanish- is a metric 
that indicates the percentage of clients or subscribers who have ceased their commercial 
activity with a company in a given period of time.

The cancellation rate is used to find out what percentage of customers have unsubscribed 
from a service. For example, they have stopped contracting their web hosting plan or they 
have abandoned a membership to which they were subscribed.

[In this reading you can understand KPIs thoroughly.](https://platzi.com/clases/2314-terminos-marketing-digital/38582-que-es-kpi/"Qué es un KPI")

*Resources to learn how to assign KPIs in 10 min:*
- [Metrics and KPIs. How to establish them according to business objectives](https://platzi.com/clases/1429-lean-ux/15280-metricas-y-kpis4181/)
- [Build your KPI's and follow them. Lots of examples and application cases](https://platzi.com/clases/2635-consultoria-producto/43862-construye-tus-kpis-y-siguelos/) 

# Motivation

The key actions that are carried out under the business logic must be traceable, measurable
and transformed into an indicator that reveals immediately if the goals are being achieved.

In the Requirements and Business Logic (RBL) document of the proyect, we have alredy 10 Metrics 
and General Considerations:

**Metrics**
1. Number of registered users
2. Number of accountless users who use the features of the application.
3. Number of accommodations
4. Number of active reservations.
5. History of reservations over time.
6. History of canceled reservations.
7. Geographic analysis of where reservations are made.
8. Earnings graph with filters by day, month and year.
9. List of top-rated amenities, based on the overall rating given to the accommodation.
10. Rating chart by hosting for the host.

**General considerations:*
- All delete operations to the database must be soft delete.
- If the user is eliminated, he can create an account with the same email, if he was banned, no.
- The platform will earn 15% of the total cost of the reservation.

# Detailed design

In this proposal, we award the work teams the 10 metrics required in the RBLs and enrich them 
through new KPIs that allow each team to show that their tasks are in accordance with their goals.

|Team            | KPI (**From RBL**; *New ones*)                       |
|----------------|------------------------------------------------------|
|Geolocalization |**Geographic analysis of where reservations are made**|
|Booking         | *Number of confirmed reservations per day / total searches performed per day* \n *Number of uncompleted reservations per day / total searches performed per day*|
|Authentication  |*Authenticated users per day / total searches per day* \n *Hours of the day in which they are authenticated*
|User account    |**Number of accommodations**|
|                |*History of month day, year and time in which you make reservations*|
|                |**Number of registered users**|
|                |**Number of accountless users who use the features of the application**|
|                |*Country/province/state/region/city of tenant and landlord*|
|                |*History of month day, year and time in which you make reservations*|
|                |*Age/gender of tenant and landlord*|
|                |*Type of property for rent*|
|                |*Type of property you like to rent*|
|Notification system|*Number of daily reservation guest notifications / daily total reservations*| 
|                |*Number of daily reservation host notifications / daily total reservations*| 
|Messaging system|*Daily generated chats / daily total reservations*|
|                |*Conversations to carry out natural language treatment*|
|Places          |**List of top-rated amenities, based on the overall rating given to the accommodation**| 
|                |**Host ratings graph for the host**| 
|Data monitoring |*Recurrence of use*| 
|                |*Registration completion time*| 
|                |*Reservation completion time*| 
|                |*Churn rate: how many people cancel their account per month*| 
|Business intelligence|**Earnings graph with filters by day, month and year**| 
|Administrator panel|**Number of active reservations**| 
|                |**History of reservations over time**| 
|                |**History of canceled reservations**| 
|                |*Data that tenant client consults more*| 

# Drawbacks
We consider that the measurement and continuous reporting of data is an automatable job, 
with little or no extra cost in terms of software, but that can have an impact on:
-three hours of work to program the generation of data by equipment.
-one hour of weekly work for a person from the team who is in charge of verifying that 
the data is being generated.

On the other hand, the analysis of the data for the generation of KPIs is a job that may 
have associated costs such as software licenses, some of the programs that have been considered 
to be used are: 

-  [streamlit.io](https://streamlit.io/) 
-  [plotly](https://plotly.com/)
-  [apacheAirflow]( https://airflow.apache.org/)


# Alternatives

Not having KPIs per team can lead to losing sight of the business logic within the short 
and long term activities within the pile of tasks that each person performs from their 
workspaces.

# Adoption strategy
We believe that this proposal will be successful when each team has validated 
that the assigned KPI is designed under the business objective pursued by the 
user story of each squad. You can leave your questions and comments below, just 
copy and paste the example comment module:

# How we teach this
It is possible that the data monitoring squad supports each work team in the construction 
of the data pipelines so that their generation is as automated as possible and generates 
a low level of work between the teams. Even so, it is desirable that each team prepares 
itself so as not to stop continuously producing this data.

# Unresolved questions
1. Who will implement the data generation? Each team with data monitoring instructions? datamonitoring itself?
2. What software will BI use to build and visualize the KPIs?
3. How often will the KPIs be reported to the teams that generate the data?
4. How to make markdown not separate a column into rows but do it in the other adjacent? jiji

![KIPs champions](https://media.giphy.com/media/VHI6svvhu5xuqzyAoM/giphy.gif)
