---
id: doc5
title: Create Auth Controller
---

1. Create folder "/controllers"

2. Create file /controllers/auth.js

3. Past code into /controllers/auth.js
```
module.exports.login = function(req, res) {
    res.status(200).json({
        login: true
    })
}
```

4. Change file /routes/auth.js
```
const express = require('express')
const controller = require('../controllers/auth')
const router = express.Router()

router.get('/login', controller.login)

module.exports = router
```

5. Change file /controllers/auth.js
```
module.exports.login = function(req, res) {
    res.status(200).json({
        login: 'from controller'
    })
}
```

6. Add register method in file /controllers/auth.js
```
module.exports.login = function(req, res) {
    res.status(200).json({
        login: 'from controller'
    })
}

module.exports.register = function(req, res) {
    res.status(200).json({
        register: 'from controller'
    })
}
```

7. Add register route in file /routes/auth.js
```
const express = require('express')
const controller = require('../controllers/auth')
const router = express.Router()

router.get('/login', controller.login)
router.get('/register', controller.register)

module.exports = router
```

8. Start server in terminal
```
npm run server
```

9. Check address **[http://localhost:5000/api/auth/login](http://localhost:5000/api/auth/login)** in browser