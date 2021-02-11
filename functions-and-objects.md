## What is this?
This is *Yet Another Javascript Guide: a quick guide to Javascript functions and objects*. The intended audience is somebody who knows a language like Ruby or Python and has somehow avoided learning Javascript, yet found themselves working on a Javascript project. This is the *Cliff's Notes* for Javascript. This is for cramming, for all-nighters, for people who need to get things done.

This guide will demonstrate how to declare functions, pass arguments in functions, and use the arguments inside a function. It will also explain the basics of a Javascript object. Hopefully, this information will help to understand how destructuring works when you want to pass an object into a function. Destructuring is a common pattern in present-day Javascript projects, like React or Gatsby or ExpressJS.

## Contents
- [Define a function that says hello](#define-a-function-that-says-hello)
  - [breaking down sayHello: parameter and argument](#breaking-down-sayHello)
- [A function can accept different types of arguments](#a-function-can-accept-different-types-of-arguments)
  - [some examples](#some-examples)
- [Objects](#objects)
  - [Use an object as a function argument](#use-an-object-as-a-function-argument)
  - [Destructuring](#destructuring)
- [Resources](#resources)

## Define a function that says hello
```javascript
function sayHello(name) {
  return console.log(`Hello ${name}.`)
}
```

The function is named `sayHello`. It can be used like this:
```javascript
sayHello('Sylvia')
```

That will print "Hello Sylvia." in a Javascript console. You can see the code execute by [visiting this site](https://repl.it/@smcalilly/sayHello#index.js) and clicking "Run" at the top of the page. You can also open up your browser's developer tools and click `console`, then copy/paste the code into the console like you would a Ruby or Python console.

Javascript functions can be defined several different ways, using different syntax. [Here are examples of different syntaxes](https://repl.it/@smcalilly/functionDeclarationVariety#index.js) which do the same thing. This is outside of this guide, but you should at least know this variety exists. ([For further reading.](https://dmitripavlutin.com/6-ways-to-declare-javascript-functions/))

### breaking down sayHello: parameter and argument
The `sayHello` example function: 
- It has a **parameter** called `name`. The parameter can be used as a variable throughout the function. 
- "Sylvia" is passed into the function as an **argument**. In other words, `name` carries the value, or passes the message, into the function. 

[StackOverflow user 0x499602d2 said](https://stackoverflow.com/questions/12874467/what-is-the-difference-between-arguments-and-parameters-in-javascript#answer-12874546), "The parameters are the aliases for the values that will be passed to the function. The arguments are the actual values."

Basically, parameter == argument == variable == storing a value and reasoning about code.

## A function can accept different types of arguments
For the `sayHello` function's argument, I'm passing a string with the text "Sylvia". But if I wanted, I could pass any sort of Javascript [object](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes) or [primitive](https://developer.mozilla.org/en-us/docs/Glossary/Primitive), like:
- [String](https://developer.mozilla.org/en-us/docs/Web/JavaScript/Reference/Global_Objects/String)
- [Number](https://developer.mozilla.org/en-us/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [Object](https://developer.mozilla.org/en-us/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [Array](https://developer.mozilla.org/en-us/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)
- [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- etc...

### some examples
#### string
[See the string example above](#define-a-function-that-says-hello).

#### number
```javascript
function sayAge(age) {
  return console.log(`My age is ${age}.`)
}

// prints "My age is 6."
sayAge(7)
```

[Demo](https://repl.it/@smcalilly/sayAge#index.js)

#### array
```javascript
function helloFriends(friends) {
  // loop through friends
  friends.forEach(function (friend) {
    // say hello to each friend
    return console.log(`Hello ${friend}.`)
  })
}

const myFriends = ['Sylvia', 'Okie', 'Nacho']

// prints
// Hello Sylvia.
// Hello Okie.
// Hello Nacho.
helloFriends(myFriends)
```
[Demo](https://repl.it/@smcalilly/helloFriends#index.js)

#### multiple arguments
Make a function that accepts multiple arguments:
```javascript
function sayNameAndAge(name, age) {
  return console.log(`My name is ${name}. I am ${age} years old.`)
}

// prints "My name is Sylvia. I am 6 years old."
sayNameAndAge("Sylvia", 6)
```
[Demo](https://repl.it/@smcalilly/positionalArguments#index.js)

#### multiple arguments with a bug
These arguments are positional, which means that flip-flopping the arguments would create a bug:
```javascript
function sayNameAndAge(name, age) {
  return console.log(`My name is ${name}. I am ${age} years old.`)
}

// prints "My name is 6. I am Sylvia years old."
sayNameAndAge(6, "Sylvia")
```
[Demo](https://repl.it/@smcalilly/positionalArgumentsBug#index.js)

## Objects
An object is a key/value pair. The value can hold all sorts of stuff. Ruby has the hash, Python has the dictionary, and Javascript has the object. [Here is a more thorough explanation](https://javascript.info/object).

In it's most basic form, you can create an object like this:
```javascript
const kitty = {
  "name": "Sylvia",
  "age": 6
}
```

You can access the values in an object like this:
```javascript
const kitty = {
  "name": "Sylvia",
  "age": 6
}

// prints "Sylvia"
console.log(kitty.name)

// prints 6
console.log(kitty.age)
```
[Demo](https://repl.it/@smcalilly/objectValues#index.js)

### Use an object as a function argument
Create a function that uses an object inside the function:
```javascript
function sayNameAndAge(cat) {
  return console.log(`My name is ${cat.name}. I am ${cat.age} years old.`)
}

const kitty = {
  "name": "Sylvia",
  "age": 6
}

// prints "My name is Sylvia. I am 6 years old."
sayNameAndAge(kitty)
```
[Demo](https://repl.it/@smcalilly/basicObject#index.js)

Notice how the object named `kitty` does not match the expected parameter `cat` in `sayNameAndAge`. You can name your object whatever you want and pass it into the function with no problems. You just need to match the object's keys whenever you're accessing them, like `cat.name`.

### Destructuring
Destructuring is a useful way to do this, too. It looks like this:
```javascript
function sayNameAndAge({ name, age }) {
  return console.log(`My name is ${name}. I am ${age} years old.`)
}

const kitty = {
  "name": "Sylvia",
  "age": 6
}

// prints "My name is Sylvia. I am 6 years old."
sayNameAndAge(kitty)
```
[Demo](https://repl.it/@smcalilly/functionDestructured#index.js)

The important part is this: `sayNameAndAge({ name, age })`, where the brackets surround the parameters. The function essentially "unpacks" the object so that you can directly access the variables throughout the function, like this: `My name is ${name}. I am ${age} years old.`.

#### destructured with a bug
The destructured parameters must match the keys that are in the object. For example:
```javascript
function sayNameAndAge({ firstName, age }) {
  return console.log(`My name is ${firstName}. I am ${age} years old.`)
}

const kitty = {
  "name": "Sylvia", 
  "age": 6
}

// kitty.name does not match the parameter "firstName" so this has a bug
//
// prints "My name is undefined. I am 6 years old." :( poor kitty!
sayNameAndAge(kitty)
```
[Demo](https://repl.it/@smcalilly/functionDestructuredWithBug#index.js)

#### in the wild
Here's a real world example to see the two different ways of passing an object into a function. A React component might have a `props` which you use throughout your component:
```javascript
function Article(props) {
  return (
    <article>
      <h1>{props.title}</h1>
      <p>{props.body}</p>
    <article>
  )
}
```

Or, you can destructure `props` so that you don't have to use the props argument in your component:
```javascript
function Article({ title, body }) {
  return (
    <article>
      <h1>{title}</h1>
      <p>{body}</p>
    <article>
  )
}
```

## Resources
- Chapters 1 - 6 of [Eloquent JavaScript](https://eloquentjavascript.net).
- [javascript.info](https://javascript.info) for learning ES6 and for reference.
- [MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript) for reference.
