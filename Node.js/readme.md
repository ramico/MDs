# Node.js and Express.js

Here we'll start publishing stuff  questions and improvements on regular basses

## Chapters 

Chapter notes well be added here each chapter with a reference number 

* ### 01 REPL *Simple excitable **JS** code*

    Code | Note
    ---|---
    `node` | start *REPL*
    `.exit` | close {*ctrl+c*}

* ### 02 Globals

    `__dirname`: A global var referencing current working directory name

* ### 03 Module 

    Every file is a module that can be required in different ways 

    Method | Description
    --- | ---
    `module.exports = json` | An object containing *Ref vars*
    `module.exports.var = state` | not a recommended way to state exports
    `module.exports.ref = varRef` | ref is new var ref **varRef** is already declared 

    In the working file you use `require()` to import with `'./Jsfile'` **no ext**

> if imported file has an executable code it'll run *without refVars* 

* ### 04 some libs

* OS `require('os')`

    Member | Description
    --- | ---
    `os.userInfo()` | Gets user information
    `os.upTime()` | Gets System uptime
    `os.type()` | Gets operating system's name
    `os.release()` | Gets operating system's version number
    `os.totalMem() && os.freeMem()` | Gets total and free memory

* path `require('path')`

    Member | Description
    --- | ---
    `path.sep` | File separator
    `path.join(...path:string[])` | join a string in pieces to a whole *string*
    `path.baseName(path:string)` | Gets the last chunk of path given
    `path.resolve(...path:string)` | Gets the absolute path *start with `__dirname`*

* fs `require('fs')`
    1. sync

        Member | Description
        --- | ---
        `readFileSync(path,encoding):string`| Read file contents synchronously
        `writeFileSync(path,encoding,options?:{flag:char})` | Write file synchronously
        `existsSync(path)` | returns boolean

    1. async

        Member | Description
        --- | ---
        `readFile(path,encoding,callback:(err,res)=>{...}` | Read file contents asynchronously
        `writeFile(path,encoding,callback:(err,res)=>{...}` | Write file asynchronously

        > **callback** use defensive programming

        <dl>
            <dt>Sync</dt>
            <dd>happens for once; can't support lots of users</dd>
            <dt>Async</dt>
            <dd>an approach in which may support many users; watch command times</dd>
        </dl>

* http `require('http')`
    
    #### 2 members

    1. `http.createServer((req:obj,res:obj)=>{...}):server`
        
        * ##### callback params

            * req

                Member | Description
                ---|---
                `url` | Requested url
                `method` | Requested method

             * res

                Member | Description
                ---|---
                `writeHeader(status:number, headers:{content-type:mime})` | Meta response data
                `write() && end()` | Both writes to the server; you should end the session

    1. `http.listen(:number)`

        > listens to the port number *arbitrarily 5000*

* ### npm stuff

    * `npm init`
        
        > **creates *package.json***  
        > **-y** if added defaults are accepted *recommended*

    * `npm i`

        > **install package(s)**  
        > if  `<package name>` is added it gets installed  
        > **@** maybe added to reference a specific package version e.g `express@4.17.1`  
        > else all *dependencies and devdependencies* gets installed  
        > **-D** if added then it's a *devdependency*  
        > **-g** if added *instead of* **-D** it's installed globally

* ### Promises trinity

    1. Promise object

        ``` javascript
        return new Promise((resolve, reject) => {
            // a function that has 2 results 
            if(working) resolve(data); // then()
            else reject(error); // catch()
        });
        ```
    1. util `require('util')`

        ``` javascript
        const util = require('util'); // you can just import {promisify}
        const {fn} = util.promisify(fn);
        // just use async fn
        ```
    1. sub packages *if exists*

        ``` javascript
        const {fn} = require('package/promises'); 
        // just use async fn
        ```
* ### Events

    Events functionality comes from `require('events')`
    arbitrarily code as follows 

    ```javascript
    const EventEmitter = require('events');
    const eventRef = new EventEmitter();
    ```
    <dl>
        <dt>eventRef.on(name:string, callback)</dt>
        <dd>Assigns an event to the eventRef</dd>
        <dt>eventRef.emit(name:string, ...args?)</dt>
        <dd>Fires the event as many times as it appeared in code; in a procedural fashion</dd>
    </dl>

* ### Streams 

    A way to chunk data for reading

    #### ReadStream class

    > `createStream(path:string,option?:string or options?:{})` => creates the object options  
    >   * `hightWaterMark:number` => chunk size  
    >   * `encoding` => charset mainly *utf8*
    >
    > ##### Events *`on()`*  
    >
    >   * `open` when resource is open 
    >   * `ready` happens after open  
    >   * `error` may occur   
    >   * `data` do what ever you want with *it's arg from callback*
