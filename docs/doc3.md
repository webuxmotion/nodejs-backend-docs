---
id: doc3
title: Install Nodemon and refactor app
---
1. Install nodemon
```
npm install nodemon --save-dev
```
2. Create file app.js and past this code:
```
const express = require('express')
const app = express()

module.exports = app
```
3. Change file index.js
```
const app = require('./app')
const port = process.env.PORT || 5000

app.listen(port, () => console.log(`Server has been started on ${port}`))
```
4. Set "scripts" option in file package.json
```
...
"scripts": {
    "start": "node index",
    "server": "nodemon index",
    "test": "echo \"Error: no test specified\" && exit 1"
},
...
```
5. Start server in terminal
```
npm run server
```

6. Check address **[http://localhost:5000/](http://localhost:5000/)** in browser