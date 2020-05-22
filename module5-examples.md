## Module 5 Examples

### Array Query Operators

1) Find all the crew members where all the skills are either 'tehchnical' or 'sales'

`db.crew.find({ skills: {$all: ["technical", "sales"]}})`


2) Find all the crew members that have exactly 2 skills

`db.crew.find({ skills: { $size: 2} })`


3) Find all the crew members where the skill object matches multiple conditions

`db.crew.find({skills: {$elemMatch: {name: "flying", lvl: {$gt: 7}}}})`


### Array Projection Operators

1) Show first 2 elements from an array when performing queries

`db.crew.find({}, {skills: {$slice: 2})`


2) Show the first element that matches the array querying

`db.crew.find({skills: "management"}, {"skills.$":1})`


3) Only display the array elements that match a list of given conditions

`db.crew.find({}, {skills: { $elemMatch: {lvl: {$gt: 7}} } })`


### Demo Queryies


1) Flights containing at least a German crew member

`db.flights.find({"crew.nationality": "Germany"},{crew: 1}).pretty()`

`db.flights.find({"crew.nationality": "Germany"},{"crew.$": 1}).pretty()`


2) Flights that do not have a crew (size is 0)

`db.flights.find({crew: []}, {crew:1}).pretty()`

`db.flights.find({crew: {$size: 0}},{crew: 1}).pretty()`


3) Flights that do not have a captain

`db.flights.find({"crew.position": {$ne: "Captain"}}, {"crew.position": 1}).pretty()`


4) Flights where the captain has little hours of sleep (7)

`db.flights.find({crew: {$elemMatch: {position: "Captain", hoursSlept: {$gt: 6}}}}, {crew: 1}).pretty()`

`db.flights.find({crew: {$elemMatch: {position: "Captain", hoursSlept: {$gt: 6}}}}, {"crew.$": 1}).pretty()`


5) Display only the captain in the crew array when querying the flight documents

`db.flights.find({}, {crew: {$elemMatch: {position: "Captain"}}}).pretty()`

