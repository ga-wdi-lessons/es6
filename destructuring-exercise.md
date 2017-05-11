# Destructuring Exercise

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
