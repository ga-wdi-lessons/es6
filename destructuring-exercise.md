# Destructuring Exercise

#### 1

Consider the following object...

```js
const pokemaster = {
  firstName: "Ash",
  lastName: "Ketchum",
  gymsWon: ["Pewter City", "Cerulean City", "Vermilion City"],
  currentPokemon: {
    pikachu: {
      name: "Pikachu",
      type: "Electric",
      weaknesses: ["Ground"]
    },
    squirtle: {
      name: "Squirtle",
      type: "Water",
      weaknesses: ["Electric", "Grass"]
    },
    charmander: {
      name: "Charmander",
      type: "Fire",
      weaknesses: ["Ground", "Rock", "Water"]
    }
  }
}
```

Store the following values located in the above `pokemaster` object into variables, with names of your choice. Each prompt must be completed on one line and using array/object destructuring...
- "Ash" and "Ketchum"
- "Pewter City" and "Cerulean City" (found in `gymsWon` array)
- The entire `pikachu` and `squirtle` objects
- "Electric" and "Grass" (found in `squirtle` object)

#### Bonus I

The `detectCollision` function below searches through an array of rectangles and
returns the first rectangle that the given point is inside of.

Use destructuring to make this code cleaner.

You might also want to use the new array method `.find`, which takes a function as argument and returns the first element in the array for which the function returns true.

> Resource: [`.find` documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find?v=example)

```js
function detectCollision(object, point){
  if(point.x >= object.x && point.x <= object.x + object.width &&
    point.y >= object.y && point.y <= object.y + object.height){
    return true
  } else {
    return false
  }
}

const myObjects = [
  {x:  10, y: 20, width: 30, height: 30},
  {x: -40, y: 20, width: 30, height: 30},
  {x:   0, y:  0, width: 10, height:  5}
]

testPoint = {x: 4, y: 2}

for(let i = 0; i < myObjects.length; i++){
  let didCollide = detectCollision(myObjects, testPoint)
  if(didCollide){
    console.log("There was a collision!")
  } else {
    console.log("There was not a collision.")
  }
}
```

#### Bonus II

Use a higher-order function (e.g., `.filter`, `.map`, `.forEach`) to further clean up the code in Bonus I.
