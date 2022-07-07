---
description: Set up express project
---

# Express generator

## Step 0.0

Clean up directory

```shell
---
sh: rm -R server
---
```

Set up express boiler plate

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

- Edit `package.json` scripts:

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

- Add `.env` and `.gitignore`

```shell
---
sh:  echo 'node_modules/ \n .env' >.gitignore && echo 'PORT=8000' >.env
---
```

## Step 0.1

<!-- ```shell

sh: cd server
change_process_dir: ./server

---

````-->

Clean up boilerplate

- Remove `public/`

```cmd
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

- Go to `app.js` add

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

- Go to `app.js` add

```javascript
---
to: app.js
inject: true
after: public
---
app.use(cors())
```

- Go to `app.js` remove `require userRouter` line

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
