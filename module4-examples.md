## Module 4 Queries

### Query Sub-Documents

1. Select all flights where departure city is Paris

`db.flights.find({"departure.city" : "Paris"}).pretty()`


2. Find all flights where the destination runway length is less than 3000

`db.flights.find({"destination.runwayLength": {$lt: 3000}})`


### Query Against Multiple Conditions

1. Select all the flights where duration is less than 2 hours AND the type is internal

`db.flights.find({$and: [{duration: {$lt: 120}}, {type: "Internal"}]}, {duration: 1, type: 1})`


2. Select all the flights where the duration is between 2 and 3 hours (short query version because the same field is targeted)

`db.flights.find({duration: {$lt: 180, $gt: 120}}, {duration: 1})`


3. Select all the flights where the depart OR land in Germany

`db.flights.find({$or: [{"departure.country": "Germany"}, {"destination.country": "Germany"}]}, {"departure.city": 1, "destination.city": 1})`


4. Find all the aircraft where the capacity is greater than 200 OR the range is less than 6000

`db.aircraft.find({ $or: [ {capacity : {$gt: 200}} , {range : {$gt : 6000}} ] })`


5. Combine AND and OR: Select all the flights where the 'minRunwayLength' is less than 3000 AND either the capacity is greater than 200 OR the range is greater than 6500

````
db.aircraft.find({ $and: [
		{ minRunwayLength: {$lte: 3000} },
		{ $or: [ {capacity: {$gt: 200}} , {range: {$gt: 6500}} ] }, 
	]
}).pretty()

````


### Edge Cases: Find by null, type or by field existence 


1. Find all the flights where the 'aircraftCode' field exists

`db.flights.find({aircraftCode: {$exists: true}}, {aircraftCode: 1})`


2. Find all the flights where the 'aircraftCode' field exists and it's type is 'string'

`db.flights.find({aircraftCode: {$exists: true, $type: "string"}}, {aircraftCode: 1})`


3. Find all the flights where the 'aircraftCode' fiels is null

`db.flights.find( {aircraftCode : null} ).pretty()`


### Free Text Search

1. Create text index on departure and destination fields
	
`db.flights.createIndex({"departure.city": "text", "destination.city": "text", "departure.country": "text", "destination.country": "text"})`


2. Find all the documents by free text 'Paris Portugal' and also print the text score (relevance)
`db.flights.find({$text: {$search: "Paris Portugal"}}, {_id:1, score: {$meta: "textScore"}}).pretty()`