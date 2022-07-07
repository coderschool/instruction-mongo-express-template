---
description: Error handling
---

# 3. Add error handling

## Step 3.0

```javascript
---
to: app.js
inject: true
at_line: 0
---
const { sendResponse, AppError } =require("./helpers/utils.js")
```

## Step 3.1

Add error handling

Create a function to catch a request that do not match any previous routes. Create an error with 404 and message.

* Go to `app.js` add

```javascript
---
to: app.js
inject: true
before: module.exports
---

// catch 404 and forard to error handler
app.use((req, res, next) => {
  const err = new AppError(404,"Not Found","Bad Request");
  next(err);
});

```

Customize express error handling by using 4 args controller. This controller will be execute when ever error are throw .Error by AppError throw will have errorType and isOperational while uncaught system error throw by system will have `Internal Server Error` type.

```javascript
---
to: app.js
inject: true
before: module.exports
---




/* Initialize Error Handling */
app.use((err, req, res, next) => {
  console.log("ERROR", err);
    return sendResponse(
      res,
      err.statusCode ? err.statusCode : 500,
      false,
      null,
      { message: err.message },
      err.isOperational ? err.errorType : "Internal Server Error"
    );
});
```
