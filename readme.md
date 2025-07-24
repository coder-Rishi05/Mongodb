# MongoDB Tutorial

MongoDB is a NoSQL database that stores data in JSON-like documents. It is highly scalable and flexible, making it a popular choice for modern applications.

## Installation

### 1. Install MongoDB

Visit the [MongoDB Download Center](https://www.mongodb.com/try/download/community) and download the appropriate version for your operating system. Follow the installation instructions for your platform.

1. Mongodb shell.
2. Mongodb database tools.
3. Mongodb 

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

3. Show dbs -> to show the databases.

(*Always run the mongod --dbpath="E:\mongoDb\data" before using mongodb show dbs. )
  


### 1. Connect to MongoDB


```
| Task                 | Command                             |
| -------------------- | ----------------------------------- |
| Start MongoDB Server | `mongod --dbpath="E:\mongoDb\data"` |
| Open Shell           | Open new CMD and run `mongosh`      |

```

## Basic Commands

1. Show dbs -> show database.
2. use <db_name> -> to use the database.
3. db.dropDatabase(); -> to drop database.
4. show collections. -> to show collections.
5. db.createCollection('collection_name');
6. db.collectionName.drop() -> to drop collection.

### Creating databse

```
std> db.createCollection('std-data')
{ ok: 1 }
std> show sbs

std> show dbs
admin    40.00 KiB
config  108.00 KiB
local    72.00 KiB
std       8.00 KiB
std>

```
### Show collections

```
std> show collections
std-data

```
### Drop Database.

```
std> db.dropDatabase()
{ ok: 1, dropped: 'std' }
```
