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
