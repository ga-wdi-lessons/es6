# Arrow Functions Exercise

Each of the below code snippets will come with a prompt. It is your job to update the code snippet so that prompt is satisfied. Your answer must leverage what you just learned about arrow functions.

The prompts will indicate which lines of code you cannot modify and/or touch. You are not restricted, however, from adding code to the existing code snippets.

#### 1

Update this code snippet so that it uses arrow functions wherever possible.

```js
function createUser(name, password, permissions)
  return {
    name: name || null,
    password: password || "ilovepuppies999",
    permissions: permissions || [],
    updatePassword(newPassword){
      this.password = newPassword || "password"
    },
    addPermission(newPermission){
      this.permissions.push(newPermission)
    },
    autoPost(){
      setInterval(function(){
        console.log(`${this.name}'s Status: learning ES6 right now and it is rad.`)
      }, 1000).bind(this)
    }
  }
}

const adrian = createUser("Adrian", "awesomepassword311")
adrian.autoPost()
// => Should print out `"Adrian's Status: learning ES6 right now and it is rad."` every second
```

> If you have extra time, find other ways you can ES6-ify the above code snippet

#### 2

In `script.js` file, define an event listener that is triggered when a user clicks on the button in `index.html` file. When clicked, the button text (i.e., "Click Me!") should be printed to the console.

Some additional requirements...
- The listener's callback function must be an arrow function
- You cannot hardcode the "Click Me!" string into your solution.

> Hint: you will need to leverage [something you learned about](https://github.com/ga-wdi-lessons/js-events-callbacks#the-event-object) in preparation for the Pixart homework...
