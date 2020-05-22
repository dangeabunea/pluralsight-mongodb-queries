## How to import sample database

In order to import the sample database, you will need to ahve MongoDB
server installed and running. I am assuming that the MongoDB server directory
is also available on the path.

After this, you can use the mongoimport command to create the 'flightmgmt' database
with the 'aircraft' and 'flights' collections.

You can also import the 'crew' collection. It is not used in the demos, but some examples
in the slides relate to it.

The sample collections are stored in this repository, under the 'sampledb' directory.

### Example

`mongoimport --file C:\aircraft.json --collection aircraft --db flightmgmt --drop`

`mongoimport --file C:\flights.json --collection flights --db flightmgmt --drop`

`mongoimport --file C:\crew.json --collection crew --db flightmgmt --drop`

### Explanation

Let's take the first command as an example.

This will import the documents from 'C:\flights.json' in a database named
'flightmgmt', in a collection named 'flights'. All previous collections
will be dropped first, so that the data is not appended, byt recreated
from scratch.
If no db or collection exists, they will be created for you.

### Docs

https://docs.mongodb.com/manual/reference/program/mongoimport/

---
