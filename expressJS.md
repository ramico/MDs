# Express.js

> **Note**  
> the poor setup comes from the tutorial  
> since your on *ramico/express* branch go to the express folder

## learning curve

### Handle requests

* Using `http.createServer` from `http` you need to branch request URL
  for each and every resource as follows

    ``` javascript
    switch(req.url){
        case '/': // homepage
            res.writeHead(200, {'content-type':'mime-type'});
            res.end(/*something*/);
            break;
        default: // 404
    }
    ```

* Using *express.js*

    ``` javascript
    const express = require('express');
    const app = express(); // or const app = require('express')(); Executing return type
    // app has all types of method submits GET, POST, PUT, and DELETE
    app.get('/', (req, res) => {
    res.status(200).send(/*something*/);
    });

    app.all('*', (req, res) => {
        res.status(404).send('<h1> Page not found </h1>');
    });
    ```

    <dl>
        <dt> Router vars </dt>
        <dd> Those vars attached with backslash separator e.g /api/items/<b>id</b></dd>
        <dt> QueryString </dt>
        <dd> vars which are submitted as /q?a=1&b=2</dd>
    </dl>

    #### app methods

    Method | Description
    --- | ---
    `use(query?:string, ...Function)` | Middleware
    `all(route:string, callback)` | handles all request types used as shown above
    `listen(port:number, callback)` | you should listen and may log the callback

    ##### `req, res` members in **express.js**

    * res

        Member | Description
        --- | ---
        `status(:number):res` | HTTP status
        `send(:any)` | Send a response
        `sendFile(:string)` | sends a file with abs path {*path.resolve*} generating content-type
        `json(:abj)` | Send a json response
    
    * req

        Member | Description
        --- | ---
        `params` | An object for router params
        `query` | An object for query string
        `body` | json that contains posted data

### Static

* express.js

    ``` javascript
    // setup static and middleware
    // note page index page should be called 'index.html'
    app.use(express.static('./public'));
    ```

* To overcome this: `npm i serve-static`

    ``` javascript
    const express = require('express');
    const app = express();
    const serveStatic = require('serve-static');
    app.use(serveStatic('./public', { index: ['index.html', 'index.htm'] }));
    ```

### something about arrays **...** operator

> used in functions as ParamArrays.  
> used to insert container elements as a copy rather than a reference  
> **if elements where objects *references are copied***  
>  
> **functions find and filter**  
> `find((e)=> /* condition */ )` // get the element matching the condition  
> `filter((e)=> /* condition */ )` // get the element(s) that matching the condition

### Middleware

A set of function(s) bounded to queried routs 

#### query ways

1. Adding middleware to selective routes 
1. Inserting `app.use()` between routs

> **Note**: the insertion ways are *procedural*  
> **syntax** e.g: `app.use('/api/?(wordA/)wordB', [fn1(...param?), fn2])`

#### middleware function prototype

`funcRef(req, res, next)` you may either

* End the route here *by branching for instance* 
* Call next function to execute the next route

### morgan 

install it with `npm i morgan`

> This is a middleware that logs information to console check it's **[documentation](https://www.npmjs.com/package/morgan)**

### HTTP request methods middleware related

Posting data

Middleware | Usage | Mime/type
--- | --- | ---
`express.json()` | javascript | application/json
`express.urlencoded({extended:false})` | form | application/x-www-form-urlencoded

### Router 

Is a way to build hierarchy for routs in a web application  

Steps:

1. move similar routing functions to router/aRoute.js 
1. delete similar route portion of each route your rout stats with /
1. export the file and import it in your app 
1. use the selective rout `app.use('./api/people/', X})` were X is the imported module reference 
1. create controller folder and place same file name for convenience 
1. move the callbacks into declared function references in the controller 
1. export and import what's needed 

#### router snippets e.g 

* router file e.g

    ``` javascript
    const router = require('express').Router();
    const {fn1,fn2} = require('../controller/aController');

    // either 
    router.get('/',fn1)
    router.post('/',fn2)
    router.delete('/',fn2)
    // or
    router.rout('/').get(fn1).post(fn1); // ... watch what you want to do 
    ```
* controller file 

    ``` javascript
    const fn1 = (req,res) => {
        // ...
    }

    module.exports = fn1
    ```

> **bottom line**  
> a controller is just middleware between routs and views 
