---
description: Set up express project
---

# 0. Generate Express App

## Step 0.0

Set up express boilerplate

```shell
---
sh: npx express-generator --no-view server
---
```

```shell
---
sh: cd server
change_process_dir: ./server
---
```

- Install dev dependencies

```shell
---
sh: npm i nodemon cors dotenv
---
```

- Edit `package.json` scripts to use nodemon:

```json
---
to: package.json
inject: true
after: start
skip_if: dev
---
,
"dev": "nodemon ./bin/www"
```

- Add `.env` and `.gitignore` . Then add `node_modules` to `.gitignore` and add `PORT=8000` to `.env`

```shell
---
sh:  echo 'node_modules/ \n .env' >.gitignore && echo 'PORT=8000' >.env
---
```

## Step 0.1

Clean up boilerplate

- Remove `public/`

```
---
sh: rm -R public/
---
```

- Remove `routes/users.js`

```shell
---
sh: rm routes/users.js
---
```

- Go to `app.js` require cors library

```javascript
---
to: app.js
inject: true
at_line: 0
---
require(
    "dotenv"
).config()
const cors= require("cors")
```

- Go to `app.js` enable cross-origin access&#x20;

```javascript
---
to: app.js
inject: true
after: public
---
app.use(cors())
```

- Go to `app.js` remove `require userRouter` line. Since we don't need it

```javascript
---
to: app.js
inject: true
remove_lines:
    from: usersRouter
    to: 1
---
```

- Go to `app.js` remove `app.use(/users)` line

```javascript
---
to: app.js
inject: true
remove_lines:
    from: /users
    to: 1
---
```

- Go to `index.js` remove `res.render` line

```javascript
---
to: routes/index.js
inject: true
remove_lines:
    from: render
    to: 1
---
```

- Then replace with

```javascript
---
to: routes/index.js
inject: true
after: function
---
res.status(200).send("Welcome to CoderSchool!")
```
