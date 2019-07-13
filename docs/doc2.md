---
id: doc2
title: Installation Express
---


1. Initialization
```
npm init
```
2. Set fields in console:

package name - press Enter

version - press Enter

description - **Some description** - press Enter

entry point - press Enter

test command - press Enter

git repository - press Enter

keywords - **express angular** - press Enter

author - **Andrii Pereverziev** - press Enter

license - press Enter

Is this ok? - press Enter

3. Create file "index.js"

4. Install express
```
npm install express
```

5. Create simple server using Express. 

5.1 Open file index.js

5.2 Past this code
```
const express = require('express')

const app = express()

app.get('/', (req, res) => {
    res.status(200).json({
        message: 'Working'
    })
})

app.listen(5000, () => console.log('Server has been started'))
```

6. Start server in terminal
```
node index.js
```

7. Check address **[http://localhost:5000/](http://localhost:5000/)** in browser