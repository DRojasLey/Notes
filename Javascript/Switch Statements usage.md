Switch statements in JavaScript can be useful for simple branching based on a single variable or expression, especially when there are multiple well define cases to handle. 

However, they do come with limitations and are sometimes considered less ideal in specific situations. Here are some common pros and cons of using them:

### Pros of Using Switch Statements

1. **Readability**: (for short cases) When there are multiple specific cases to handle, switch statements can make code easier to read than multiple `if...else if` statements.
2. **Performance**: In some JavaScript engines, switch statements can be optimized for performance better than multiple `if...else if` conditions, especially when there are many cases.
3. **Grouping Cases**: Switch statements allow grouping cases that should execute the same block of code, which is helpful for cases that share functionality.

### Cons of Using Switch Statements

1. **Limited Flexibility**: Switch statements only work with discrete values, meaning they can't handle more complex conditions (like ranges or logical combinations).
2. **Code Duplication**: If a switch has multiple similar cases that need slightly different handling, this can lead to duplicated code.
3. **Maintainability**: Large switch statements can become unwieldy and harder to maintain. The more cases there are, the more difficult it becomes to understand the flow.
4. **Error-Prone with `break`**: Forgetting a `break` statement can lead to unexpected behavior due to fall-through.
5. **Encourages Procedural Logic**: Large switch statements are generally associated with procedural code, which can make it harder to follow compared to other patterns like polymorphism, especially in object-oriented programming.

#### 3rd con details:

Taking into account modern Js data structures and the usage of objects, we can better define functions using objects for the values we need to check, making the information more accessible and the function can be easily escalated in case of new cases, without needing to add whole new switch statements:

```js
function **Switch_RPSLS_Eval_Game**(alice, bob) {  
// If Alice and Bob chose the same choice, we will output a tie  
if (alice === bob) {  
console.log("Alice and Bob tie")  
}  
else {  
let isAliceWin; // variable to determine if alice won  
// Switch on Alice choice  
**switch (alice) {**  
**case "Rock":** **switch (bob)** {  
**case "Lizard":**  
**case "Scissors":** isAliceWin = true;  
**break;**  
**default:** isAliceWin = false;  
}  
**break;**  
**case "Scissors":** switch (bob) {  
**case "Lizard":**  
**case "Paper":** isAliceWin = true;  
**break;**  
**default:** isAliceWin = false;  
}  
**break;**  
**case "Paper":** **switch (bob)** {  
**case "Spock":**  
**case "Rock":** isAliceWin = true;  
**break;**  
**default:** isAliceWin = false;  
}  
break;  
**case "Lizard":** **switch (bob)** {  
**case "Paper":**  
**case "Spock":** isAliceWin = true;  
**break;**  
**default:** isAliceWin = false;  
}  
**break;**  
**case "Spock":** switch (bob) {  
**case "Rock":**  
**case "Scissors":** isAliceWin = true;  
**break;**  
**default:** isAliceWin = false;  
}  
**break;**  
}  
if (isAliceWin) {  
console.log("Alice Wins!");  
}  
else {  
console.log("Bob Wins!");  
}  
}  
}
```


Vs the object based solution:


```js
const RPSLS_rules = {  
Rock: {  
Scissors: true,  
Lizard: true  
},  
Scissors: {  
Paper: true,  
Lizard: true  
},  
Paper: {  
Rock: true,  
Spock: true  
},  
Lizard: {  
Paper: true,  
Spock: true  
},  
Spock: {  
Scissors: true,  
Rock: true  
}  
};

function createRuleGame(rulesObj) {  
return function (alice, bob) {  
// If Alice and Bob chose the same choice, we will output a tie  
if (alice === bob) {  
console.log("Alice and Bob tie")  
}  
else {  
// variable to determine if alice won  
let isAliceWin = rulesObj[alice][bob];  
if (isAliceWin) {  
console.log("Alice Wins!");  
}  
else {  
console.log("Bob Wins!");  
}  
}  
}  
}


const Object_RPS_Eval_Game = createRuleGame(RPS_rules)
```


The second option is easier, not only to read, but to add more variables.

## Conclusion:

Switch statements can be safely used, but they are unnecessary due to modern Js features.

[Source: Medium](https://nisimdor.medium.com/why-we-really-need-to-stop-using-switch-statements-in-javascript-cdd0ab61ef5a)
