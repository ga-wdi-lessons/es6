# Template Literals Exercise

Each of the below code snippets will come with a prompt. It is your job to update the code snippet so that prompt is satisfied. Your answer must leverage what you just learned about template literals.

The prompts will indicate which lines of code you cannot modify and/or touch. You are not restricted, however, from adding code to the existing code snippets.

#### 1

Given the data in the code snippet below, use a template string to produce the
following string...

```text
There are 4 people on the tooling team.
Their names are Jennie, Ronald, Martin, Anneli.
```

Make sure the numbers, names, and team name actually come from the data. They should not be hardcoded into the `message` variable.

```js
const teamName = "tooling"
const people = [{name: "Jennie", role: "senior"},
                {name: "Ronald", role: "junior"},
                {name: "Martin", role: "senior"},
                {name: "Anneli", role: "junior"}]

let message = YOUR_CODE_HERE

console.log(message)
```

> [Source](http://marijnhaverbeke.nl/talks/es6_falsyvalues2015/exercises/#The_tooling_team)
