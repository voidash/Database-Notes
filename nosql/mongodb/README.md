# MongoDB

- NoSQL doesn't mean the data is not structured, it just means that it uses other means to structure and store data instead of using Relational Methods.
- NoSQL database uses various methods to store data like graph relation, sparse matrix etc. MongoDB uses collection of documents to store data.
    - What are documents?
        - JSON like files with optional schemas which are actually called BSON
        - BSON is
            - ( Binary Javascript Object Notation)
            - faster to parse than JSON
            - lighter to store than JSON
            - not human readable
        - BSON can be represented as JSON
    - Has more types that JSON does
- MongoDB is document oriented database.. It stores data records as **documents** which are gathered together in **collection**
- MongoDB atlas is the service provided by MongoDB as github is a hosting service for git repositories.
- JSON
    - starts and ends with curly braces `{ }`
    - key and value is seperated with colon `:`

```json
    {
        'name': 'ashish',
        'college':'Kathmandu University',
        'courses'	: {
            'math203'	: 'Khim Bahadur Khatri',
          'DBMS101' : 'Rajani Chulyaldyo'
        }
    }
```

- Each collection can have documents with same data(same key value pairs). but will have different ID
- Each collection can also have documents with different Keys and different values and that won't be problem like relational database.
    ![](https://i.imgur.com/bDuYOve.png)

## Exporting and Importing Data

- mongoimport, mongoexport for JSON
    - `mongoimport` : import JSON files to Database
    - `mongoexport`: to download JSON files to your computer
- mongorestore, mongodump for BSON

```
mongodump --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies"

mongoexport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --collection=sales --out=sales.json

mongorestore --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies"  --drop dump

mongoimport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --drop sales.json
```

- Example URI string of MongoDB used on commands
    - `"mongodb+srv://haha.test.mongodb.net/myFirstDatabase" --username <username>`
        - Notice *srv* , which is actually a record(DNS SRV ) which speccifies a host and port for specific services such as VOIP , instant messaging etc.

## Quering MongoDB

- Each Database is organized to namespaces, which are mapped to wiredtiger files.
    
    - namespaces are simply a name for a collection or index in MongoDB. usually combination of database name and name of collection or index.
- first Install MongoDB shell ,`mongoshell` on your computer.
    
- then go to your cluster's page and click on connect button and choose mongoshell . A uri of this type will be given to you to copy and paste on your terminal.
    ![](https://i.imgur.com/R0lPkMa.png)
    
- Enter your password and you will have access to your instance
    

![](https://i.imgur.com/l9Xcp7z.png)

- To show the database present in databases, use`show dbs`
    ![](https://i.imgur.com/53c04em.png)
- `use <dbname>` : to use specific database
- `show collections`: show all the collections present on database that is being used.

`db.<collection_name>.find('<query>')`
`db.<collection_name>.find('<query>').count()`
`db.zips.find({"sole_size": 9})`

other related commands
`findOne(), insert(), update(), etc`

- Each Document in a collection will have a unique ID represented by `_id`

- Delete collection with `db.collection_name.drop()`
# Queriying with MQL ( Mongo Query Language)
- Done for Documents within a collection
- One can `find()` or `findOne()` and then chain `count()` or `pretty()`

```mql
db.collection_name.findOne("{"test": "document"}").count()
```

- `updateOne()` or `updateMany()`
    
- `deleteOne()` or `deleteMany()`
    
- To increase the price of all goldstar shoes with name `goldstart MXQ` by 12. use `$inc` operator.
    

```mql
db.shoes.updateMany({"name"goldstar MXQ"}, {"$inc": {"price": 12}})
```

- Other operators include `$inc`, `$set`: to set value to specific key, `$push` for pushing to array

- `$lte`:  <= , `$gte`: >= , `$eq`: == , `$ne`: !=,
```mql
// for all trip duration that are less than 200 
db.trips.find(
{"tripduration": {"$lte": 200}}
)


//trips that are less than 200 but greater than 40
db.trips.find({
"tripduration": {"$gte": 40, "$lte": 200}
})


```


- `$and`, `$or`, `$not` , `$nor` are available. operators with two operands require array. 

- `$expr` 
	- Expr is powerful: allows us to replace the constant value with variables from field. ie. instead of passing `12`to `greater than($gt)` we can pass some field ie. key to it.
	-  
```
	{
	"$expr": {"$eq": ["$start station id", "$end station id"]}
	}
	
	// here $ represents either a operator
	// or represents a field value. 
```

![](https://i.imgur.com/KflTgBX.png)


- `$all` returns all documents that has . 

```mql
// some examples

db.listingsAndReviews.find({"$and": [{"accommodates":{"$gt":6}},{"reviews": {"$size":50}}]}).pretty()


db.listingsAndReviews.find({"$and": [{"property_type":{"$eq": "House"}},{"amenities": {"$all": ["Changing table"]}}]}).count()
```

