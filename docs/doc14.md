---
id: doc14
title: errorHandler
---

1. Create file /utils/errorHandler.js
```
module.exports = (res, error) => {
  res.status(500).json({
    success: false,
    message: error.message ? error.message : error
  })
}
```

2. Use errorHandler in register method in /controllers/auth.js
```
const errorHandler = require('../utils/errorHandler')

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
      errorHandler(res, e)
    }

  } else {
    res.status(409).json({
      message: 'This email already used'
    })
  }
}
```