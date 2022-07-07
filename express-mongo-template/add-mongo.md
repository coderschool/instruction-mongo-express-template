---
description: add mongo to project
---

# 1. Add Mongo to project

## Step 1.0

Add mongo uri to env

```
---
to: .env
inject: true
at_line: 0
---
MONGODB_URI="mongodb://localhost:27017/template"
```

## Step 1.1

Install mongoose library

```shell
---
sh:  npm i mongoose
---
```

## Step 1.2

Config mongoose to connect to local MongoDB

```javascript
---
to: app.js
inject: true
after: app\.use\(cors\(\)\)
---
const mongoose = require("mongoose")
/* DB connection*/
const mongoURI = process.env.MONGODB_URI;

mongoose
  .connect(mongoURI)
  .then(() => console.log(`DB connected ${mongoURI}`))
  .catch((err) => console.log(err));

```
