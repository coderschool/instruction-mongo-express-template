# 5. Define schema and model

## Step 5.0

Create Foo.js module in models/

```shell
---
sh: mkdir models && touch models/Foo.js
---
```

## Step 5.1

Define schema

```javascript
---
to: models/Foo.js
---
const mongoose = require("mongoose");
//Create schema
const fooSchema = mongoose.Schema(
  {
    name: { type: String, required: true },
    flag: { type: Boolean, enum: [true, false], require: true },

  },
  {
    timestamps: true,
  }
);
//Create and export model
```

## Step 5.2

Create and export model so that this could be use across the project

```javascript
---
to: models/Foo.js
inject: true
after: export model
---
const Foo = mongoose.model("Foo", fooSchema);
module.exports = Foo;
```
