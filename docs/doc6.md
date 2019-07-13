---
id: doc6
title: Change Routes Methods
---

1. Change file /routes/auth.js
```
const express = require('express')
const controller = require('../controllers/auth')
const router = express.Router()

router.post('/login', controller.login)
router.post('/register', controller.register)

module.exports = router
```