---
id: doc4
title: Create Auth Routes
---

1. Create folder "/routes"

2. Create file /routes/auth.js

3. Past code into /routes/auth.js
```
const express = require('express')
const router = express.Router()

router.get('/login', (req, res) => {
    res.status(200).json({
        login: true
    })
})

module.exports = router
```

4. Change app.js
```
const express = require('express')
const authRoutes = require('./routes/auth')
const app = express()

app.use('/api/auth', authRoutes)

module.exports = app
```

5. Start server in terminal
```
npm run server
```

6. Check address **[http://localhost:5000/api/auth/login](http://localhost:5000/api/auth/login)** in browser