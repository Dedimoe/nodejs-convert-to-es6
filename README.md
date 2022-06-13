# nodejs-convert-to-es6
nodejs convert to es6

## 1. Before

#### index.routes.js:
```
module.exports = app => {
    const student = require('../controllers/student.controller.js');
    var router = require('express').Router();
    // create a new student
    router.post('/student', student.create);
    app.use('/api/students', router);
  };
```

#### server.js:
```
const express = require('express');
const db = require('./app/models/index');

const app = express();

app.get('/', (req, res) => {
  res.json({ message: 'Welcome to My Web Application.' });
});
require('./app/routes/index.routes')(app);
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}.`);
});
```


## 2. After convert to ES6

#### index.routes.js:
```
import express from 'express';
import student from '../controllers/student.controller.js';

export function initRoute(app) {
    // create a new student
    const router = express.Router();
    router.post('/student', student.create);
    app.use('/api/students', router);
}
```

#### server.js:
```
import express from 'express';
import db from './app/models/index';
import initRoute from './app/routes/index.routes';

const app = express();

app.get('/', (req, res) => {
  res.json({ message: 'Welcome to My Web Application.' });
});

initRoute(app);

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}.`);
});
```

