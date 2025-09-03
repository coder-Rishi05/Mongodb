
### mongodb server

- After running server and closing server of mongoDB

here as soon as i will run the server my db.js will also setup the mongoDB server.
when i open my server of mongoDB : it will say connect to server
when i close my server of mongoDB : it will say Mongodb Disconnected.


### models or schema 

- model is like  a blueprint for our database.
- Its a representation of  a specific collection in MongoDB like a person
- once we defined a model you can create read update and delete doc in the mongoDB collection.
- mongoose allows you to define a schema for you document. A schema is structure of you databse.

ex :

Person Schema : 
```

const mongoose = require("mongoose");

// creating/setup the schema/models.

const personSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true, // mandatory field.
  },
  age: {
    type: Number,
    required: true,
  },
  mobile: {
    type: String,
    required: true,
  },
  work: {
    type: String,
    enum: ["chef", "waiter", "manager"], // for multiple values.
    required: true,
  },
  email: {
    type: String,
    required: true,
    unique: true, // every time it will accept unique id only.
  },
  address: {
    type: String,
    required: true,
  },
  salary: {
    type: Number,
    required: true,
  },
});


// creating person model.

const Person = mongoose.model('Person', personSchema);

module.exports = Person;


```
