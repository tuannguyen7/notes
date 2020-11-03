# Notes
## API design
- URIs naming convention: 
Follow the [REST naming guide](https://restfulapi.net/resource-naming/). Also take a look at [Stormpath Beautiful RES + JSON APIs](https://www.slideshare.net/stormpath/rest-jsonapis).
- Nested objects or IDs:
    Nested objects are preferable most of the time.
	```json
		{
		"id": "24a5a823-db2a-4106-b8de-d79c7362f5eb",
		"name": "Harry Potter and the Sorcerer's Stone",
		"category": {
			"id": "bbc816ca-6654-4a9e-8c14-15ab02e75341",
			"name": "book"
		},
		"price": 19
	}
	```
	Return only a `category_id` is not ideal unless getting nested objects is hard or cause bad performance.
	```json
	{
		"id": "24a5a823-db2a-4106-b8de-d79c7362f5eb",
		"name": "Harry Potter and the Sorcerer's Stone",
		"category_id": "bbc816ca-6654-4a9e-8c14-15ab02e75341",
		"price": 19
	}
	```
	Another way is to return `id` and a `_href` which is a link to get the object.
	```json
	{
		"id": "24a5a823-db2a-4106-b8de-d79c7362f5eb",
		"name": "Harry Potter and the Sorcerer's Stone",
		"category": {
			"id": "bbc816ca-6654-4a9e-8c14-15ab02e75341",
			"_href": "../category/bbc816ca-6654-4a9e-8c14-15ab02e75341"
		},
		"price": 19
	}
	```
- Auto increment/Sequence IDs or UUIDs
Use UUIDs for primary keys but keep auto increment id as a row in DB.
## Connection pooling
- [How many connections in pool](https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing)
