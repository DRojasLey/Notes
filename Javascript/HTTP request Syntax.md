**XMLHttpRequest:** The traditional method, directly interacting with the browser's built-in object.
Create an instance and set the requirements:
```js
const xhr = new XMLHttpRequest();

// (method, URL, asynchronous)
xhr.open('GET', 'https://api.example.com/data', true); 
```

**Handle Response:**

**XMLHttpRequest:**

JavaScript

```js
xhr.onload = function() {
  if (xhr.status === 200) {
    console.log(xhr.responseText);
  } else {
    console.error('Request failed: ' + xhr.status);
  }
};

xhr.send();
```

- **Headers:** Set headers using `xhr.setRequestHeader()` (XMLHttpRequest) or the `headers` option in `fetch()`.
- **Asynchronous vs. Synchronous:** The third argument in `xhr.open()` controls whether the request is asynchronous (default) or synchronous.
- **Error Handling:** Use `xhr.onerror` or `xhr.onreadystatechange` for more granular error handling in XMLHttpRequest.
- **Promises:** The Fetch API uses promises for asynchronous operations, making it easier to handle errors and chain requests.

### Fetch API:

**. GET Request:**

- **Purpose:** Retrieves data from a specified URL.
- **Syntax:**
    
    JavaScript
    
    ```js
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => {
        // Process the retrieved data
        console.log(data);
      })
      .catch(error => {
        // Handle    1.  juejin.cn juejin.cn errors
        console.error(error);
      });
    ```

**POST Request:**

- **Purpose:** Sends data to a specified URL, often for creating new resources.
- **Syntax:**
```js
fetch('https://api.example.com/data', { 
	method: 'POST',
	headers: { 'Content-Type': 'application/json' },
	body: JSON.stringify({ // Data to be sent 
		name: 'John Doe',
		age: 30 
		})
	}) 
	.then(response => response.json()) // parses the response as JSON
	.then(data => { // Process the response
		console.log(data);
	 })
	.catch(error => { 
	// Handle errors 
	console.error(error); 
	});  

```


PUT Request:

**3. PUT Request:** - **Purpose:** Updates existing data at a specified URL. - **Syntax:** 

```javascript
fetch('https://api.example.com/data/123', {
	method: 'PUT',
	headers: { 'Content-Type': 'application/json' },
	body: JSON.stringify({
		// Updated data
		name: 'Jane Smith',
		age: 25
	}) })
	.then(response => response.json())
	.then(data => {
		// Process the response
		console.log(data);
	})
	.catch(error => {
		// Handle errors
		console.error(error);
	});
```


DELETE Request:
  
```js
fetch('https://api.example.com/data/123', {
	  method: 'DELETE'
	})
	  .then(response => response.json())
	  .then(data => {
		// Process the response
		console.log(data);
	  })
	  .catch(error => {
		// Handle errors
		console.error(error);
	  });
```

