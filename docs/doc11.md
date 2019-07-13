---
id: doc11
title: Register method in controller
---

1. Install bcryptjs
```
npm i bcryptjs
```

2. Require bcrypt and User model to controller /controllers/auth.js
```
const bcrypt = require('bcryptjs')
const User = require('../models/User')
```

3. Edit method register
```
module.exports.register = async function(req, res) {
  const candidate = await User.findOne({email: req.body.email})

  if (!candidate) {
    const salt = bcrypt.genSaltSync(10)
    const password = req.body.password
    const user = new User({
      email: req.body.email,
      password: bcrypt.hashSync(password, salt)
    })

    try {
      await user.save()
      res.status(201).json(user)
    } catch(e) {
      
    }

  } else {
    res.status(409).json({
      message: 'This email already used'
    })
  }
}
```

4. Run server
```
npm run server
```

5. Send POST request using Postman

url - http://localhost:5000/api/auth/register

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
    "_id": "5d26d745066cb1050cf99319",
    "email": "example@gmail.com",
    "password": "$2a$10$kks6jr.bgUHhYDzfH2FjQ.FgjeiTEigmRgbed3cG2rRT7vlAFZi6C",
    "__v": 0
}
```