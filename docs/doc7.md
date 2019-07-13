---
id: doc7
title: Test api using Postman
---

1. Install Postman - [https://www.getpostman.com/downloads/](https://www.getpostman.com/downloads/)

2. Install body-parser using console
```
npm install body-parser --save-dev
```

3. Use body-parser. Change file app.js
```
const express = require('express')
const bodyParser = require('body-parser')
const authRoutes = require('./routes/auth')
const app = express()

app.use(bodyParser.urlencoded({extended: true}))
app.use(bodyParser.json())

app.use('/api/auth', authRoutes)

module.exports = app
```

4. Read request params in controller. Change file /controllers/auth.js
```
module.exports.login = function(req, res) {
    res.status(200).json({
      login: {
        email: req.body.email,
        password: req.body.password 
      } 
    })
}

module.exports.register = function(req, res) {
    res.status(200).json({
        register: 'from controller'
    })
}
```

5. Open Postman

6. Set request params:

url - http://localhost:5000/api/auth/login

method - POST

Body Raw JSON (application/json):
```
{
	"email": "example@gmail.com",
	"password": "123456"
}
```

7. Click "SEND" button

8. See response Body Pretty:
```
{
	"email": "example@gmail.com",
	"password": "123456"
}
```
