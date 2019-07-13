---
id: doc10
title: Connect with MongoDB
---

1. Import Mongoose in file app.js
```
const mongoose = require('mongoose')
```

2. Use connect
```
mongoose.connect('')
    .then(() => console.log('MongoDB connected.'))
    .catch(error => console.log(error))
```

3. Create folder /config

4. Create file /config/keys.js and past this code:
```
module.exports = {
    mongoURI: 'mongodb://localhost:27017/fullstack'
}
```

5. Import keys in file app.js and use it
```
const keys = require('./config/keys')

mongoose.connect(keys.mongoURI, { useNewUrlParser: true })
    .then(() => console.log('MongoDB connected.'))
    .catch(error => console.log(error))
```

6. Run MongoDB in console
```
mongod
```

7. Run server
```
npm run server
```