- Start Date: 2022-02-16
- Members:
  - Emanuel Alvarado
  - Dilan Ariza
- RFC PR:
​
# Summary
​
Implementation Db to Geolocalization Squad
​
# Basic example
​
Does not apply in this case
​
# Motivation
​
Database implementation for the geolocation squad.
​
Due to the fact that there is no prior selection of the geolocation's squad database this RFC is made in order to define the database to be used.
​
PostgreSQL is proposed for the development of the squad's data storage system
​
# Detailed design
​
## Database to use
​
A prior consensus was made to choose the database. In this case PostgreSQL (SQL) database was chosen as the main option to implement as the squad's data storage system.
​
The main reasons why we decided to use PostgreSQL database are:
​
- The data model to be used is a relational model of queries. An example of the queries expected to be made are searches by country, region, city or a range of kilometers; Therefore it is assumed that the best option is a relational database (SQL).
​
- PostgreSQL creates a new process for each request or query. This process has its own memory allocated by PostgreSQL and makes its architecture, unlike Mysql (which creates threads within the main query process per connection), more feasible for business areas.
​
- PostgreSQL offers more variety of data types than MySQL. This offers more versatility when generating the data types architecture.
​
- The Knowledge and experience the team has with the database is quite a lot compared to different alternatives which could be implemented later on and could help us make faster searches.
​
- Integration with Node JS and Sequelize (ORM to Node Js) is easier and faster than native integration. This facilitates the database usage.
​
## Data diagram
​
We chose this data diagram to organize the information of each place to be saved with specific coordinates and therefore with precise data of each position.
​
This data model facilitates finding locations due to the relations made in each model (cities, countries, states and locations model).
​
[![UML-Diagram.jpg](https://i.postimg.cc/1tdhYKnS/UML-Diagram.jpg)](https://postimg.cc/XG9zrdk1)
​
## Terms used
​
- [Node JS](https://nodejs.org/) - "Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine." [source.](https://nodejs.org/en/)
​
- [Sequelize ORM](https://sequelize.org/) - "Sequelize is a promise-based Node.js ORM for Postgres, MySQL, MariaDB, SQLite and Microsoft SQL Server. It features solid transaction support, relations, eager and lazy loading, read replication and more." [source.](https://sequelize.org/)
​
# Drawbacks
​
- **The implementation cost**: although low, it has an impact on memory usage and the database server cost due to the way PostgreSQL manages processes. This happens because each query creates a new process and therefore has more resource allocation.
​
# Alternatives
​
The main alternative in this case is MySQL since we have knowledge of the database engine and also has fast integration with Sequelize. Therefore it is the best option if PostgreSQL is not integrated.
​
It's important to note that MySQL has lower server operating costs, but at the same time it has less enterprise-level process management and fewer date types to store.
​
# Adoption strategy
​
Since this is the first database design, it does not affect the current development of the "Booking System" process so the adoption by other developers is simple and the communication towards this process is carried out by API (Application Program Interface). Making this process independent of the rest of the services.
​
# How we teach this
​
For C9 developers who are currently working on the backend architecture side, learning the adoption of this architecture could come from this RFC and thus from the discussions around the topic.
​
The focus of this RFC is almost 100% Backend focused therefore the process will not affect C9 Frontend developers at all.
​
It is proposed that the Backends currently developing in C9 can rely on this RFC and on the database modeling documentation with Sequelize.
​
# Unresolved questions
​
The main undetermined issue is the use of an ORM as a database management enabler.
​
It is also unclear whether data migrations are going to be performed periodically on the system.