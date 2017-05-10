# ES6

## Learning Objectives

- Explain the history of Javascript and ECMAScript
- Compare/contrast features of ES5 and ES6
- Explain when to use `var` vs. `let` vs. `const`
- Use template literals to interpolate variables and strings
- Use deconstruction to extract values from objects and arrays
- Use default parameters and arrow functions

## Framing (10 minutes / 0:10)

Today, we are going to be looking at a new way to write Javascript by playing with some of the new features released with ES6.

### Javascript vs. ECMAScript

The Javascript standard is officially referred to as [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript).

As Javascript is so widely used that any changes would affect the whole web, there is a body known as Ecma International, which formally approves official versions for release. Each version contains features and changes to be added to the language.

In short, ECMAScript is the language, and JavaScript an implementation of that language. <!-- AM: Is this worth getting into? -->

### Evolution of Javascript

> Check out [this awesome visualization](http://shaunlebron.github.io/solar-system-of-js/#0) of the current state of the Javascript universe

#### Timeline

- **1999: ES3 released.** This was the first widespread use of the Javascript.
- **2009: ES5 released.** This is what we have been writing so far in class.
- **2015: ES6 published.** This brought about a wide set of new features and syntax.

> ES4 was never released, largely due to political reasons

#### Why now?

Many plugins, frameworks and modules still use ES5, as browser support for
the new version of the language is [still not universal](http://caniuse.com/#search=es6), but the new syntax and features
of ES6 are increasingly becoming more and more popular in the developer world at large. You are very likely to see it pop up in the documentation of some of the technologies we will be using in this course.

Today is all about exploring some of the [new features](https://github.com/lukehoban/es6features) and getting comfortable with the new syntax.

> For more backstory, we recommend checking out [this talk](https://www.youtube.com/watch?v=PlmsweSNhTw) from Brendan Eich on what he views as the future of Javascript.

## New Features

### Block Scope (10 minutes / 0:20)

<details>
  <summary><strong>What does the concept of scope refer to in Javascript?</strong></summary>

  > In short, the notion of which variables are available where.

</details>

<br>

<details>
  <summary><strong>What is the primary way to control scope in Javascript? Why do we want to control scope?</strong></summary>

  > Functions create new local scopes.
  >
  > Scope allows us to use generic variable names using `var` while considering them in an isolated space. This makes our code easier to reason about.

</details>

#### `let`

The fact that blocks of other special forms (`if`, `for`, `while`, etc) *do not* create scopes is one of the oddities for which Javascript gets knocked. <!-- AM: What are some examples of Javascript getting knocked? -->

ES6 introduces the `let` keyword which works just like `var` but is scoped to its block (`{...}`) rather than its function.

Some examples of block scope are...
- `if` statements
- `while` and `for` loops
- functions
- singular `{ }` blocks

> Object literals **are not** code blocks. Object literals should always follow an assignment or be provided as an argument to a function but never stand on their own.

Below are contrived examples of isolating a variable `x` to a local scope.

Prior to ES6, we needed to use something called an IIFE ("immediately invoked function expression") to place the `x` (which is a `var`) in an isolated scope. This is because `var`s are ***function-scoped***. In contrast `let` statements are ***block scoped***, meaning they don't exist or are not accessible outside of curly braces `{}`.  <!-- AM: Did we have to use an IIFE? Why not a named function? Don't want to make earliest examples too contrived/complicated... -->

<!-- AM: Maybe add an exercise similar to the scope lesson in which they have to identify the values of variables at certain points in the code... -->

```js
// ES5
var x = 1;
(function(){
  var x = 2
  console.log(x);
})();
console.log(x);
```


```js
// ES6
var a = 1;
{
  let a = 2;
  console.log(a);
}
console.log(a);
```

You're more likely to see `let` declarations inside an `if` or `for` block:

```js
// ES5
for(var i = 0; i < 10; i++) {
  console.log(i)
}

console.log("outside loop:", i)
```

```js
// ES6
for(let j = 0; j < 10; j++) {
  console.log(j)
}

console.log("outside loop:", j)
// => Uncaught ReferenceError: j is not defined
```

The function-scoped behavior of `var` and block-scoped behavior of `let` can have some puzzling but important differences in certain situations. We will delay the `console.log(i)` operation, or evaluating `i`, with `setTimeout` to highlight an important distinction in how **scope** with `let` and `var` operates differently.

In the following scenario, since `var` is ***not block-scoped***, it "leaks" outside of the for-loop. This is not the case with `let`, which is **block-scoped**.

```js
// ES5
for (var i = 0; i < 10; i++) {
  setTimeout(function(){
    console.log(i)
  }, 200)
}
```

```js
// ES6
for (let j = 0; j < 10; j++) {
  setTimeout(function(){
    console.log(j)
  }, 200)
}
```


#### `const`

ES6 introduces another keyword for declaring variables: `const`. It declares a variable that won't be reassigned or redeclared.

```js
const a = 1;
a = 2;
// => Uncaught TypeError: Assignment to constant variable.

const a = 2;
// => Uncaught SyntaxError: Identifier 'a' has already been declared

var a = 2;
// => Uncaught SyntaxError: Identifier 'a' has already been declared
```

### You Do: Block Scope Exercises (10 minutes / 0:30)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/01-var-let-const.js
2. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/02-const-complex.js

### Default parameters (5 minutes / 0:35)

Here we've defined a function with three parameters. We then invoke the function with two arguments...

```js
function printAndSum(a, b, c){
  console.log(a)
  console.log(b)
  console.log(c)
  return a + b + c
}

printAndSum(1, 2)
// => 1
// => 2
// => undefined
// => NaN
```

With ES6, we now have the option to set a default value for any of our functions' parameters...

```js
function printAndSum(a = 0, b = 0, c = 0) {
  console.log(a)
  console.log(b)
  console.log(c)
  return a + b + c
}

printAndSum(1, 2)
// => 1
// => 2
// => 0
// => 3
```

> Is there a more pragmatic example we can use here?

#### You Do: Default Parameters Practice (10 minutes / 0:45)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/04-default-parameters.js
2. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/05-default-parameters.js

### Destructuring (10 minutes / 0:55)

Destructuring makes it possible to extract data from collections (i.e., arrays and objects) into distinct variables.

#### Destructuring Arrays

```js
let [a,b] = [1,2]

a
// => 1

b
// => 2

let nums = [1,2,3,4,5]
let [first, second, third] = nums

first
// => 1

second
// => 2

third
// => 3
```

#### Destructuring Objects

```js
var user = {
   id: 1,
   name: "Bob",
   age: 43 ,
   profile_url:  "http://api.co/users/1",
   location: "DC"
}

// ES5
function greetUser (user) {
  console.log("Hello " + user.name + ", how's the weather in " + user.location)
}

// ES6
function greetUser ({ name, location })  {
  console.log("Hello " + name + ", how's the weather in " + location)
}
```

<!-- AM: Add an example where we define multiple variables using objects keys on the same line. -->

#### You Do: Destructuring Practice (15 minutes / 1:10)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/06-deconstruction.js

## Break (10 minutes / 1:20)

### Concise Object Literal Definitions (5 minutes / 1:25)

<!-- AM: Overall framing for this section? What does "concise" mean here? -->

#### Methods

ES6 allows us to shorten method definitions from this...

```js
// ES5
var car = {
  drive: function(){
    console.log("vroom")
  }
}
```

...to this...

```js
// ES6
let car = {
  drive() {
    console.log("vroom")
  }
}
```
<!-- AM: Include attributes in object -->

#### Properties

It is very common that we will set a property to the value of a variable by the same name.
ES6 lets us avoid this redundance.

```js
// ES5
var x = 1
var y = 2
let obj = {
  x: x,
  y: y
}

// ES6
let x = 1
let y = 2
let obj = { x, y }
```

> This functionality is not particular to `let`. We could replace `let` with `const` or `var` in these examples.

#### You Do: Concise Methods and Properties Practice (10 minutes / 1:35)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/07-concise-properties-and-methods.js

### Template Literals (5 minutes / 1:40)

Here's how we previously used variables to build custom strings...

```js
var name = "Inigo Montoya"
var killee = "father"
var prepareTo = "die"

console.log("Hello. My name is "+ name + ". You killed my " + killee +". Prepare to " + prepareTo)
```

ES6 introduces a template literal syntax for strings...

- Backticks surround the entire string template
- Line breaks are permitted
- `${...}` are placeholders for interpolating Javascript expressions

```js
let name = "Inigo Montoya"
let killee = "father"
let prepareTo = "die"

console.log(`Hello. My name is ${name}. You killed my ${killee}. Prepare to ${prepareTo}`)
```

<!-- AM: Anything else to say in this section? -->

#### You Do: Template Exercise (10 minutes / 1:50)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/09-templates.js

### Arrow Functions (15 minutes / 2:05)

Arrow functions are a new shorthand syntax for defining anonymous functions...

<!-- AM: Start with an example that compares single functions -- not inside of .forEach -->
<!-- AM: Also earlier on talk about how this relates to function declarations / expressions. -->
<!-- AM: They don't know `.forEach` yet. Either introduce officially now or replace examples. -->

```js
// ES5
let foods = ["pizza", "mac n cheese", "lasagna"]

foods.forEach(function(food, i){
  console.log("My #" + i + "favorite food is " + food)
})

// ES6
let foods = ["pizza", "mac n cheese", "lasagna"]

foods.forEach((food, i) => {
  console.log(`My #${i} favorite food is ${food}`)
})
```

If we have only one argument to the function, we don't need to surround it in parens...

```js
foods.forEach(food => {
  console.log(`I love ${food}`)
})
```

But we do for functions that take more than one or no arguments...

```js
// No arguments
let makeNoise = () => console.log("Bang!")
makeNoise() // => Bang!
```

#### Return Statements

Here is a standard multi-line arrow function written using no shorthands. With a multi-line function, you (usually) need to explicitly return (i.e., use the `return` keyword).

```js
var add = (num1, num2) => {
  const sum = num1 + num2
  return sum
}
```

If the function is single-line, you can omit both the return keyword and curly brackets...

```js
var add = (num1, num2) => num1 + num2

add(2, 3)
// => 5
```

If the function is multi-line, you need to explicitly return. Otherwise, you get this...

```js
let add = (x,y) => {
  x + y
}

add(2,3)
// => undefined
```

Though the single line return can be faked by wrapping the expression in parentheses...

```js
let add = (x,y) => (
  x + y
)
```

#### Context in Arrow Functions

<!-- AM: Is it always a benefit? What are some "weird" cases (i.e., event listeners)? -->
Arrow functions also have the benefit of maintaining the context (`this`) of where the function is defined...

Context works differently in arrow functions than it does in ES5. Consider the below example.

<details>
  <summary><strong>What is the result of running `this.temperature++`? Why?</strong></summary>

  > `setInterval`'s callback is what we call an "unbound" function (i.e., it is stand-alone and not contained in an object). That means that it will default to a global context, which in the browser is the `window` object.
  >
  > When we call `this.temperature++`, Javascript looks for a `temperature` property on the `window` object. This does not occur naturally.
  >
  > If we `console.log(window.temperature)`, we see that it is `NaN`. This is the result of incrementing an `undefined` value by 1.

</details>

```js
var pizza = {
  temperature: 0,
  toppings: ["cheese", "ham", "pineapple"],
  bake() {
    setInterval(function() {
      this.temperature++
    }, 1000)
  }
}

pizza.bake()
console.log(pizza.temperature)
```

It would be nice, however, if we could use `this` in a similar way and have it work.

Let's try the same thing, except this time we will replace `setInterval`'s callback function with an arrow function.

<details>
  <summary><strong>What is the result of running `this.temperature++`? What might this tell us about context when using arrow functions?</strong></summary>

  > It incremented the `temperature` value stored in pizza!
  >
  > Perhaps unbound arrow functions do not default to the global scope...

</details>

```js
var pizza = {
  temperature: 0,
  toppings: ["cheese", "ham", "pineapple"],
  bake() {
    setInterval(() => {
      this.temperature++
    }, 1000)
  }
}

pizza.bake();
console.log(pizza.temperature)
```

An arrow function's context is defined by its enclosing context (i.e., where it is defined). In this case, that enclosing context is the `pizza` object. An arrow function does not create its own context, unlike an unbound `function` which would have created its own context -- `window`.

<!-- AM: Something about event listeners? Or have them encounter that in an exercise? -->

#### You do: Arrow functions (15 minutes / 2:20)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/11-arrow-functions.js

## Legacy Browser Support

Support for ES6 is great! Check out this [compatibility table](https://kangax.github.io/compat-table/es6/).

If you need to support a legacy browser, check out the following tools...
- [Babel](https://babeljs.io/)
- [Traceur](https://github.com/google/traceur-compiler/wiki/Getting-Started)

## Bonus

### Spread Operator

The spread operator `...` allows an expression to be expanded into multiple elements.

This is useful for separating an array into individual elements...

```js
var dimensions = [10, 5, 2]
var volume = function(height, width, length){
  return height * width * length
}

// ES5
volume(dimensions[0], dimensions[1], dimensions[2])

// ES6
volume(...dimensions)
```

#### Avoiding Mutation

This also makes it very easy to create copies of an array in functions where
mutation occurs. Here is some code in which we generate a reversed array of days (`reversedDays`) from a sorted array of days (`days`). This approach ends up mutating the original `days` array.

```js
var days = ["monday","tuesday","wednesday","thursday","friday","saturday","sunday"]
function reversedDays(arr){
  return arr.reverse()
}
console.log(reversedDays(days))
// => Returns the reversed array of days.

console.log(days)
// => But now `days` is reversed as well.
```

We can use the spread operator to avoid this effect. Below you'll find two examples: one that does not use the spread operator and one that does.

```js
// ES5
function reversedDays(arr){
  var newArray = []
  for(let i = 0; i < arr.length; i++){
    newArray.push(arr[i])
  }
  return newArray.reverse()
}
console.log(reversedDays(days))
console.log(days)

// ES6
function reversedDays(arr){
  return [...arr].reverse()
}
console.log(reversedDays(days))
console.log(days)
```

#### You Do: Spread Practice

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/03-spread-practice.js

## Keep Going

There are plenty more ES6 features that we have not covered...

- [Symbols](http://es6-features.org/#SymbolType)
- [Iterator & for..of operator](http://es6-features.org/#IteratorForOfOperator)
- [Generators](https://davidwalsh.name/es6-generators)
- [Proxies](https://ponyfoo.com/articles/es6-proxies-in-depth)
- [Reflection and meta-programming](http://www.2ality.com/2011/01/reflection-and-meta-programming-in.html)

## Resources

- [You Don't Know ES6](https://github.com/getify/You-Dont-Know-JS/tree/master/es6%20%26%20beyond)
- [Block Scope](https://www.sitepoint.com/joys-block-scoping-es6/)
- [Destructuring](http://www.2ality.com/2015/01/es6-destructuring.html)
- [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals)

## Additional Practice

Update the following exercises to include ES6 features.

- [ATM](https://github.com/ga-wdi-exercises/atm)
- [Cash Register](https://github.com/ga-wdi-exercises/cash-register)
- [Choose Your Own Adventure](https://github.com/ga-wdi-exercises/choose_your_own_adventure_js)

<!-- AM: Replace an original exercise(s) with one/some of these? -->
