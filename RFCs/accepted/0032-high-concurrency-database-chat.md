- Start Date: (2022-02-22)
- Members: (Neisser Villa, Nahomi Conde)
- RFC PR: (leave this empty)

# Summary
Implementation of MongoDB as the best database for handling high concurrency requests in the messaging system, considering the current budget, squad's previous knowledge and learning curve.

# Motivation
We need to choose the right database to build a messaging system to support massive requests for CRUD operations simultaneously in short times.
We need to create a messaging system that allows CRUD operations from massive users simulataneously in short times. For that reason, a database that can handle high concurrency is needed. Although there will be a low demand at the begginning, this system should be able to scale when the demand increases. 

The use cases that we would have may be: 
* Thousand of users sending messages simultaneously without any crash.
* Thousands of operations per seconds without bottlenecks slowing down the system speed.

We hope that the application of this database will be very helpful in building a system that will allow scaling in the future.

# Detailed design
## Why MongoDB?
We recommend MongoDB because it ensure consistency using locking and concurrency control to prevent clients from modifying the same data simultaneously. Writes to a single document occur either in full or not at all, and clients always see consistent data.
The MongoDB server currently uses a thread per connection plus a number of internal threads.

So, if you have 8 incoming requests, each of those will be handled by a separate connection thread. Your O/S will manage concurrent execution (distributing threads across available CPU cores). Individual operations (for example, a query or index build) will generally run on a single thread. Internal operations such as syncing changes to disk may take advantage of parallel threads if appropriate.

In general, multithreading enables higher concurrency for multiple operations on a deployment rather than enabling a single operation to dominate all available resources. Long running read and write operations will also yield to allow other operations to interleave. [MongoDB. Concurrency](https://docs.mongodb.com/manual/faq/concurrency/)

## How much it cost?
[Mongo atlas](https://www.mongodb.com/pricing) provide a free tier that allow create database servers for learning and exploring MongoDB in a sandbox environment. This will be very usefull for our project considering the following features:

* 512MB to 5GB of storage
* Shared RAM
* Upgrade to dedicated clusters for full functionality
* No credit card required to start
## Where we host it?
The database will be hosted in [Mongo Atlas](https://www.mongodb.com/atlas/database). Each database will be created automatically in a shared cluster located in Ohio.

## recommended schema
Before implementing the logic, we recommend the following shema for the chat collection:
```
{
  customerId: ObjectId, // User that want to book an apartement
  hostId: ObjectId, // Apartment owner
  bookingId: ObjectId, // Housing post
  messages: [{
      messageId: ObjectId,
      message: string,
      remitentId: ObjectId,
      seen: [{
          userId: ObjectId,
          seenAt: Timespam // seen date
      }],
      createdAt: Timespam // message creation date
  }],
  createdAt: Timespam, // chat creation date
  updatedAt: Timespam // Last update
}
```
## Implementation example
This is a basic implementation for mongoDB using mongoose framework.

Mongoose installation
```
npm i mongoose o yarn add mongoose
```
Mongoose configuration
```
// lib/database.js
const mongoose = require('mongoose');
mongoose.Promise = global.Promise

async function connect(uri) {
    const options = {
        useNewUrlParser: true,
        useUnifiedTopology: true
    }
    await mongoose.connect(uri, options).then(
        () => {
            console.log("[database] connected to mongoDB")
        },
        (err) => {
            console.error(err)
        }
    )
}

module.exports = connect
```
Schema configuration for chat
```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const chatCollection = new Schema({

    customerId: [{ type : mongoose.ObjectId, required: true, ref: 'users' }],
    hostId: [{ type : mongoose.ObjectId, required: true, ref: 'users' }],
    bookingId: [{ type : mongoose.ObjectId, required: true, ref: 'users' }],
    messages: [{
            messageId: { type: mongoose.ObjectId, required: true },
            message: { type: String, lowercase: true, trim: true },
            remitent: { type : mongoose.ObjectId, required: true, ref: 'users' },
            seen: [{ 
                userId: {type : mongoose.ObjectId, required: true, ref: 'users'},
                seen: { type: Date, default: Date.now }
            }],
            createdAt: { type: Date, default: Date.now }
        }],
    createdAt: { type: Date, default: Date.now },
    updatedAt: { type: Date, default: Date.now }
});

const chatModel = mongoose.model('chats', chatCollection)

module.exports = {
    chatModel
}

```
# Drawbacks
Why should we *not* do this? Please consider:

- Schemaless is a concept interpreted as lack of structure and storage control although, this versatility favors in agile development environments, do not standardize keys within the documents of a collection may involve unexpected behaviors in the application, therefore a base structure should be defined in their documents together with a strategy to control the changes that are made on them.
- Atlas server have certain restrictions in its free tier, which can be a problem at the point where there are many active users in the application.
- MongoDB has matured, and so have the resources for learning how to use the database. The docs, mailing lists and user forums are all at least three years old and are available in a number of languages. Additionally, there are community developed resources for getting started, including the Little MongoDB book. Mongo DB allows you to query and manipulate data in JSON format, therefore see all the data of an ej: user would be a very simple query.

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives
Other interesting alteratives in the market may be the next ones: 
1. [Redis](https://redis.io/documentation)
2. [Firebase](https://firebase.google.com/docs?gclid=CjwKCAiA9tyQBhAIEiwA6tdCrNT2nRvZnn7DadS3dGRK3MYbon-y2_l_Kw-xWasQFEKmSLUhzUTKzRoC37gQAvD_BwE&gclsrc=aw.ds)

# Adoption strategy
In order to adop this database, we need to:
1. Create a mongo atlas account [Mongo Atlas](https://www.mongodb.com/atlas)
2. Create a new database in a shared cluster
3. Generate mongo string connection
4. [Download Robo3T](https://robomongo.org/download)
We need to create a setup file where we can conne
This is not a breaking change because wi will implement it from scratch, so it wont need a codemod.
This database must be coordinated with [mongoose](https://mongoosejs.com/docs) library, and other libraries like [joi](https://joi.dev/api/) which will allow us validate schemas.

# How we teach this
We can teach this by using the following resources:

[Curso basico de mongoDB](https://platzi.com/cursos/mongodb/)
[Documentación oficial de mongo](https://docs.mongodb.com/)
[Documentación de mongoose](https://mongoosejs.com/docs/api.html)
[Curso Node.js: 52. Introducción a MongoDB - #jonmircha](https://www.youtube.com/watch?v=c0bjIo6OaeI)
[Curso de Node.js [ #01 Fundamentos desde cero - Primeros Pasos ]](https://www.youtube.com/watch?v=mG4U9t5nWG8&list=PLPl81lqbj-4IEnmCXEJeEXPepr8gWtsl6)

# Unresolved questions
Is it better to have a chat schema with nested messages? or is better separate chat collection from messages collection?