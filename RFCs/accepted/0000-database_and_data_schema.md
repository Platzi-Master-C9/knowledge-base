- Start Date: (2022-19-02)
- Members: (Simón Torres, Josefina López, Mario Luevano)
- RFC PR: (leave this empty)

# **Summary**

Search Engine data schema and ElasticSearch implementation.

# **Motivation**

**Why are we doing this?**

- The system requires a data model to be able to search and categorize the different places efficiently.
- The Search Engine requires a fast database to find the required results

**What use cases does it support?**

- When a user searches for a place to stay, the system will be able to filter information by location, dates and number of guests

**What is the expected outcome?**

- Offer a functional and search-optimized database, this is key for our users to quickly obtain the results that fit their search.

# **Detailed design**

### Why Elasticsearch?

Elasticsearch is a distributed open source search and analysis engine for all types of data, including textual, numeric, geospatial, structured and unstructured, this makes it ideal for our project, it will allow us to have an optimized and searchable database fast and accurate.

### Ventajas de usar Elasticsearch

- **Many search options**. We have many different types of search options that will allow us to get the most out of this tool. Search types available include whole words, snippets, custom stemming searches, faceted searches, full text searches, instant and autocomplete searches.
- **Saving analysis time and higher speed**. Elasticsearch can run complex queries extremely fast. It also stores almost all the commonly used structured queries as a filter for the result set and executes them only once.
- **Elasticsearch is document-oriented.** Elasticsearch is schema-free, accepts JSON documents, and tries to detect the data structure, index the data, and make it searchable.
- **Scalability**, it is very easy to scale ElasticSearch horizontally, providing better resource management and load balancing of Elastic across multiple nodes within a single clustered server environment.
- **It is free and open source,** which is why it is supported by a large community that has allowed it to have an amazing growth and can be implemented by everyone: from small websites and companies to large corporations.

### Data modeling

```json
{
	id: BOOKING_ID,
	title: BOOKING_TITTLE,
	subtitle: BOOKING_SUBTITLE,
	description: BOOKING_DESCRIPTION,
	price: BOOKING_PRICE,
	guest: BOOKING_GUESTS,
	rooms: BOOKING_ROOMS,
	beds: BOOKING_BED,
	toilets_ BOOKING_TOILETS,
	location: {
		city: BOOKING_CITY,
		deparment: BOOKING_DEPARMENT,
		country: BOOKING_COUNTRY	
	},
	reviews: [
		{
			user: 'COMMENT_BY',
			message: TEXT,
			dateCreated: DATE 	
		},
		{
			user: 'COMMENT_BY',
			message: TEXT,
			dateCreated: DATE 	
		}
	],
	host: {
		name: TEXT,
		description: TEXT,
		registration_date: DATE,
		number_evaluations: NUMBER,
		isVerified: BOOLEAN,
		languages: [LANGUAGE1, LANGUAGE2, LANGUAGE3],
		responseRate: NUMBER,
		averageResponseTime: NUMBER, 
	},
	images: [URL_IMAGE_1, URL_IMAGE_2, URL_IMAGE_3],
	benefitsPlace: [
		{
			icon: NAME_ICON,
			title: TEXT,
			description: TEXT
		},
		{
			icon: NAME_ICON,
			title: TEXT,
			description: TEXT
		}
	],
	characteristicsPlace: [
		{
			icon: ICON_NAME,
			characteristic: TEXT
		},
		{
			icon: ICON_NAME,
			characteristic: TEXT
		},
	],
	rules: [
		{
			title: TEXT,
			rulesList: [RULE_1, RULE_2, RULE_3, RULE_4]
		},
		{
			title: TEXT,
			rulesList: [RULE_1, RULE_2, RULE_3, RULE_4]
		},
	]
}
```

# **Drawbacks**

- **Difficult to use it**. ElasticSearch is undoubtedly very powerful and a great software in its field, however using it correctly is not easy, the learning process can take time, the learning curve can be a bit steeper compared to other databases.
- **Lack of multilanguage support.** Unlike other similar solutions such as Apache Solr, ElasticSearch does not provide multilanguage support, which limits the possibility of handling requests and obtaining data in more than one language simultaneously, so if we want to do this type of query in the future in the booking system we can see ourselves limited.

# **Alternatives**

We have considered using other search-optimized databases such as Apache Solr, Ambar and Algolia, although we think that any of them would work well with the booking system, we chose ElasticSearch in the end, although it is not the easiest to manage, we think it is the most robust and scalable, in addition to having an important community as it is open source that is always helpful when developing.

# **Adoption strategy**

Follow good practices and create clear rules when doing searches.

# **How we teach this**

The learning of this technology must be through learning and using it, with courses at Platzi and self-education.