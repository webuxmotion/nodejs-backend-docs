---
id: doc8
title: Install Utils
---

1. Install utils
```
npm install cors morgan
```

2. Include to file app.js
```
const cors = require('cors')
const morgan = require('morgan')
```

3. Call morgan and cors in file app.js
```
app.use(morgan('dev'))
app.use(cors())
```

4. Run server
```
npm run server
```

5. Send post request in postman

6. See the terminal message like this:
```
POST /api/auth/login 200 25.959 ms - 59
```