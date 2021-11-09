# Json-server
 
 Installed `npm i json-server`

 may watch a *.json* file and make requests for it in `package.json` scripts

 e.g
 ```json
 "serve-json": "json-server --watch [file]"
 ```

 ## Options using query string

 * **Filter** type *fieldName1=value&fieldName2=value*
 * **Sort and order** use properties _sort=[...fields]&_order=[...orderAbbreviation]
 * **Pagination** _page=result*10 can be paired with _limit per page

 > ### Notes  
 > * you can filter id on a rout param  
 > * If _limit was used alone (without _page) it's like `SELECT TOP # FROM json`
