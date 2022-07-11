# 7. Create route for foos

## Step 7.0

Create foo api in routes

```shell
---
sh: touch routes/foo.api.js
---
```

## Step 7.1

```javascript
---
to: routes/foo.api.js
inject: true
at_line: 0
---
const express= require("express")
const router = express.Router()
const {createFoo, getAllFoos, updateFooById ,deleteFooById} = require("../controllers/foo.controllers.js")

//Read
//Create
//Update
//Delete
```

## Step 7.2

Create endpoints for basic Read with informative route information

```javascript
---
to: routes/foo.api.js
inject: true
after: \/\/Read
---
/**
 * @route GET api/foo
 * @description get list of foos
 * @access public
 */
router.get("/",getAllFoos)
```

## Step 7.3

Create endpoints for basic Create with informative route information

```javascript
---
to: routes/foo.api.js
inject: true
after: \/\/Create
---
/**
 * @route POST api/foo
 * @description create a foo
 * @access public
 */
router.post("/",createFoo)
```

## Step 7.4

Create endpoints for basic Update with informative route information

```javascript
---
to: routes/foo.api.js
inject: true
after: \/\/Update
---
/**
 * @route PUT api/foo
 * @description update a foo
 * @access public
 */
router.put("/:id",updateFooById )
```

## Step 7.5

Create endpoints for basic Delete with informative route information

```javascript
---
to: routes/foo.api.js
inject: true
after: \/\/Delete
---
/**
 * @route DELETE api/foo
 * @description delet a foo
 * @access public
 */
router.delete("/:id",deleteFooById)

//export
```

## Step 7.6

Export the routes

```javascript
---
to: routes/foo.api.js
inject: true
after: \/\/export
---
module.exports= router
```

## Step 7.7

Add foo api to index routes

```javascript
---
to: routes/index.js
inject: true
before: module.exports
---

const fooRouter = require("./foo.api.js")
router.use("/foo",fooRouter)
```
