# 9.1 - 9.2 Define boo schema & model

## Step 9.0

Create Boo.js module in models/

```shell
---
sh: touch models/Boo.js
---
```

## Step 9.1

Define schema

```javascript
---
to: models/Boo.js
---
const mongoose = require("mongoose");
//Create schema
const booSchema = mongoose.Schema(
  {
    name: { type: String, required: true },
    description: { type:String, required:true},
    referenceTo:{type: mongoose.SchemaTypes.ObjectId, ref: "Foo"} //one to one optional
  },
  {
    timestamps: true,
  }
);
//Create and export model
```

## Step 9.2

Create and export model so that this could be use across the project

```javascript
---
to: models/Boo.js
inject: true
after: export model
---
const Boo = mongoose.model("Boo", booSchema);
module.exports = Boo;
```
