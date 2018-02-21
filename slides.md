# web team
### `<ReactWorkshop />`

---

# JavaScript
### a quick crash course

***

# Objects and Functions

- Objects in JavaScript specified with `{}`
- Objects describe key-value mappings with `key: value,`
- Keys can map to _any_ kind of value
  - `Number`, `String`, `Object`, `Function`, `Array`, etc.

```javascript
var car = {
  gas: 30,
  drive: function() {
    console.log("Beep!");
  },
  name: "Ethan's Car",
}
```

***

# Objects and Functions, continued

- The `this` keyword describes the callee of a function - the **object** that invokes the function

```javascript
var car = {
  gas: 30,
  drive: function(miles) {
    this.gas = this.gas - miles / this.mpg;
  },
  mpg: 16,
  name: "Ethan's Car",
}
```
<!-- .element: class="fragment" -->

***

# Closures
- JavaScript specifies _functional_ scope

```javascript
function a() {
  var x = 3;
}

console.log(x); // x is undefined

```

***

# Revisiting `this`

- `this` is the caller of a function, always

```javascript
var x = {
  y: function() {
    console.log(this);
  },
  z: 10
};
x.y();
```

- What does `x.y()` output?

<!-- .element: class="fragment" -->

```javascript
> { y: [Function], z: 10 }
```
<!-- .element: class="fragment" -->

***

# Revisiting `this`, continued

- How about this one?

```javascript
var x = {
  y: function() {
    console.log(this);
  },
  z: 10
};
var huh = x.y;
huh();
```
<!-- .element: class="fragment" -->

```javascript
> [Window global]
```
<!-- .element: class="fragment" -->

***

# ES6 Primer

- JavaScript is growing, features are being added to the language

- Arrow Functions

```javascript
var sum = (a, b) => {
  return a + b;
}

// or more succinctly:
var sum = (a, b) => a + b;

```
<!-- .element: class="fragment" -->

***

# ES6 Classes

```javascript
class Car {
  constructor(name) {
    this.name = name;
    this.gas = 30;
    this.mpg = 15;
  }

  drive(miles) {
    this.gas -= this.mpg / miles;
  }
}

```
<!-- .element: class="fragment" -->

***

# More ES6 features (what is `...` ???)

- Object Destructuring

```javascript
var x = { y: 3, z: "hello" };
var { y, z } = x;
```
<!-- .element: class="fragment" -->

- Spread Operators

```javascript
var arr = [1, 2, 3, 4];
var sum = (...args) => args.reduce((v, c) => v + c);
```
<!-- .element: class="fragment" -->

***

# Even more ES6 Features

- Template strings

```javascript
var sayHappyBirthday = (name) => `Happy birthday, ${name}!`;
```
<!-- .element: class="fragment" -->

- `let` and `const` - block scope

```javascript
if (true) {
  let x = 5;
}
console.log(x); // undefined
```
<!-- .element: class="fragment" -->

- [See all of the ES6 features](https://github.com/lukehoban/es6features)
<!-- .element: class="fragment" -->

---

# A brief history
### From AJAX to $ to React

***

# What is AJAX?

- Asynchronous JavaScript and XML
<!-- .element: class="fragment" -->

- Used to request resources over HTTP, without a page reload
<!-- .element: class="fragment" -->

```javascript
var request = new XMLHttpRequest();
request.onreadystatechange = function() {
  if (request.readyState === XMLHttpRequest.DONE) {
    console.log(httpRequest.responseText);
  }
};
request.open('GET', 'https://1crb6kfpove4.runkit.sh/status', true);
request.send();

```
<!-- .element: class="fragment" -->

***

# AJAX and the DOM

- An idea: send an AJAX request and place it _into_ our page

```javascript
var status = document.querySelector('#status');
request.onreadystatechange = function() {
  if (request.readyState === XMLHttpRequest.DONE) {
    status.innerHTML = request.responseText;
  }
};
```
<!-- .element: class="fragment" -->

***

# AJAX and DOM string templates

- A better idea: send an AJAX request and generate elements that get placed into our page

```javascript
function generateStatusBar(status) {
  return "\
    <div class='status'>\
      <h1>" + status + "</h1>\
    </div>\
  ";
}

$("body").append(
  $(generateStatusBar(request.responseText))
);

```
<!-- .element: class="fragment" -->


- `$` is jQuery, a tool for making selecting DOM nodes and manipulating them _way easier_

<!-- .element: class="fragment" -->

***

# This gets messy!

- Managing a bunch of different `generateAnotherComponent(withParam1, withParam2)` across different files (or one huge one), for every single dynamic component you need, is bad
<!-- .element: class="fragment" -->

- We need a way to create **stateful components** in an HTML page and render their data dynamically
<!-- .element: class="fragment" -->


***

# Enter React

- A result of the Facebook ads team - creating complex interfaces with lots of data entry is hard!

<!-- .element: class="fragment" -->


- A _composable view library_ to manage self-contained components that consume a lot of data

<!-- .element: class="fragment" -->

---

# Thinking in React

***

# Codealong!

***

# Anatomy of rendering a JSX element

```jsx
  <MyComponent
    aProp="string value for a prop"
    bProp={3} /* number value for a prop */
    cProp={(a, b) => a + b} /* function value for a prop */
    dProp={{ textAlign: 'left' }} /* object value for a prop */
  >
    {children}
  </MyComponent>
```

***

# Anatomy of a component

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      /* Set a first step for state */
    };
  }

  componentDidMount() {
    /* Do some setup */
  }

  render() {
    /* Return JSX or value */
    return (<h1>{this.props.aProp}</h1>);
  }
}
```

***

# Key lifecycle methods

- `constructor()`: Initialize state and setup the component (before mounting)

<!-- .element: class="fragment" -->

- `componentDidMount()`: Perform asynchronous actions after the component has mounted

<!-- .element: class="fragment" -->

- `render`: Return one JSX element (possibly with children) that you want to display
  - `render` should be a _pure_ function of `state` and `props`

<!-- .element: class="fragment" -->

***

# State vs. Props

- `props` are passed down from a parent and can cause a component to update

<!-- .element: class="fragment" -->

- `state` is modified within a component instance and can cause a component to update

<!-- .element: class="fragment" -->

- `state` _only_ modified with `this.setState`

<!-- .element: class="fragment" -->


***

# Exercise

Build a simple React app in CodePen that renders the weather in a user-specified city!

