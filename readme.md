# MongoDB Tutorial

MongoDB is a NoSQL database that stores data in JSON-like documents. It is highly scalable and flexible, making it a popular choice for modern applications.


MogoDB created by 10gen it was released in 2009.


## Installation

### 1. Install MongoDB

Visit the [MongoDB Download Center](https://www.mongodb.com/try/download/community) and download the appropriate version for your operating system. Follow the installation instructions for your platform.

1. Mongodb shell.
2. Mongodb database tools.
3. Mongodb

---

### 2. Start MongoDB

Once installed, start the MongoDB server:

1. Setup it on environment path.

   - edit system environment.
   - environment variables.
   - Double click on path.
   - click new.
   - now paste : E:\mongoDb\Server\8.0\bin

2. Check whether it is intalled or not.

   1. cmd -> run mongod.
   2. cmd -> mongod --dbpath="E:\mongoDb\data"
   
      (for running server).
   3. cmd -> mongosh to run the mongodb shell

in this setup you need to keep on cmd open in running to use the server of mongodb.

3. Show dbs -> to show the databases.

(\*Always run the
 mongod --dbpath="E:\mongoDb\data"
  before using mongodb show dbs. )


or i can also use mogodb server which will automatically run server.    
---

### 1. Connect to MongoDB

```
| Task                 | Command                             |
| -------------------- | ----------------------------------- |
| Start MongoDB Server | `mongod --dbpath="E:\mongoDb\data"` |
| Open Shell           | Open new CMD and run `mongosh`      |

```

---

## 2 Basic Commands

1. Show dbs -> show database.
2. use <db_name> -> to use the database.
3. db.dropDatabase(); -> to drop database.
4. show collections. -> to show collections.
5. db.createCollection('collection_name');
6. db.collectionName.drop() -> to drop collection.

---

### 3. Creating databse

```
std> use stdData; // it create a databse of stdData name.
{ ok: 1 }
std> show dbs // here because my databse dont have any error it will not show anything here.


std> show dbs
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
std> 

std> db.createCollection('data') // this will create a data collection inside stdData. 
std> show dbs // now my dbs will start to shoe on hte list;

std> show dbs
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
stdData  8.00 KiB
std> 

agar ham collection bna bhi dete han to vo tb tk show nhi krega jb tk use koi data nhi hoga,
```

---

### 4. Show collections

```
std> show collections
std-data

* we wont see database listed in the output of the show dbs command until that database contains at least one collection data in it.
```

### create collection.

```
db.createCollection('collection_name');
```

### 5. Drop Database and collection
- collection deletion

to drop a collection inside a data base
db.collection_name.drop();
practice-mongo> db.data.drop(); it return boolean values for operations. 
true

- database 
to drop databse.
```
std> db.dropDatabase()
{ ok: 1, dropped: 'std' }
```

### 6. Crud operations

- Inserting/c

- Update/u

- delete/d

- read/r

### Inserting document in mongoDB

```

for inserting 1 object

1. db.<collection-name>.insertOne({
    field1:value1,
    field2:value2,
})

for inserting multiple objects in the documents and use array of objects for it.

db.<collection-name>.insertMany([
    {
          field1:value1,
          field2:value2,
    },
    {  
        field1:value1,
        field2:value2,

    }
])

-- insertMany includes( array of objects).

ex : 
    my-collections> db.data.insertOne({name:"rishi"}) // here if we dont have any collection we can directly create a new one on the same insert command where we want to store the data.
    {
    acknowledged: true,
    insertedId: ObjectId('68834fb49ac4ebb3e7eec4a9')
    }


    my-collections> db.data.insertMany([{name:"sud", age:12},{name:"sai", age:18},{name:"krish", age:6}])
        {
        acknowledged: true,
        insertedIds: {
            '0': ObjectId('6883513a9ac4ebb3e7eec4ab'),
            '1': ObjectId('6883513a9ac4ebb3e7eec4ac'),
            '2': ObjectId('6883513a9ac4ebb3e7eec4ad')
        }
        }
        my-collections>
       

```

### Find method() :- db.data.find()

```
   my-collections> db.data.find()
                    [
                    { _id: ObjectId('68834fb49ac4ebb3e7eec4a9'), name: 'rishi' },
                    { _id: ObjectId('6883509b9ac4ebb3e7eec4aa'), name: 'rishi1' },
                    { _id: ObjectId('6883513a9ac4ebb3e7eec4ab'), name: 'sud', age: 12 },
                    { _id: ObjectId('6883513a9ac4ebb3e7eec4ac'), name: 'sai', age: 18 },
                    { _id: ObjectId('6883513a9ac4ebb3e7eec4ad'), name: 'krish', age: 6 }
                    ]
```

### When to use quotes and when not to.

```
1. Special Characters

     If a field name contains special characters or spaces, or starts with
     a numeric digit, using quotes is necessary.

2. Reserved Words

    If a field name is a reserved keyword in MongoDB, use quotes to
    distinguish it from the reserved keyword.

```

### Ordered and unorderd Inserts


```
When executing bulk write operations, "ordered" and "unordered" determine the batch
behavior.

   1. Ordered Inserts

            Default behavior is ordered, where MongoDB stops on the first error.
            db.<collection-name>.insertMany([ doc1, doc2, ... ]);



   2. Unordered Inserts

            When executing bulk write operations with unordered flag, MongoDB continues processing
            after encountering an error.
            db.<collection-name>.insertMany([ doc1, doc2, ... ], { ordered: false });

```

### $Ordered Insert

Documents Before the wrong one will be inserted & after the one with error will not.
(mtlb agr mai koi data insert krta hun jisme collection of document hai pr kisi ek collection me koi error hai to is case me ye hoga ki jo mere wrong data se pehle ki information hogi vo successfully insert ho jaaegi pr error or uske baad wali file insert nhi hogi. )

### $Ordered = false

Documents before the one with an error will be inserted, and the documents after the one with an error
will also be inserted. Only the document with the error will not be inserted.
error wali insertion ke alava baki sare document insert ho jaenge.

to aslo insert documents after error we need to write :  { ordered: false }

ex : db.<collection-name>.insertMany([ doc1, doc2, ... ], { ordered: false });

- Example
    ```
            my-collections> db.data.insertMany([{name:"luffy", sirname:"monkey D"} ,{ _id: ObjectId('68f2511a00822de274eec4aa')}, name: 'vinod', age: 21 , {"name":"vinod", age:45, }, {name:"krishTrish",age:12 }])
        Uncaught:
        SyntaxError: Unexpected token, expected "," (1:106)

        > 1 | db.data.insertMany([{name:"luffy", sirname:"monkey D"} ,{ _id: ObjectId('68f2511a00822de274eec4aa')}, name: 'vinod', age: 21 , {"name":"vinod", age:45, }, {name:"krishTrish",age:12 }])
            |                                                                                                           ^
        2 |

        my-collections> db.data.insertMany([{name:"luffy", sirname:"monkey D"} ,{ _id: ObjectId('68f2511a00822de274eec4aa')}, {name: 'vinod', age: 21 }, {name:"shanks",age:31 }]);
        Uncaught:
        MongoBulkWriteError: E11000 duplicate key error collection: my-collections.data index: _id_ dup key: { _id: ObjectId('68f2511a00822de274eec4aa') }
        Result: BulkWriteResult {
        insertedCount: 1,
        matchedCount: 0,
        modifiedCount: 0,
        deletedCount: 0,
        upsertedCount: 0,
        upsertedIds: {},
        insertedIds: { '0': ObjectId('68f2538b00822de274eec4ac') }
        }
        Write Errors: [
        WriteError {
            err: {
            index: 1,
            code: 11000,
            errmsg: "E11000 duplicate key error collection: my-collections.data index: _id_ dup key: { _id: ObjectId('68f2511a00822de274eec4aa') }",
            errInfo: undefined,
            op: { _id: ObjectId('68f2511a00822de274eec4aa') }
            }
        }
        ]
        my-collections> db.data.insertMany([{name:"luffy", sirname:"monkey D"} ,{ _id: ObjectId('68f2511a00822de274eec4aa')}, {name: 'vinod', age: 21 }, {name:"shanks",age:31 }],{ordered:false});
        Uncaught:
        MongoBulkWriteError: E11000 duplicate key error collection: my-collections.data index: _id_ dup key: { _id: ObjectId('68f2511a00822de274eec4aa') }
        Result: BulkWriteResult {
        insertedCount: 3,
        matchedCount: 0,
        modifiedCount: 0,
        deletedCount: 0,
        upsertedCount: 0,
        upsertedIds: {},
        insertedIds: {
            '0': ObjectId('68f253b000822de274eec4af'),
            '2': ObjectId('68f253b000822de274eec4b0'),
            '3': ObjectId('68f253b000822de274eec4b1')
        }
        }
        Write Errors: [
        WriteError {
            err: {
            index: 1,
            code: 11000,
            errmsg: "E11000 duplicate key error collection: my-collections.data index: _id_ dup key: { _id: ObjectId('68f2511a00822de274eec4aa') }",
            errInfo: undefined,
            op: { _id: ObjectId('68f2511a00822de274eec4aa') }
            }
        }
        ]
    ```

---

# Case senstivity in mongodb.

```
Collections names are case sensitive.
feilds name within documents are also case sensitive.

db.Product.insertOne({name:'thapa', age:30}); // here both the products will be diffrent. not the same.
db.product.insertOne({name:'thapa', age:30});

```

# Read operations on mongoDB

1. Reading Document in MongoDB
2. Comparision Operators.
3. Logical operators.
4. Cursors in MongoDB.
5. Elements Operators.



# Finding Documents in MongoDB

find() -> db.collection_name.find({key:value})

ex: 

my-collections> db.data.find({name:'vinod'});
[
  { _id: ObjectId('68f250b100822de274eec4a9'), name: 'vinod', age: 45 },
  { _id: ObjectId('68f2511a00822de274eec4aa'), name: 'vinod', age: 45 },
  { _id: ObjectId('68f253b000822de274eec4b0'), name: 'vinod', age: 21 }
]

findOne() -> db.collection_name.find({key:value})

ex: 

my-collections> db.data.findOne({name:'vinod'});
{ _id: ObjectId('68f250b100822de274eec4a9'), name: 'vinod', age: 45 }

## Importing Mongo In json


