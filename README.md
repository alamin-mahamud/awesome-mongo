# Awesome MongoDB


## Features
- Document DB
- Ad hoc queries [field, range query, regular expression]
    - return specific fields of documents and also include user-defined Javascript functions.
    - return a random sample of reults of a given size.
- Indexing - fields can be indexed with both primary and secondary indices.
- Replication
    1. high availability with replica sets
    2. each replica set consists of two or more copies of the data.
    3. each replica can act in the role of primary or secondary replica.
    4. all reads and writes are done on the primary replica by default
    5. when a primary fails then election process happens.
    6. secondary can optionally serve read operations.
- Load Balancing
    - sharding [ a shard is a master with one or more slaves ]
    - user chooses a shard key
    - the shard key can be hashed to map to a shard - enabling an even data distribution.
    - MongoDB can run on multiple servers, balancing the load or duplicating data to keep the system up and running in case of hardware failure.
- File Storage
    - GridFS with load balancing and data replication features over multiple machines
    - GridFS divides a file into parts, or chunks and stores each of those chunks as a separate document.
- Aggregation [analogous to Unix Pipes]
    - aggregation pipeline [better performant for aggregation ops]
    - map-reduce function [batch processing of data and aggregation ops]
    - single-purpose aggregation
- Server side javascript execution
    - send js directly to the database to be executed.
- Capped Collections
    - fixed size collections
    - after specified size acts like circular queue
- transactions
    - ACID transactions support.
 
- Criticisms
    - security
        - default security configuration of MongoDB, allowing anyone to have full access to the dtabases, data stolen from 1000s of servers.



## _id:
```bash
_id: ObjectId(4 bytes timestamp, 3 bytes machine id, 2 bytes process id, 3 bytes incrementer)
```

## find
### where
- equality: `{<key>: <value>}`
- less than: `{<key>: {$lt: <value>}}`
- less than equals: `{<key>: {$lte: <value>}}``
- greater than: `{<key>: {$gt: <value>}}`
- greater than equals: `{<key>: {$gte: <value>}}`
- not equals: `{<key>: {$ne: <value>}}`

### and
```bash
>db.mycol.find({
	$and: [
		{key1: value1},
		{key2: value2}
	]
}).pretty()
```
### or
```bash
>db.mycol.find({
	$or: [
		{key1: value1},
		{key2: value2}
	]
}).pretty()
```
### `and` and `or`
```bash
>db.mycollection.find({
	"likes": {$gt:10},
	$or: [
		{"by": "123"},
		{"title": "456"}
	]
}).pretty()
# likes > 10 and (by=="123" or title==456)
```


## Command History
```mongo shell
>use DATABASE_NAME
>db
>show dbs
>db.movie.insert({"name": "tutorials point"})
>db.dropDatabase()
>show dbs
>use mydb
>db.dropDatabase()
>show dbs
>db.createCollection(name, options)
>use test
>db.CreateCollection("myCollection")
>show collections
>db.createCollection("mycol": {capped:true, autoIndexId:true, size:6142800, max:10000})
>db.tutorialspoint.insert({"name" : "tutorialspoint"})
>show collections
>db.getCollection('tutorialsPoint').find({})
>show dbs
>db.COLLECTION_NAME.drop()
>use mydb
>show collections
>db.COLLECTION_NAME.drop()
>db.tutorialsPoint.drop()
>db.COLLECTION_NAME.insert(document)
>db.mycol.insert({
  _id: ObjectId(123123123afdaf1312),
  title: 'MongoDB insertion',
  description: 'inserting things in mongo db is dead simple',
  by: 'tutorials point',
  url: 'http://www.mongodb.com',
  tags: ['mongodb', 'no-sql', 'replication, persistency']
  likes: 100
})
>db.getCollection('post').find({})
>db.post.insert([
   {
      title: 'MongoDB Overview', 
      description: 'MongoDB is no sql database',
      by: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 100
   },
	
   {
      title: 'NoSQL Database', 
      description: "NoSQL database doesn't have tables",
      by: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 20, 
      comments: [	
         {
            user:'user1',
            message: 'My first comment',
            dateCreated: new Date(2013,11,10,2,35),
            like: 0 
         }
      ]
   }
])
>db.getCollections('post').find({})
>db.getCollection('post').find({}).pretty()
```

## Data Types
1. string
2. integer
3. boolean
4. double
5. min/max keys
6. arrays
7. timestamp
8. object
9. null
10. symbol
11. date
12. object ID
13. binary data
14. code
15. regular expression

## mongo shell

* Without Authentication 

``` bash
# Run Local MongoDB on default Port
mongo

# Run Local MongoDB on a Non-default Port
mongo --port 28015

# use a connection string
mongo mongodb://mongodb0.example.com:28015

# Use a CLI option --host <host>:<port>
mongo --host mongodb0.example.com:28015

mongo --host mongodb0.example.com --port 28015
```

* MongoDB instance Requires Authentication

``` bash
mongo --host mongodb://alice@mongodb0.examples.com:28015/?authSource=admin
```

``` bash
mongo --username alice --password --authenticationDatabase admin --host mongodb0.examples.com --port 28015
```

* Connect to a MongoDB Replica Set

``` bash
mongo mongodb://mongodb0.example.com.local:27017,mongodb1.example.com.local:27017,mongodb2.example.com.local:27017/?replicaSet=replA
```
	- TLS/SSL Connection
	```bash
	mongo mongodb://mongodb0.example.com.local:27017,mongodb1.example.com.local:27017,mongodb2.example.com.local:27017/?replicaSet=replA&ssl=true
	```

* Working with Mongo Shell

``` bash
db // display the database you are using
use <database> // switch database
show dbs // list all dbs
db.getSiblingDB() // list databases without switching

use myNewDatabase // new database automatically created
db.myCollection.insertOne( { x: 1 } ); // automatically creating collection
```

* Format Printed Results

``` bash
db.myCollection.find().pretty()
print() // to print w/o formatting
print(tojson(<obj>)) == printjson()
```

## Connection String
* Standard Connection String Format

``` bash
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
```

* Example - connection to a replica set named test, with the following `mongod` hosts:
  1. `db1.example.net` on port `27017` and
  2. `db2.example.net` on port `2500`

``` bash
mongodb://db1.example.net:27017,db2.example.net:2500/?replicaSet=test
```

* Example - sharded cluster with the following `mongos` hosts:
  1. `r1.example.net` on poort `27017` and 
  2. `r2.example.net` on port 27018
  
  ``` bash
  mongodb://r1.example.net:27017,r2.example.net:27017/
  ```

* Example :

``` bash
mongodb+srv://server.example.com/
```

```
Record                            TTL   Class    Priority Weight Port  Target
_mongodb._tcp.server.example.com. 86400 IN SRV   0        5      27317 mongodb1.example.com.
_mongodb._tcp.server.example.com. 86400 IN SRV   0        5      27017 mongodb2.example.com.
```

``` bash
mongodb://mongodb1.example.com:27317,mongodb2.example.com:27017/?replicaSet=mySet&authSource=authDB
```

``` bash
mongodb+srv://server.example.com/?connectTimeoutMS=300000&authSource=aDifferentAuthDB
```

* More Examples
  - Database Server Running Locally
  
  ```bash
  mongodb://localhost
  ```
  - admin Database
  
  ```bash
  # The following connects and logs in to the admin database as user sysop with the password moon.
  mongodb://sysop:moon@localhost
  ```
  
  - records database
  ```bash
  mongodb://sysop:moon@localhost/records
  ```
  - Unix Domain Socket
  Use a URL Encoded Connection string when connecting to a UNIX domain socket. the following connects to a UNIX domain socket with file path `/tmp/mongodb-27017.sock`
  ```bash
  mongodb://%2Ftmp%2Fmongodb-27017.sock
  ```
  
  - Replica Set with Members on Different Machines
  ```bash
  mongodb://db1.example.net,db2.example.com/?replicaSet=test
  ```
  
  - Replica set with members of localhost - 27017, 27018, 27019
  ```bash
  mongodb://localhost,localhost:27018,localhost:27019/?replicaSet=test
  ```

*  Replica Set with Read Distribution
   - The following connects to a replica set with three members and distributes reads to the secondaries:
   
   ```bash
   mongodb://example1.com,example2.com,example3.com/?replicaSet=test&readPreference=secondary
   ```
   - The following connects to a replica set with write concern configured to wait for replication to succeed on at least two members, with a two-second timeout.
   
   ```bash
   mongodb://example1.com,example2.com,example3.com/?replicaSet=test&w=2&wtimeoutMS=2000
   ```

* Sharded Cluster

``` bash
mongodb://router1.example.com:27017,router2.example2.com:27017,router3.example3.com:27017/
```
