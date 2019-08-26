# Getting Started

Thanks for choosing `nanoexpress` as backend server

## Warning

This library does not support HTTP2!

## Install

### **Requires**: Node.js v10 or greater

### npm

```bash
npm install nanoexpress
# or
npm install nanoexpress@latest
# or
npm install nanoexpress@{VER}-beta
```

### yarn

```bash
yarn add nanoexpress
# or
yarn add nanoexpress@latest
# or
yarn add nanoexpress@{VER}-beta
```

## Let's create server

There few types of method defining, let me show you

- `app.get(req, res)`
- `app.post(req, res)`
- `app.put(req, res)`
- `app.patch(req, res)`
- `app.del(req, res)`
- `app.head(req, res)`
- `app.trace(req, res)`

Special route are

- `app.ws(req, ws)`
- `app.any(req, res)`
- `app.options(req, res)`

### [Basic](../examples/basic.js) server

```js
const nanoexpress = require('nanoexpress');

const app = nanoexpress();

app.get('/', (req, res) => {
  res.end('hello world');
});

app.listen(4000);
```

or if you want try `async` example, you can try code below

### [Async](../examples/json.js) example

```js
const nanoexpress = require('nanoexpress');

const app = nanoexpress();

app.get('/', async () => ({ hello: 'world' }));

app.listen(4000);
```

Caveats: Using `app.listen(PORT, '0.0.0.0')` is recommended for Docker, Heroku and AWS for compatibility.

## Let's use middlewares

Note: _You can use almost any [express](https://expressjs.com) middleware without issues, if you facing with issues, let me know, we will solve issue together_

### [CORS](../examples/cors.js) example

```js
const nanoexpress = require('nanoexpress');
const cors = require('cors');

const app = nanoexpress();

// This is only way to apply this plugin and related to only CORS plugin
app.options('/*', cors());

app.listen(4000);
```

### `app.use` example

```js
const nanoexpress = require('nanoexpress');

const app = nanoexpress();

app.use(async (req) => {
  req.time = Date.now();
});
// or sync variant (aka Express/Connect variant)
app.use((req, res, next) => {
  req.time = Date.now();
  next();
});

app.listen(4000);
```

### You may look to [Passport](../examples/passport.js) example

[Middlewares &raquo;](./middlewares.md)
