---
id: doc13
title: Private routes with Passport
---

1. Install deps
```
npm i passport passport-jwt
```

2. Require and init passport in file app.js
```
const passport = require('passport')

app.use(passport.initialize())
require('./middleware/passport')(passport)
```

3. Create file /middleware/passport.js
```
const JwtStrategy = require('passport-jwt').Strategy
const ExtractJwt = require('passport-jwt').ExtractJwt
const keys = require('../config/keys')
const mongoose = require('mongoose')
const User = mongoose.model('users')

const opts = {}

opts.jwtFromRequest = ExtractJwt.fromAuthHeaderAsBearerToken()
opts.secretOrKey = keys.jwt

module.exports = passport => {
  passport.use(
    new JwtStrategy(opts, async (payload, done) => {
      try {
        const user = await User.findById(payload.userId).select('email id')

        if (user) {
          done(null, user)
        } else {
          done(null, false)
        }
      } catch (e) {
        console.log(e)
      }
    })
  )
}
```

4. Require and use passport in /routes/auth.js for register route
```
const passport = require('passport')

router.post('/register', passport.authenticate('jwt', {session: false}), controller.register)
```

5. Run server 
```
npm run server
```

6. Send POST request with Postman

url - http://localhost:5000/api/auth/register

method - POST

Body Raw JSON (application/json):
```
{
    "email": "example@gmail.com",
    "password": "123456"
}
```

7. See response 
```
Unauthorized
```

8. Get token using POST request in Postman

url - http://localhost:5000/api/auth/login

method - POST

Body Raw JSON (application/json):
```
{
    "email": "example@gmail.com",
    "password": "123456"
}
```

9. Copy token from response, for example:
```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImV4YW1wbGVAZ21haWwuY29tIiwidXNlcklkIjoiNWQyNmQ3NDUwNjZjYjEwNTBjZjk5MzE5IiwiaWF0IjoxNTYyODMwMTk2LCJleHAiOjE1NjI4MzM3OTZ9.S6o4_zK084sJ2MpKcCpw6LDKSk4iHJ5dfyg3qtVgfSg
```

10. Add header Authorization for POST request in Postman

key: Authorization

value: **"your token"**

11. Send request in Postman

url - http://localhost:5000/api/auth/register

method - POST

Body Raw JSON (application/json):
```
{
    "email": "example@gmail.com",
    "password": "123456"
}
```

12. See response 
```
{
    "message": "This email already used"
}
```