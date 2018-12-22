# Awesome MongoDB
 
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
