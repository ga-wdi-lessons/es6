# ES6

## Learning Objectives

- Explain the history of ES and JS
- Compare/contrast features of ES5 and ES6
- Explain when to use `var` vs `let` vs `const`
- Use template literals to interpolate variables and strings
- Use deconstruction to extract values from objects and arrays
- Use default parameters and arrow functions

## Framing (15 / 15)

Today, we are going to be looking at a new way to write Javascript by playing with some of the new features released in ES6.

### JS vs ES

The JavaScript standard is officially referred to as [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript).

As JS is so widely used that any changes would affect the whole web, there is a body known as TC39 or Ecma International, which formally approves official versions for release.

Each version contains features / changes to be added to the language.

In short, I like to think of ECMAScript as the language, and JavaScript an implementation of that language.

### Evolution of JS

> Check out [this awesome visualization](http://shaunlebron.github.io/solar-system-of-js/#0) of the current state of the JS universe

Condensed timeline:

- 1999 - ES3 released, the first widespread use of the language.
- ES4 never released, largely due to  political reasons
- 2009 - ES5 released, what we've been writing so far in class.
- 2015 - ES6 published releasing a wide set of new features and syntax

#### Why now?

Many plugins, frameworks and modules still use ES5, as browser support for
the new version of the language is [still not universal](http://caniuse.com/#search=es6), but the new syntax and features
of ES6 are increasingly becoming more and more popular among many open-source projects and in the developer world at large. Also,
you are very likely to see it pop up in the documentation of some of the technologies we will be using in this course.

Today is all about exploring some of the [new features](https://github.com/lukehoban/es6features) and getting comfortable with
the new syntax.

> For more backstory, we recommend checking out [this talk](https://www.youtube.com/watch?v=PlmsweSNhTw) from Brendan Eich on what he views as the future of JS.

## New Features

### Block Scope (10 / 25)

<details>
<summary>What does the concept of scope refer to in JS?</summary>

In short, the notion of which variables are available where.

</details>

---

<details>
<summary>So far in class, what is the primary way to control scope in JS? Why do we want to control scope?</summary>

Functions create new local scopes.

Scope allows us to use generic variable names (eg `count`, `input`, `evt`) while considering them in an isolated space.
This makes our code easier to reason about.

</details>

#### `let`

The fact that other blocks (`if`, `for`, `while`, etc) *do not* create scopes is one of the oddities for which JS does and should get knocked.

ES6 introduces the `let` keyword which works just like `var` but is scoped to its block (`{...}`) rather than its function.

> Objects use curly braces `{}` but are not code blocks!

Below are contrived examples of isolating a variable `a` to a local scope.
Pre-es6 we need to use a verbose IIFE (immediately invoked function expression) to create an isolate scope.

```js
// es5
var a = 1;
(function(){
  var a = 2
  console.log(a);
})();
console.log(a);
```


```js
// es6
var a = 1;
{
  let a = 2;
  console.log(a);
}
console.log(a);
```

You're more likely to see `let` declarations inside an `if` or `for` block:

```js
//es5
for(var i = 0; i < 10; i++){
  console.log(i)
}
console.log("outside loop:", i)

// versus

//es6
for(let j = 0; j < 10; j++){
  console.log(j)
}
console.log("outside loop:", j)
//throws an error
```
#### `const`

ES6 introduces another keyword for declaring variables: `const`

`const` declares a variable that won't be reassigned or redeclared:

```js
const a = 1;
a = 2;
// Throws an error in chrome
const a = 2;
// throws an error
var a = 2;
// throws an error
```

### You do: Block Scope Exercises (10 / 35)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/01-var-let-const.js
2. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/02-const-complex.js

### Default parameters (5 / 40)

If a function defined to take 3 parameters is called with two arguments, what is the value of the third parameter in the function body?

For example:

```js
function printAndSum(a, b, c){
console.log(a)
console.log(b)
console.log(c)

return a + b + c
}

printAndSum(1, 2)

// => ???
```

With ES6, we now have the option to set a default value for any of our functions' parameters.

```js
function hello( name = "stranger"){
  console.log("Hello, " + name)
}

hello() // Hello, stranger
hello('Juan') // Hello, Juan
```

How can we make our `printAndSum` example more durable?

#### You do: Default Parameters Practice (10 / 50)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/04-default-parameters.js
2. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/05-default-parameters.js

### Destructuring (10 / 60)

Destructuring assignment makes it possible to extract data from collections (arrays and objects) into distinct variables:

```js
// destructuring arrays
let [a,b] = [1,2]
a 
//=> 1
b 
//=> 2
let nums = [1,2,3,4,5]
let [first, second, third] = nums
first 
//=> 1
second 
//=> 2
third 
//=> 3
```


```js
// destructuring objects
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

// In ES6 becomes

function greetUser ({ name, location })  {
  console.log("Hello " + name + ", how's the weather in " + location)
}

//You would call both by using: greetUser(user)
```

#### You do: Destructuring Practice (15 / 75)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/06-deconstruction.js


## Break (10 / 90)

### Concise Object Literal Definitions (Properties and Methods) (5 / 95)

ES6 allows us to shorten method definitions from:

```js
var car = {
  drive: function(){
    console.log("vroom")
  }
}
```

to

```js
let car = {
  drive(){
    console.log("vroom")
  }
}
```

It is very common that we will set a property to the value of a variable by the same name.
ES6 lets us avoid this redundance.

```js
// es5
var x = 1
var y = 2
let obj = {x:x, y:y}

// vs
//es6
let x = 1
let y = 2
let obj = {x,y}
```

NOTE: this is not `let` giving us this ability. `vars` and `conts` can be used to set object properties the same way in es6

#### You do: Concise methods and properties practice (10 / 105)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/07-concise-properties-and-methods.js

### Template Literals (5 / 110)

Here's how we previously used variables as to build custom strings.

```js
var name = "Inigo Montoya"
var killee = "father"
var prepareTo = "die"

console.log("Hello. My name is "+ name + ". You killed my " + killee +". Prepare to " + prepareTo)
```

ES6, introduces a template literal syntax for strings:

- `\`` (backticks) surround the entire string template
- line breaks are permitted
- `${...}` are placeholders for interpolating JS expressions

```js
let name = "Inigo Montoya"
let killee = "father"
let prepareTo = "die"

console.log(`Hello. My name is ${name}. You killed my ${killee}. Prepare to ${prepareTo}`)
```

#### You do: Template Exercise (10 / 120)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/09-templates.js

### Arrow Functions (15 / 135)

Arrow functions are a new shorthand syntax for defining anonymous functions:

```js
let foods = ["pizza","mac n cheese","lasagna"]
foods.forEach( food => console.log(`I love ${food}`) )

// vs the old

foods.forEach(function(food){
  console.log("I love " + food)
})
```

If there is more or fewer than one argument to the anonymous function, wrap
them in parens:

```js
let foods = ["pizza","mac n cheese","lasagna"]
foods.forEach( (food,i) => console.log(`My #${i} favorite food is ${food}`) )
```

Arrow functions also have the benefit of keeping the context (`this`) of where it is defined:

```js
var pizza = {
  temperature: 0,
  toppings: ["cheese", "ham", "pineapple"],
  bake() {
    setInterval(function(){
      this.temperature++ // doesnt work because this is GLOBAL. The setInterval function belongs to the window object.
    }, 1000)
  }
}

// vs ES6

var pizza = {
  temperature: 0,
  toppings: ["cheese", "ham", "pineapple"],
  bake() {
    setInterval( () => {
      this.temperature++
    }, 1000)
  }
}

pizza.bake();
pizza.temperature //will display the return value of setInterval, which is the ID value of the timer that was set
```

Additionally, the `return` statement is not needed with single line arrow functions. There is an implicit return.

```js
let add = (x, y) => x + y
add(2, 3) 
//=> 5
```

```js
//ES5
function subtract(x,y){
  x+y
}
//undefined in console
```

If the function is multi-line, you need to explicitly return:

```js
let add = (x,y) => {
  return x + y
}
add(2,3)
//undefined in console
```

Though the single line return can be faked by wrapping the expression in parentheses:

```js
let add = (x,y) => (
  x + y
)
```

#### You do: Arrow functions (15 / 150)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/11-arrow-functions.js


## Legacy Browser Support

Support for ES6 is great! - https://kangax.github.io/compat-table/es6/

If you need to support a legacy browser, check out the following tools:
- [Babel](https://babeljs.io/)
- [Traceur](https://github.com/google/traceur-compiler/wiki/Getting-Started)

## Bonus

### Spread operator

The spread operator `...` allows an expression to be expanded into multiple elements.

This is useful for separating an array into individual elements:

```js
var dimensions = [10, 5, 2];
var volume = function(height, width, length){
  return height * width * length;
}
volume(...dimensions);

// versus

volume(dimensions[0], dimensions[1], dimensions[2])
```

This also makes it very easy to create copies of an array in functions where
mutation occurs:

```js
var days = ["monday","tuesday","wednesday","thursday","friday","saturday","sunday"]
function reversedDays(arr){
  return arr.reverse()
}
console.log(reversedDays(days))
// but now days is no longer in order
console.log(days)

// To deal with this, we can either:

function reversedDays(arr){
  var newArray = []
  for(let i = 0; i < arr.length; i++){
    newArray.push(arr[i])
  }
  return newArray.reverse()
}
console.log(reversedDays(days))
console.log(days)

// or... (<- pun)

function reversedDays(arr){
  return [...arr].reverse()
}
console.log(reversedDays(days))
console.log(days)
```

#### You do: Spread Practice

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/03-spread-practice.js

## Keep Going

There are lots more features of ES6 that we have not covered:

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
