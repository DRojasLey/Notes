It is a client side protocol
meaning it will be started from the browser, client side 


## types
it can be any of the following types:

* GET -- for fetching data
* POST -- send data to the server
* PUT or PATCH -- update data in the server
* DELETE -- delete data from the server

## Status codes:

![[HTTPS.png]]


* 100 -- Continue
	* Things are getting processed
* 200 -- success
	* 200 -- success
	* 201 -- created
	* 204 -- no content
* 300 -- Redirects
	* 301 -- resource moved
* 400 -- client error
	* 400 -- Bad request 
	* 401 -- Unauthorized
	* 403 -- Forbidden
	* 404 -- Not found
* 500 -- server error

Investigate:

XMLHttpRequest()

