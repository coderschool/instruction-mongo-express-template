# 6. Create an example controller

Here is a guide for create basic crud controllers

## Step 6.0

Create foo.controllers.js module in controllers/

```shell
---
sh: mkdir controllers && touch controllers/foo.controllers.js
---
```

## Step 6.1

```javascript
---
to: controllers/foo.controllers.js
---
const { sendResponse, AppError}=require("../helpers/utils.js")

const Foo = require("../models/Foo.js")

const fooController={}
//Create a foo
//Get all foo
//Update a foo
//Delete foo
```

## Step 6.2

Create foo

```javascript
---
to: controllers/foo.controllers.js
inject: true
after: \/\/Create a foo
---
fooController.createFoo=async(req,res,next)=>{
    //in real project you will getting info from req
    const info = {
        name:"foo",
        flag:false
    }
    try{
        //always remember to control your inputs
        if(!info) throw new AppError(402,"Bad Request","Create Foo Error")
        //mongoose query
        const created= await Foo.create(info)
        sendResponse(res,200,true,{data:created},null,"Create Foo Success")
    }catch(err){
        next(err)
    }
}

```

## Step 6.3

Get foos

```javascript
---
to: controllers/foo.controllers.js
inject: true
after: \/\/Get all foo
---
fooController.getAllFoos=async(req,res,next)=>{
    //in real project you will getting condition from from req then construct the filter object for query
    // empty filter mean get all
    const filter = {}
    try{
        //mongoose query
        const listOfFound= await Foo.find(filter)
        sendResponse(res,200,true,{data:listOfFound},null,"Found list of foos success")
    }catch(err){
        next(err)
    }
}

```

## Step 6.4

Update a foo (by id)

```javascript
---
to: controllers/foo.controllers.js
inject: true
after: \/\/Update a foo
---
fooController.updateFooById=async(req,res,next)=>{
    //in real project you will getting id from req. For updating and deleting, it is recommended for you to use unique identifier such as _id to avoid duplication
    //you will also get updateInfo from req
    // empty target and info mean update nothing
    const targetId = null
    const updateInfo = ""

    //options allow you to modify query. e.g new true return lastest update of data
    const options = {new:true}
    try{
        //mongoose query
        const updated= await Foo.findByIdAndUpdate(targetId,updateInfo,options)

        sendResponse(res,200,true,{data:updated},null,"Update foo success")
    }catch(err){
        next(err)
    }
}

```

## Step 6.5

Delete a foo (Hard delete)

```javascript
---
to: controllers/foo.controllers.js
inject: true
after: \/\/Delete foo
---
fooController.deleteFooById=async(req,res,next)=>{
    //in real project you will getting id from req. For updating and deleting, it is recommended for you to use unique identifier such as _id to avoid duplication

    // empty target mean delete nothing
    const targetId = null
    //options allow you to modify query. e.g new true return lastest update of data
    const options = {new:true}
    try{
        //mongoose query
        const updated= await Foo.findByIdAndDelete(targetId,options)

        sendResponse(res,200,true,{data:updated},null,"Delete foo success")
    }catch(err){
        next(err)
    }
}
//export
```

## Step 6.6

Export the model module

```javascript
---
to: controllers/foo.controllers.js
inject: true
after: \/\/export
---
module.exports = fooController
```
