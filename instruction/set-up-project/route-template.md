## Step 4.0

Making the route - controller template for operation

- Go to `index.js` using sendReponse and AppError

```javascript
---
to: routes/index.js
inject: true
at_line: 0
---
const { sendResponse, AppError}=require("../helpers/utils.js")

```

## Step 4.1

Adding the route and controller

```javascript
---
to: routes/index.js
inject: true
before: module.exports
---
router.get("/foo/:test", async(req,res,next)=>{
    const { test } = req.params
    try{
        //turn on to test error handling
        if(test==="error"){
        throw new AppError(401,"Access denied","Authentication Error")
        }else{
        sendResponse(res,200,true,{data:"foo"},null,"template success")
        }
    }catch(err){
        next(err)
    }
})

```
