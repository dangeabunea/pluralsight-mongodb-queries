## Module 3 Queries

### Equality / Non Equality

1. Select all the aircraft where the model field is equal to 'Boeing 737-900'

`db.aircraft.find({model: "Boeing 737-900"})`
`db.aircraft.find({model: { $eq : "Boeing 737-900“ }})`

	
2. Select all the aircraft where the range field is 5600 

`db.aircraft.find({range: 5600})`
`db.aircraft.find({range: {$eq: 5600}})`


3. Select all the aircraft where the underMaintenance field is true

`db.aircraft.find({underMaintenance: true})`	
`db.aircraft.find({underMaintenance: {$eq: true}})`	


4. Select a single document by _id

`db.aircraft.findOne({_id: ObjectId("5e8aa971e1562c14d031a021")})`


5. Select all the aircraft where the model field is not 'Boeing 737-900'

`db.aircraft.find({range: { $neq : 5600 }})`



### Greater Than
	
1. Select all the aircraft where the capacity field is strictly greater than 200

`db.aircraft.find({capacity: { $gt : 200 }})`	

			
2. Select all the aircraft where the nextMaintenance field is greater then (after) 2020-02-20

`db.aircraft.find({nextMaintenance: { $gt : ISODate("2020-02-20") }})`	
`db.aircraft.find({nextMaintenance: { $gte : ISODate("2020-02-20T10:15:00Z") }})`

3. Select all the aircraft where the capacity field is greater or equal than 200

`db.aircraft.find({capacity: { $gte : 200 }})`



### Less Than

1. Select all the aircraft where the capacity field is strictly less than 200

`db.aircraft.find({capacity: { $lt : 200 }})`	

			
2. Select all the aircraft where the nextMaintenance field is less then (before) 2020-02-20

`db.aircraft.find({nextMaintenance: { $lt : ISODate("2020-02-20") }})`	
`db.aircraft.find({nextMaintenance: { $lte : ISODate("2020-02-20T10:15:00Z") }})`

3. Select all the aircraft where the capacity field is less than or equal to 200

`db.aircraft.find({capacity: { $lte : 200 }})`


### In / Not In

1. Select all aircraft where the model field has one of the values : 'Airbus A350', 'Boeing 747'

`db.aircraft.find({ model: { $in: ["Airbus A350“, “Boeing 747”] }})`


2. Select all the crew that have at least a skill in the array: 'engineering', 'management'

`db.crew.find({skills: { $in: ["engineering", "management"] } })`


3. Select all the aircraft where the model field matches a regular expression

`db.aircraft.find({ model: { $in: [/^A/] } })`


4. Select all aircraft where the model field is different than : 'Airbus A350', 'Boeing 747'

`db.aircraft.find({ model: { $nin: ["Airbus A350“, “Boeing 747”] }})`


5. Select all the crew that have no skill element in the array: 'engineering', 'management'

`db.crew.find({skills: { $nin: ["engineering", "management"] } })`


6. Select all the aircraft where the model field does not matche a regular expression

`db.aircraft.find({ model: { $nin: [/^A/] } })`


### Near

1. Find all the aircraft within 10 km of lon=26.2, lat=44.4

````
db.aircraft.find({position: {$near : {
	$geometry: {type: "Point", coordinates: [26.2, 44.4]}, 
	$maxDistance: 10000
	}}
}).pretty()
````


### Demo

1) Find flight by id

	`db.flights.findOne({_id: ObjectId("5e8aa95dab3db3fab191ff969f")})`

2) Flights that are delayed

	````
	db.flights.find({delayed:true}).pretty()
	db.flights.find({delayed: {$eq: true}}).pretty()
	db.flights.find({delayed: {$neq: false}}).pretty()
	````


3) Number of non-internal flights

	````
	db.flights.find({type: {$in: ["International", "Intercontinental"]}}).count()
	db.flights.find({type: {$nin: ["Internal"]}}).count()
	````

4) Flights that depart today / in specific dates

	````
	db.flights.find({departureDate: ISODate("2020-02-20T21:30:00Z")})
	db.flights.find({departureDate: {$gt: ISODate("2020-02-22")}})
	````
	
5) Flights flights shorter than 3 hours and display them in ascending order

	
	`db.flights.find({duration:{$lte: 180}}, {duration:1}).sort({duration:1})`


6) Bad weather near Paris. All flights that depart within 100 km from Paris (2.35, 48.85)

	````
	db.flights.find({"departure.location": {$near: { $geometry: {type:"Point", coordinates: [2.35,
	````
