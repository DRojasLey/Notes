

### Concept:

'The process in which a function calls itself directly or indirectly is called recursion and the corresponding function is called a recursive function.'

*[source](https://www.geeksforgeeks.org/introduction-to-recursion-2/)*

Other definitions:

In Computer science, recursion is a method of solving a problem where the solution depends on solutions to smaller instances of the same problem.


Any situation where you do something, and depending on the results, you might do it again.

### Interpretation:

Recursion is the act of calling a function from within itself

This implies that a recursive function is just a function calling itself

However a recursive function can also be interpreted as a sort of loop that will include all the parts of a for loop:

* Initialization
* Exit condition
* Advancement
* Action

This implies that all loops can be written as a recursive function, but not all recursive functions can be written as a loop

Consider the following loop
```javascript
for (let i =0; i < 10; i++){
	console.log(i) //action
}
```

It contains all the parts of a valid loop:

* `let i = 0` Initialization
* `i < 10` Exit condition
* `i++` Advancement
* `console.log(i)` Action

Now this recursive function will accomplish the same result:

```javascript
const recursiveFunction = (i) => {
	if (!(i < 10)) return 
	console.log(i) 
	recursiveFunction(i + 1)
}

recursiveFunction(0)

```

it also contains all the parts of a loop:

* `const recursiveFunction = (i) =>` Initialization (i is defined as the value we will use to track) & `recursiveFunction(0)` we call the function with the desired value.
* `if (!(i < 10)) return` Exit condition (if the value is no longer truth we will return)
* `recursiveFunction(i + 1)` Advancement (We call the function recursively )
* `console.log(i)` Action (we perform the same action as the loop)

### Examples:

#### Range returning function:

Test cases of the function:

```javascript
range(0,0);
range(1,5);
range(0,1);
```

Recursive solution:

```javascript
const range = (min, max, accumulator = []) => {

		if (min === max){
			console.log('base case', min, max, accumulator);
			return accumulator.concat(min);
		}
		console.log('recursive case', min, max, accumulator);
		return range(min + 1, max, accumulator.concat(min));
	}
}
```

Console Output:

![[Pasted image 20241008122443.png]]

### Resources:

https://www.recursionvisualizer.com/