## Module 2 Queries

### MongoDB Server Navigation

1. Shows all the databases present on the server

`show dbs`

	
2. Select a database to work against. After this command, all the queries will be issued against `flightmgmt`

`use flightmgmt`

3. Show the collections in the `flightmgmt` database

`show collections`	


### Queries

		
1. Counts all the documents in the flights collection

`db.flights.count()`	

			
2. Prints all the documents in the flights collection

`db.flights.find()`	


3. Prints all the documents in the flights collecion in a redable JSON format

`db.flights.find().pretty()`	


4. Prints the duration, departure.city and destination.city to the console in a redable JSON format
The _id is also going to be added by default

`db.flights.find({}, {duration: 1, "departure.city": 1, "destination.city": 1}).pretty()`


5. Prints the duration, departure.city and destination.city to the console in a redable JSON format
The _id is going to be excluded

`db.flights.find({}, {duration: 1, "departure.city": 1, "destination.city": 1, _id: 0}).pretty()`


6. Prints the first 5 documents returned by the find method to the screen in a readable JSON format

`db.flights.find({}, {duration: 1, "departure.city": 1, "destination.city": 1, _id: 0}).limit(5).pretty()`


7. Prints the flight documents in descending order by the duration field.

`db.flights.find({}, {duration: 1, "departure.city": 1, "destination.city": 1, _id: 0}).sort({"duration: -1"}).pretty()`
