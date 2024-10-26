Used for request and processes that take time to process.

#### Promises:
Consider the function:

return a promise first:
Promise() takes a function as a parameter
that function must have resolve and reject as parameters 

```js
const getSomething = () =>{ // regular callback function declaration
		 
	return new Promise((resolve, reject) =>{ 
		//fetch something
		
		resolve(//data to be returned by the promise);
		
		reject(//error produced by the request);
		
	});
}
```

A promise is something that will take some time to process, it will return as 'resolved' (+data) or 'rejected' (+error).

#### .then method for handling the success of a promise

We can store the promise of data and process it later with the .then method, which takes a function as parameter as well.

.then takes the data and passes it as parameter for the CB-function we provide for resolved promise.

.then takes two parameters, the function in case of 'resolve' and the function in case of reject.

```js
getSomething().then((data) => { 
	// we process the data we received 
	console.log(data);
}, (error) =>{ 
	//we process the error
	console.log(error)
});
```

The function in case of reject will take the error as parameter automatically.

#### the .catch  method for handling errors of a promise

A better way to process that data is to use the .catch method chained to the then:

```
getSomething('route to resource').then(data => { 
	// we process the data we received 
	console.log(data);
}).catch(error => {
	//we process the error
	console.log(error)
});
```
##### sequential promises for sequential data fetch
```js
getSomething('route to resource').then(data => { 

	// we process the data we received 
	
	console.log( 'promise 1 resolved', data);
	
	// for sequential we want to return a promise to the function call:
	
	return getSomething('route to second resource');
	
}).then(data =>{ 
// because the previous function returns a promise we go ahead and chain .then again.
	// we process the data we received
	console.log('promise 2 resolved', data);
	
}).catch(error => { 

	//we process the error
	console.log(error)
	
});
```

#### fetch(); API an easier way to handle promises

```js
fetch(resourceURL).then(response =>{
	// resolve section
	// check for status and handle errors
	// process the response data
}).catch( err =>{
	//rejected section
	//process the error
});
```
In contrast to the previous promises way of doing things, the fetch() API will only reject in case there is a network error. For other errors we will get 'resolved' and the actual error we are getting.

That implies that we need to do error handling inside the resolve section as well.

The Fetch API will construct an object, and under the object we need to use the .json() method to parse the response data, (else we will be trying to process the promise itself)

```js
fetch(resourceURL).then(response => {
	// resolve section
	// check for status and handle errors on the response
	// process the response (not the data yet)
	return response.json(); << this returns a promise, cannot be stored in variable, we chain it instead
}).then(data => { // now we process the data
	//resolve section of the previous promise
}).catch( err =>{
	//rejected section
	//process the error
});
```

Because we need to pass the .json() method we will be getting a promise from the data, so we need to chain it to a second .then method (as in sequential data processing)

#### async, a way to chain promises in a more concise and clean way

Any function with the async keyword returns a promise

How to call an async function:

```js
const getThings = async () => {
	//this will always return a promise to the variable.
}
```

This is a test to better illustrate how it works:

```js
const getThings = async () => {
	//this will always return a promise to the variable.
}
const test = getThings();
console.log(test);
```

Which as expected returns the promise

```js
Console output:
1. Promise {<fulfilled>: undefined}
1. [[Prototype]]: Promise
2. [[PromiseState]]: "fulfilled"
3. [[PromiseResult]]: undefined
```


#### await, completing the async functions
##### Further building the function :

We would normally write like this:
```js

const getThings = async () => {
	fetch('resourceToFecht or URL').then(() => {
		//what to do with the data goes here
	});
}
```

But instead with await:

```js
const getThings = async () => {
	const response = await fetch('resourceToFecht or URL');
	
	// here we can use the data and process it as soon as it becomes available:
	
	const data = await response.json() // get data from the promise
	
	return data; // return the data so we can process it furter in the code
}
```

In that example the fetch will process the data and return a promise, but instead of assigning the data directly to the 'response' variable, it will stall JS so it is not assigned immediately, but until the promise has resolved.

Some key-points:

* This process does not block JS because everything is processed inside the async function.
* Remember that the fetch will return a promise, to extract the data we use the .json() method of the promise

##### How to chain the promises using this method:

This code is much cleaner than the previous  sequential calls

```js
const getThings = async () => {
	const response = await fetch('resourceToFecht1 or URL');
	const data1 = await response.json() 
	const response = await fetch('resourceToFecht2 or URL');
	const data2 = await response.json() 
	const response = await fetch('resourceToFecht3 or URL');
	const data3 = await response.json() 
	
	return data; // return the data so we can process it furter in the code
}
```

#### Complete code:

```js
const getThings = async () => {
	const response = await fetch('resourceToFecht or URL');
	const data = await response.json() // get data from the promise
	return data; 
}
// now we call the function (which returns a promise)
getThings().then(data=> {
	//we use then to extract the data from the promise so we can now start procesing it:
	console.log(data)
});

```

Cleaner version (with rejected processing): 

```js
const getThings = async () => {
	const response = await fetch('resourceToFecht or URL');
	const data = await response.json() // get data from the promise
	return data; 
}

getThings().then(data => console.log(data))
.catch( error => console.log(error));
```

#### Creating custom errors

Previously we learned that the fetch API will not 'reject' the promise unless there was a network error, so regular malformed JSON or 404 status (or similar) will still read as "resolved", so we need to manually check the data and create error for it, this is a general idea of how this works:

```js
const getThings = async () => {
	const response = await fetch('resourceToFecht or URL');
		if (response.status !== 200){
			throw new Error();
		}
	const data = await response.json() // get data from the promise
	return data; 
}

getThings().then(data => console.log(data))
.catch( error => console.log(error));
```

This works because when we throw an error  inside an async function the promise of the async function will have status 'rejected'.

And rejected will then be .catch by our code



