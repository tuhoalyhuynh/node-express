# node-express

## My First Node Project

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

## npm Adventures

Installing `npm` packages.

To install `nodemon` globally with terminal:
```text
npm install -g nodemon
```
Nodemon allows us to see live updates to our node projects. It runs a new instance everytime we make changes and save our `index.js`

Next, we installed a package locally using terminal.
```text
npm install moment
```

Moment is an `npm` package used for dates and times. After we install a local package, we have to create a `.gitignore` file and put `node_modules` in it. THe reason we do this is so that when we do a push, the local packages and it's associated files aren't pushed to our repository. All modules used will appear in our `package.json` under dependencies.

After this is done, make sure to add a require for your package before using it

```js
const moment = require("moment");

const today = moment();
console.log(today.format("dddd"));

const oneMonthFromNow = moment().add(1, "month")
console.log(oneMonthFromNow.format("Do MMMM YY"))
```

## Node Modules Practice

`fork` and `clone` to our local machines and initialize our node project using:
```text
npm init -y
```
This initializes our node project with defaults and creates a `package.json`. Then we create our `index.js` and our `myModule.js` files and start coding

First, we create an array and function in `myModule.js` to use inside `index.js`
```js
const favFoods = ["sushi", "pizza", "ramen", "steak"]

function printFoods (array) {
    for (let i = 0; i < array.length; i++) {
        console.log(array[i])
    }
}

module.exports = {
    favFoods,
    printFoods,
}
```
The above goes into the `myModule.js` and the following goes into the `index.js`
```js
const { favFoods, printFoods } = require("./myModule")

printFoods(favFoods)
```
This has the requires necessary to print my favorite foods.

Next we start working with npm packages so we need to create a `.gitignore` and add `node_modules` to it. I'll be using three different packages so we'll install them all at once.
```text
npm install distance-from
npm install convert
npm install chalk
```
Distance-from calculates distance between two coordinates. Convert allows for quick unit conversions. and chalk allows you to chain and nest styles as needed.

Let's add in requires for all three packages.
```js
const distFrom = require("distance-from");
const { convert } = require('convert');
const chalk = require('chalk');
```
First we'll use distance from:
```js
const boston = [42.3601, -71.0589];
const atlanta = [33.7490, -84.3880];
const seattle = [47.6062, -122.3321];
const losAngeles = [34.0522, -118.2437];

const bostonAtlanta = distFrom(boston).to(atlanta).in('mi');
const bostonSeattle = distFrom(boston).to(seattle).in('km');
const bostonLosAngeles = distFrom(boston).to(losAngeles).in('mi');

console.log(`The distance between Boston and Atlanta is ${bostonAtlanta.toFixed(2)} miles`);
console.log(`The distance between Boston and Seattle is ${bostonSeattle.toFixed(2)} kilometers`);
console.log(`The distance between Boston and Los Angeles is ${bostonLosAngeles.toFixed(2)} miles`);
```
The above code will console log the distances between those cities using their longitude and latitude for coordinates.

Next up, convert:
```js
const tempFahrenheit = 52;
const elevationFeet = 141;
const weightPounds = 150;

const tempCelsius = convert(52).from('fahrenheit').to('celsius');
const elevationMeters = convert(141).from('feet').to('meters');
const weightKilograms = convert(150).from('pounds').to('kilograms');

console.log(`It is ${tempFahrenheit} degrees fahrenheit or ${tempCelsius.toFixed(2)} degrees celsius in Boston right now`);
// turns out the conversion from fahrenheit to celsius is wrong
console.log(`Boston is ${elevationFeet} feet or ${elevationMeters.toFixed(2)} meters above sea level`);
console.log(`${weightPounds} pounds is equivalent to ${weightKilograms.toFixed(2)} kilograms`);
```
As the commented out line says: I think the conversion for fahrenheit to celsius is wrong. I'll have to go back and check.

And chalk!
```js
console.log(chalk.blue('Hello!'))

const go = chalk.green;
const slow = chalk.yellow;
const stop = chalk.red;

console.log(stop('On your mark'), slow('Get set'), go('Go!'))
```
# Hello Express

First we make our repository, `fork`, and `clone`. Then we `cd` into our directory and initialize our Node project
```text
npm init -y
```
Here, we will be installing express locally
```text
npm i express
```
Check to make sure we have (create one if we don't yet) an `index.js` and `.gitignore`. Lets start coding
```text
code .
```
First, we will import our Express module
```js
const express = require('express');
const app = express();
```
Now we will create our express app
```js
app.get('/', function(req, res) {
    res.send('Hello!');
});

app.listen(8000);
```
The app will "listen" on our localhost, port 8000 for requests and respond with 'Hello!'


# Hello Express - Continued

Continuing our previous work with express. We learn to use routes and send different types of responses. Let's make a directory `views` and an `index.html`, `about.html`, and `blog.html`


```js
app.get('/', function(req, res) {
    res.sendFile(__dirname+'/views/index.html');
});

app.get('/about', (req, res) => {
    res.sendFile(__dirname+'/views/about.html');
});

app.get('/blog', (req, res) => {
    res.sendFile(__dirname+'/views/blog.html');
});
```
With the above code. We can send back HTML code when there are requests to those routes.

Next, we learn to use a template engine, EJS. We just need to install using:
```text
npm install ejs
```
Now, we go back into our `index.js` and add the following to above our code:
```js
app.set('view engine`, `ejs`);
```
