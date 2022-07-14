# 9.4 Apply boo route

## Step 9.4.0

Create boo api in routes

```shell
---
sh: touch routes/boo.api.js
---
```

## Step 9.4.1

```javascript
---
to: routes/boo.api.js
inject: true
at_line: 0
---
const express= require("express")
const router = express.Router()
const {createBoo, getAllBoos} = require("../controllers/boo.controllers.js")

//Read
//Create
//Update
```

## Step 9.4.2

Create endpoints for basic Read with informative route information

```javascript
---
to: routes/boo.api.js
inject: true
after: \/\/Read
---
/**
 * @route GET api/boo
 * @description get list of boos
 * @access public
 */
router.get("/",getAllBoos)
```

## Step 9.4.3

Create endpoints for basic Create with informative route information

```javascript
---
to: routes/boo.api.js
inject: true
after: \/\/Create
---
/**
 * @route POST api/boo
 * @description create a boo
 * @access public
 */
router.post("/",createBoo)

/**
 * @route PUT api/boo
 * @description update reference to a boo
 * @access public
 */
router.put("/targetName",addReference)

//export
```

## Step 9.4.4

Export the routes

```javascript
---
to: routes/boo.api.js
inject: true
after: \/\/export
---
module.exports= router
```

## Step 9.4.7

Add boo api to index routes

```javascript
---
to: routes/index.js
inject: true
before: module.exports
---

const booRouter = require("./boo.api.js")
router.use("/boo",booRouter)
```
