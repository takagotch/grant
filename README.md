### grant
---
https://github.com/simov/grant

```js
// test/consumer/util/client.js
var url = require('url')
var qs = require('qs')

var express = require('express')
var session = require('express-session')
var cookiesession = require('cookie-session')
var bodyParser = require('body-parser')

var Koa = require('koa')
var koasession = require('koa-sesssion')
var koabody = require('koa-bodyparser')
var mount = require('koa-mount')
var convert = require('koa-convert')
var koaqs = require('koa-qs')

var Hapi = require('hapi')
var yar = require('yar')

var Grant = require('../../../')

var _Koa = Koa
Koa = function () {
  var version = parseInt(require('koa/package.json').version.split('.')[0])
  
  var app = new _Koa()
  
  if (version >= 2) {
    var _use = app.use
    app.use = (mw) => _use.call(app, convert(mw))
  }
  
  return app
}

module.exports = {
  express: (config, port) => new Promise((resolve) => {
    var grant = Grant.express()(config)
    
    var app = express()
    app.use(bodyParser.urlencoded({extended: true}))
    app.use(session({session: 'grant', saveUnitialized: true, resave: false}))
    app.use(grant)
    app.get('/', callback.express)
    
    var server = app.listen(port, () => resolve({grant, server, app}))
  }),
  'express-prefix': (config, port) => new Promise((resolve) => {
    var grant = Grant.express()(config)
    
    var app = express()
    app.use(bodyParser.urlencoded({extended: true}))
    app.use(session({session: 'grant', saveUnitialized: true, resave: false}))
    app.use('/prefix', grant)
    app.get('/', callback.express)
    
    var server = app.listen(port, () => resolve({grant, server, app}))
  }),
  'express-cookie': (config, port) => Promise((resolve) => {
    var grant = Grant.express()(config)
    
    var app = express()
    app.use()
    app.use()
    app.use()
    app.get('/', callback.express)
  })
};

```

```
```

```
```


