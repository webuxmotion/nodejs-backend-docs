---
id: doc9
title: Create Models
---

1. Install mongoose
```
npm install mongoose
```

2. Create folder /models

3. Create model file /models/User.js

4. Past this code to file /models/User.js
```
const mongoose = require('mongoose')
const Schema = mongoose.Schema

const userSchema = new Schema({
    email: {
        type: String,
        required: true,
        unique: true
    },
    password: {
        type: String,
        required: true
    }
})

module.exports = mongoose.model('users', userSchema)
```
