# 9.3 Create an example controller

Here is a guide for create basic crud controllers

## STEP 9.3.0

Create boo.controllers.js module in controllers/

```shell
---
sh: touch controllers/boo.controllers.js
---
```

## STEP 9.3.1

```javascript
---
to: controllers/boo.controllers.js
---
const { sendResponse, AppError}=require("../helpers/utils.js")

const Boo = require("../models/Boo.js")

const booController={}
//Create a boo
//Get all boo
```

## STEP 9.3.2

Create boo

```javascript
---
to: controllers/boo.controllers.js
inject: true
after: \/\/Create a boo
---
booController.createBoo=async(req,res,next)=>{
    //in real project you will getting info from req
    const info = {
        name: "any",
    description: "any boo",
    referenceTo:"62cc2ac20dd407751c1e45c6"
    }
    try{
        //always remember to control your inputs
        if(!info) throw new AppError(402,"Bad Request","Create Boo Error")
        //in real project you must also check if id (referenceTo) is valid as well as if document with given id is exist before any futher process

        //mongoose query
        const created= await Boo.create(info)
        sendResponse(res,200,true,{data:created},null,"Create boo Success")
    }catch(err){
        next(err)
    }
}

```

## STEP 9.3.3

Get boos

```javascript
---
to: controllers/boo.controllers.js
inject: true
after: \/\/Get all boo
---
booController.getAllBoos=async(req,res,next)=>{
    //in real project you will getting condition from from req then construct the filter object for query
    // empty filter mean get all
    const filter = {}
    try{
        //mongoose query
        const listOfFound= await Boo.find(filter).populate("referenceTo")
        //this to query data from the reference and append to found result.

        sendResponse(res,200,true,{data:listOfFound},null,"Found list of boos success")

    }catch(err){
        next(err)
    }
}
//export
```

## STEP 9.3.4

Export the model module

```javascript
---
to: controllers/boo.controllers.js
inject: true
after: \/\/export
---
module.exports = booController
```
