# ES6: Block Scope Exercise

Each of the below code snippets will come with a prompt. It is your job to update the code snippet so that prompt is satisfied. Your answer must leverage what you just learned about block scope and variable declarations.

The prompts will indicate which lines of code you cannot modify and/or touch. You are not restricted, however, from adding code to the existing code snippets.

#### 1

Break the below code so that `myName = "Bob"` generates this error: `Uncaught SyntaxError: Identifier 'myName' has already been declared`

```js
var myName = "Adrian"

myName = "Bob"        // You cannot modify this line.

console.log(myName)   // You cannot move or modify this line.
```

#### 2

Break the code so that `console.log(num1)` and `console.log(num2)` generate reference errors (i.e., `Uncaught ReferenceError: num1 is not defined`).

`console.log(sum)` should print out the number 11.

```js
let sum = 0         // You cannot modify this line.

let num1 = 3        // You cannot modify this line.
let num2 = 8        // You cannot modify this line.
sum = num1 + num2   // You cannot modify this line.

console.log(sum)    // You cannot move or modify this line.
console.log(num1)   // You cannot move or modify this line.
console.log(num2)   // You cannot move or modify this line.
```

#### 3

Make it so that `callbacks[2]()` prints the number `2` to the console. In the current code, it prints the number `10` to the console.

```js
var callbacks = []                                // You cannot modify or move this line
for (var i = 0; i < 10; i++) {
  callbacks.push(function() { console.log(i) })   // You cannot modify or move this line
}

callbacks[2]()                                    // You cannot modify or move this line
```

> Hint: before adding or changing the code, think about why exactly `callbacks[2]()` prints out the number 10. Where is that number coming from?

#### 4

Make it so that you cannot set `account.password` to `"s3cret"`. Instead, `console.log(account.password)` should print out the key's original value: `"xyzzy"`.

```js
var account = {
  username: "marijn",
  password: "xyzzy"
}

account.password = "s3cret"

console.log(account.password)
```

> Hint: this answer might require something we have not covered yet. [Some Googling](https://www.google.com/search?q=javascript+object+read+only&oq=javascript+object+read+only&aqs=chrome..69i57j0l5.3718j0j4&sourceid=chrome&ie=UTF-8) might help though...
