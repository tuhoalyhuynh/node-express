# node-express

Start by initializing your repo in command line using:
```text
npm init
```
or
```text
npm init -y
```
This creates a `package.json` in your directory

Create an `index.js` file if you don't already have one.

Add in functions

```js
let name = "Tu Hoa Huynh";
console.log(name);

function printName(person) {
    return `Hello, ${person}`;
}
```

View in command line using:
```text
node index.js
```

Create a `myModule.js`

Add in functions to `myModule.js`

```js
const beBasic = () => "That's so fetch!";

function add(num1, num2) {
    return num1 + num2;
}

function subtract(num1, num2) {
    return num2 - num1;
}

module.exports = {
    beBasic,
    add,
    subtract
}
```

The last few lines allow functions in modules to be exported from `myModules.js`

Add the following code to `index.js`
```js
const { add, subtract } = require("./myModule");

console.log(add(5, 50));
console.log(subtract(10, 20));
```

The top line allows you to call the functions within the object from `myModule.js` to `index.js`

The purpose of this is to separate functions from your `index.js` and only have logic in your index
