Link to Challenge : https://learn.freecodecamp.org/apis-and-microservices/mongodb-and-mongoose/install-and-set-up-mongoose
Required to pass challenge :
**"mongoose" should be connected to a database**
**"mongodb" dependency should be in package.json**
**"mongoose" dependency should be in package.json**

**_NOTE :_** With the help of the following code, i was able to complete some part of challenge, only part which remaining is **"mongoose" should be connected to a database**

**_Link :_** https://impossible-sale.glitch.me

_**Server.js**_

```
> 
> var express = require('express');
> var app = express();
> 
> var fs = require('fs');
> var path = require('path');
> var bodyParser = require('body-parser');
> var router = express.Router();
> const mongoose = require('mongoose');
> mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true });
> 
> var enableCORS = function(req, res, next) {
>   if (!process.env.DISABLE_XORIGIN) {
>     var allowedOrigins = ['https://marsh-glazer.gomix.me','https://narrow-plane.gomix.me', 'https://www.freecodecamp.com'];
>     var origin = req.headers.origin;
>     if(!process.env.XORIGIN_RESTRICT || allowedOrigins.indexOf(origin) > -1) {
>       console.log(req.method);
>       res.set({
>         "Access-Control-Allow-Origin" : origin,
>         "Access-Control-Allow-Methods" : "GET, POST, OPTIONS",
>         "Access-Control-Allow-Headers" : "Origin, X-Requested-With, Content-Type, Accept"
>       });
>     }
>   }
>   next();
> };
> 
> // global setting for safety timeouts to handle possible
> // wrong callbacks that will never be called
> var timeout = 10000;
> 
> app.use(bodyParser.urlencoded({extended: 'false'}));
> app.use(bodyParser.json());
> 
> app.get('/', function(req, res) {
>   res.sendFile(path.join(__dirname, 'views', 'index.html'));
> });
> 
> router.get('/file/*?', function(req, res, next) {
>   if(req.params[0] === '.env') { return next({status: 401, message: 'ACCESS DENIED'}) }
>   fs.readFile(path.join(__dirname, req.params[0]), function(err, data){
>     if(err) { return next(err) }
>     res.type('txt').send(data.toString());
>   });
> });
> 
> app.use('/_api', enableCORS, router);
> 
> var listener = app.listen(process.env.PORT || 3000 , function () {
>   console.log('Your app is listening on port ' + listener.address().port);
> });
```

_**Package.json**_

```
> {
>   "//1": "describes your app and its dependencies",
>   "//2": "https://docs.npmjs.com/files/package.json",
>   "//3": "updating this file will download and update your packages",
>   "name": "my-glitch-app",
>   "version": "0.0.1",
>   "description": "What am I about?",
>   "main": "server.js",
>   "scripts": {
>     "start": "node server.js"
>   },
>   "dependencies": {
>     "express": "^4.16.4",
>     "mongoose": "^5.4.0",
>     "mongodb": "^2.0.0"
>   },
>   "engines": {
>     "node": "8.x"
>   },
>   "repository": {
>     "url": "https://glitch.com/edit/#!/welcome-project"
>   },
>   "license": "MIT",
>   "keywords": [
>     "node",
>     "glitch",
>     "express"
>   ]
> }
```
.**_env :_**

```
SECRET=
MADE_WITH=
MONGO_URI=mongodb://XXXXXX:XXXXXX@ds237660.mlab.com:37660/firstproject
```
please help me as iv got stuck since a week or so, went through alot of other pages but no solution,
_**Thanks in Advance**_
