# mongoose-service

> Model based wrapper for Mongoose

## Installation

```sh
npm install mongoose-service
```

## Usage

```js
const mongoose = require("mongoose");
const MongooseService = require("mongoose-service");

const schema = new mongoose.Schema({
  /* schema definition */
});
const schemaModel = mongoose.model("MySchema", schema);
const schemaService = new MongooseService(schemaModel);
```

### MongooseService(schemaModel)

**Parameters**

- `schemaModel` {mongoose.model} - Mongoose Model

**Common Options where applicable**

- `find` {Object} - Filter object for Mongoose
- `select` {String | Object} - Projection
- `sort` {Object} - Mongoose Sort Object
- `skip` {Number} - Documents to skip
- `limit` {Number} - Limit number of documents to receive
- `populate` {String | Object} - Only if specified or default `page`/`offset` values were used

### Examples

#### Create a document

```js
await schemaService.create({ name: "Joyy", age: 25, city: "ST" });
```

#### Get a single document

```js
await schemaService.get({ find: { name: "Joyy", select: "name" } });
```

#### List all documents

```js
await schemaService.list({ find: { age: { $gt: 20 } }, select: "name", limit: 10 });
```

#### Update document (many or one at once)

```js
// update single record
await schemaService.update({ name: "Joyy" }, { $set: "Maulik" });

// update many at once
const updateMany = true;
await schemaService.update(
  {
    city: "ST",
  },
  {
    $set: "Surat",
  },
  updateMany
);
```