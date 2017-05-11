# Destructuring Exercise

The `detectCollision` function below searches through an array of rectangles and
returns the first rectangle that the given point is inside of.

Use destructuring to make this code cleaner.

You might also want to use the new array method `.find`, which takes a function as argument and returns the first element in the array for which the function returns true.

> Resource: [`.find` documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find?v=example)

```js
function detectCollision(objects, point) {
  for (let i = 0; i < objects.length; i++) {
    let object = objects[i]
    if (point.x >= object.x && point.x <= object.x + object.width &&
        point.y >= object.y && point.y <= object.y + object.height)
      return object
  }
}

const myObjects = [
  {x:  10, y: 20, width: 30, height: 30},
  {x: -40, y: 20, width: 30, height: 30},
  {x:   0, y:  0, width: 10, height:  5}
]

console.log(detectCollision(myObjects, {x: 4, y: 2}))
```

#### Bonus

Use a higher-order function (e.g., `.filter`, `.map`, `.forEach`) to further clean up the code.
