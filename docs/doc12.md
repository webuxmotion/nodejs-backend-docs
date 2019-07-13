---
id: doc12
title: Login method in controller
---

1. Install jsonwebtoken
```
npm i jsonwebtoken
```

2. Edit file /config/keys.js
```
module.exports = {
    mongoURI: 'mongodb://localhost:27017/fullstack',
    jwt: 'dev-jwt'
}
```

3. Require keys and jsonwebtoken to controller /controllers/auth.js
```
const jwt = require('jsonwebtoken')
const keys = require('../config/keys')
```

4. Edit method login
```
module.exports.login = async function(req, res) {
    const candidate = await User.findOne({email: req.body.email})

    if (candidate) {
      const passwordResult = bcrypt.compareSync(req.body.password, candidate.password)
      if (passwordResult) {
        const token = jwt.sign({
          email: candidate.email,
          userId: candidate._id
        }, keys.jwt, {expiresIn: 60 * 60})

        res.status(200).json({
          token: `Bearer ${token}`
        })
      } else {
        res.status(401).json({
          message: 'Password not match'
        })
      }
    } else {
      res.status(404).json({
        message: 'User not found'
      })
    }
}
```

5. Run server
```
npm run server
```

6. Send POST request using Postman

url - http://localhost:5000/api/auth/login

method - POST

Body Raw JSON (application/json):
```
{
    "email": "example@gmail.com",
    "password": "123456"
}
```

6. See response Body Pretty:
```
{
    "token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImV4YW1wbGVAZ21haWwuY29tIiwidXNlcklkIjoiNWQyNmQ3NDUwNjZjYjEwNTBjZjk5MzE5IiwiaWF0IjoxNTYyODI3ODkzLCJleHAiOjE1NjI4MzE0OTN9.uaEui22S4SKnODAuZRDJ0DRb-kwOgEHZ4JTGiUs4VJM"
}
```