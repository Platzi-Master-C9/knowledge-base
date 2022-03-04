Start Date: (2022-03-03)
Members: (Julian Restrepo Baron)
RFC PR: ()

**Summary**
Use the mockaroo to mock data, since it can generate simulated data with a lot of data types.

**Motivation**
Mock the data allows know the correct process to do at the future with the real data.
Mockaroo allows generate a dataset with many columns and 1000 entries free and exportate it to many extensions:
	* csv.
	* SQL.
	* Excel.
	* Json.
	* Cassandra CQL.

**Detailed design**
Use https://www.mockaroo.com/ to generate the follow dataset

    "host_id":   {int},
    "place_id":  {int},
    "timestamp": {int}(seconds)(fecha_creacion),
    "price":     {double},
    "latitude":  {double},
    "longitude": {double},
    "name":      {string},
    "is_active": {bool}

**Drawbacks**
Taking into account the lot of extensions we can use with mockaroo the implementation will be easy.

**Alternatives**
Faker.
Algorithm.

**Adoption strategy**
The simulate data could be in a lot of extensions so will be easy use the simulated data.

**How we teach this**
Mockaroo is really easy to use and there is enough documentation.

