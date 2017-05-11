# Default Parameters Exercise

Each of the below code snippets will come with a prompt. It is your job to update the code snippet so that prompt is satisfied. Your answer must leverage what you just learned about default parameters.

The prompts will indicate which lines of code you cannot modify and/or touch. You are not restricted, however, from adding code to the existing code snippets.

#### 1

Complete the function `saySomething` below so that it takes three parameters: `greeting`, `firstName` and `lastName`.
- If no parameter is passed in for `firstName`, it should be set to "John"
- If no parameter is passed in for `lastName`, it should be set to "Smith"

```js
function saySomething(){

}
```

#### 2

Remove `|| "Home"` from the `myRide` object's `driveTo` method. Then update the code so that the two `myRide.location` statements still return their respective current values.

```js
const myRide = {
  make: "Ford",
  model: "Model T",
  year: 1959,
  location: "the Office",
  driveTo: function ( place ) {
    this.location = place || "Home"
  }
}

// You cannot move or modify anything below this line.

myRide.driveTo("Work")
myRide.location
// => "Work"     

myRide.driveTo()        
myRide.location
// => "Home"        
```

#### 3

<!-- Create a question that has students invoke a function as a default argument -->
