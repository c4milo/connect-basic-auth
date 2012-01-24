#Flexible HTTP Basic Authentication for Connect Framework.

## Why
This project came to live due to the lack of flexibility of the existent middlewares, specially 
when developing RESTful APIs.

## Features
* Easy to use
* Asynchronous
* Gives you access to the request and response objects from your authentication callback.
* Lets you send a custom response body along with the Authorization Required header. Useful for RESTful APIs.

## How to use

```javascript
var basicAuth = require('connect-basic-auth');
var express = require('express');

var app = express.createServer();
app.use(basicAuth(function(credentials, req, res, next) {
  /**
   * Credentials has the following structure: 
   * {
   *   username: 'c4milo'
   *   password: 'lepassword'
   * }
   **/
  Account.authenticate(credentials, function(error) {
    next(error);
  });


}, 'Please enter your credentials.'));

//Routes that do not require authentication go first
app.post('/accounts', function(req, res, next) {
  //Creates an Account.
});

//Lets require authentication for the rest of our routes.
app.all('*', function(req, res, next) {
  req.requireAuthorization(req, res, next);
});

app.get('/accounts/:username', function(req, res, next) {
  //Returns :username account information
});

```

## License
(The MIT License)

Copyright 2012 Camilo Aguilar. All rights reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.