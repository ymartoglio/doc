NodeJS
======


Command line
------------


```bash
 # Some useful command

 # execute a script [in debug mode]
 $ node [debug] script.js

 # package install
 # install package-name in the project folder [or globall] [and save the reference in package.json]
 $ npm install [-g] package-name [--save]

```

In development env `nodemon` (`npm i -g nodemon`) can be used to reload node processus when sources change.

Node debug
----------
https://nodejs.org/api/console.html


console.trace() display params and the Stack trace


ExpressJS
=========
version 4.x API

doc : http://expressjs.com/en/api.html

Key methods
-----------

`.use([path,] fn [,fn])` allows middleware to be executed on routes access

```javascript
//create new Router instance used to manage route dispatch structure
var router = express.Router()

// Create a module for routes under /api

// server.js
var app = express();
app.use('/api',require('./api-routes.js')(express.Router()));

// api-routes.js
module.exports = function(router){
    if(router){
        // match for /api/
        router.get('/',function(req,res){
            res.status(401).json({success:1,why:"Were do you think you go ?"});
        });

        //match fore /api/auth
        router.post('/auth',function(req,res){
            res.status(401).json({success:1,why:"Were do you think you go ?"});
        });
    }
};
```

Preprocessing and Validation middleware
---------------------------------------

http://expressjs.com/fr/4x/api.html#router.param
app.param()
router.param()




Static content
--------------

```javascript
// App
var app = express();

// expose the folder 'public'
app.use(express.static(path.join(__dirname, 'public')));

/*
  |public
  |--index.html
  |--css/style.css
*/
//The files are exposed : /index.html, /css/style.css

//Expose the folder 'public' under the route '/public'
app.use(express.static('public/',path.join(__dirname, 'public')));

/*
  |public
  |--index.html
  |--css/style.css
*/
//The files are exposed : /public/index.html, /public/css/style.css

```

SubApp
------
```javascript
var subApp = express();
subApp.get('/sub',function(req,res){
    console.log("You are in an express sub app");
});

mainApp.use(subApp);

```


Mongoose
========

http://mongoosejs.com/docs/validation.html

```javascript
var userSchema = new Schema({
      phone: {
        type: String,
        validate: {
          validator: function(v) {
            return /\d{3}-\d{3}-\d{4}/.test(v);
          },
          message: '{VALUE} is not a valid phone number!'
        },
        required: [true, 'User phone number required']
      }
    });
```


Useful packages
---------------

 * `express-session` : manage session on request object
 * `connect-mongo` : session manager for mongo, supports several driver (mongojs,mongoose)
 * `body-parser` : parse body request
 * `client-sessions` : mozilla's foundation client session manager
 * `mongoose` : MongoDB Driver and much more
 * `merge` : sufficently explicit
 * `validator` : to type validation and more...
