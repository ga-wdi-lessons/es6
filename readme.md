#ES6

## Learning Objectives

- Compare/contrast features of ES5 and ES6
- Explain when to use var vs let vs const
- Use default parameters and arrow functions
- Use template literals to interpolate variables and strings
- Compare ES6 classes w/ ES5 prototypes
- Use import/export syntax with modules

## A Brief History of JavaScript

The JavaScript standard is referred to as EcmaScript.

I like to think of EcmaScript as the language, and JavaScript an implementation of that language.

ES3 was the first widespread use of the language. Unfortunately, ES4 never came out.

In 2009, ES5 was finalized and it's what we've been writing in class.

2015 brought ES6, published as a standard on June 17th, 2015.

### Why now?

Many plugins, frameworks and modules still use ES5, as browser support for
the new version of the language is still limited [ahem... ie.](http://caniuse.com/#search=es6)

Later today and tomorrow, we'll be working with a framework called React, and many
React tutorials (and our lesson plans) have adopted the new syntax and features
of ES6. Today is all about exploring those features and getting comfortable with
the new syntax.

## Syntax

### Block Scope

The primary way to control scope in an application has been through the use
of functions:

```js
var a = 1
(function(){
  var a = 2
  console.log(a)
})()
console.log(a)
```

ES6 introduces the concept of block scoping, which allows us to limit the scope
of a variable declared with `let` to a given block `{ ... }`

```js
var a = 1
{
  let a = 2
  console.log(a)
}
console.log(a)
```

You're more likely to see `let` declarations inside an `if` or `for` block:

```js
for(var i = 0; i < 10; i++){
  console.log(i)
}
console.log("outside loop:", i)

// versus

for(let i = 0; i < 10; i++){
  console.log(i)
}
console.log("outside loop:", i)
```

ES6 introduces another keyword for declaring variables: `const`

`const` is an identifier for variables that won't be reassigned:

```js
const a = 1
a = 2
// Throws an error in chrome
const a = 2
// throws an error
var a = 2
// throws an error
```

### You do: Block Scope Exercises

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/01-var-let-const.js
1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/02-const-complex.js

### Spread operator

The spread operator `...` allows an expression to be expanded into multiple elements.

This is useful for separating an array into individual elements:

```js
var dimensions = [10, 5, 2]
var volume = function(height, width, length){
  return height * width * height
}
volume(...dimensions)

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

### Default parameters

Remember default parameters from Ruby, now we can do something similar in JavaScript!

```js
function hello( name = "stranger"){
  console.log("Hello, " + name)
}

hello()
hello("Jesse")
```

#### You do: Default Parameters Practice

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/04-default-parameters.js
1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/05-default-parameters.js

### Destructuring

Destructuring assignment makes it possible to extract data from complex data
types (arrays and objects) into distinct variables:

```js
let [a,b] = [1,2]
let nums = [1,2,3,4,5]
let [first, second, ...thirdfourthfifth] = nums
```

This also applies to objects:

```js
var user = {
   id: 1,
   name: "Bob",
    age: 43 ,
   profile_url:  "http://api.co/users/1"
}

// ES5
function getUserInfo (user) {
     return $.getJSON(user.profile_url)
}

// In ES6 becomes

function getUserInfo ({ profile_url })  {
  return $.getJSON(profile_url)
}
```

#### You do: (De)Constructing Practice

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/06-deconstruction.js

### Concise properties and methods

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

And for properties where the key is the same as the value:

```js
let x = 1
let y = 2
let obj = {x:x, y:y}

// vs

let obj = {x,y}
```

#### You do: Concise methods and properties practice

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/07-concise-properties-and-methods.js

### getters and setters

Getters and setters in ES6 are very similar to getters and setters in Ruby classes,
but allow us to define pseudo-properties on objects.

Consider the following example:

```js
let person = {
  firstName: "Jesse",
  lastName: "Shawl",
  get fullName(){
    return this.firstName + " " + this.lastName
  },
  set fullName(fn){
    var names = fn.split(" ")
    this.firstName = names[0]
    this.lastName = names[1]
  }
}
person.fullName = "j dog" // notice no parentheses
```

#### You do: Getters and Setters

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/08-getters-setters.js

### template literals

Remember string interpolation from ruby? We've been able to semi-accomplish this
with string concatenation in javascript:

```js
var name = "Inigo Montoya"
var killee = "father"
var prepareTo = "die"

console.log("Hello. My name is "+ name + ". You killed my " + killee +". Prepare to " + prepareTo)
```

In ES6, we can interpolate variables using template literal syntax: `\``

```js
let name = "Inigo Montoya"
let killee = "father"
let prepareTo = "die"

console.log(`Hello. My name is ${name}. You killed my ${killee}. Prepare to ${prepareTo}`)

```

#### You do: Template Exercises

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/09-templates.js
1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/10-templates.js

### arrow functions

Arrow functions are a new shorthand syntax for defining anonymous functions:

```js
let foods = ["pizza","mac n cheese","lasagna"]
foods.forEach( food => console.log(`I love ${food}`) )

// vs the old

foods.forEach(function(food){
  console.log("I love " + food)
})
```

If there is more than one argument to the anonymous function, wrap
them in parens:

```js
let foods = ["pizza","mac n cheese","lasagna"]
foods.forEach( (food,i) => console.log(`My #${i} favorite food is ${food}`) )
```

Arrow functions also have the benefit of not changing the value of `this`:

```js
function Person(){
  this.age = 0
  setInterval(function(){
    this.age++ // doesnt work because this is GLOBAL
  }, 1000)
}

var bob = new Person()

// vs ES6

function Person(){
  this.age = 0
  setInterval(() => {
    this.age++
  }, 1000)
}

var bob = new Person()
```

#### You do: Arrow functions

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/11-arrow-functions.js

## Classes

Classes in ES6 are defined as syntactical sugar on top of the existing prototypal
interface we've worked with:

```js
function Animal(name){
  this.name = name 
}
Animal.prototype.speak = function(){
  console.log("my name is " + this.name)
}

function Dog(name){
  this.name = name
}
Dog.prototype = new Animal()

var lassie = new Dog("lassie")
lassie.speak()
```

and the es6 version:

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}

var lassie = new Dog("lassie")
```

#### You do: Class exercises

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/12-classes.js
1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/13-classes.js
1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/14-classes.js

## Modules

We have seen modules with `export` and `require` like so:

```js
// routes.js

module.exports = {
  index: function(){
    console.log("index route")
  }
}

// app.js

var routes = require("./routes.js")
routes.index()
```

ES6 introduces named imports and exports, which allow us to import functions and
objects with a particular name:

```js

// routes.js

export function index(){
  console.log("index route")
}
export function show(){
  console.log("show route")
}

// app.js

import {index, show} from 'routes'
index()
show()

// or...

import * as routes from 'routes'
routes.index()
routes.show()
```

A quick cheat sheet:

```js
//Import an entire module's contents. This inserts myModule into the current scope, containing all the exported bindings from "my-module.js".
import * as myModule from "my-module"

// Import a single member of a module. This inserts myMember into the current scope.
import {myMember} from "my-module"

// Import multiple members of a module. This inserts both foo and bar into the current scope.
import {foo, bar} from "my-module"

//Import a member with a more convenient alias. This inserts shortName into the current scope.
import {reallyReallyLongModuleMemberName as shortName} from "my-module"

// Import multiple members of a module with convenient aliases.
import {reallyReallyLongModuleMemberName as shortName, anotherLongModuleName as short} from "my-module"

// Import an entire module for side effects only, without importing any bindings.
import "my-module"
```

## Legacy Browser Support

Support for ES6 is great! - https://kangax.github.io/compat-table/es6/

If you need to support a legacy browser, check out the following tools:
- [Traceur](https://github.com/google/traceur-compiler/wiki/Getting-Started)
- [Babel](https://babeljs.io/)

## Resources

- [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS/tree/master/es6%20%26%20beyond)
- https://www.sitepoint.com/joys-block-scoping-es6/
- https://coryrylan.com/blog/javascript-es6-class-syntax
- http://www.2ality.com/2015/01/es6-destructuring.html
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes