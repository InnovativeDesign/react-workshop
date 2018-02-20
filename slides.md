# web team
### `<ReactWorkshop />`

---

# JavaScript
### a quick crash course

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

# The `this` keyword

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

# The `this` keyword, continued

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

---

# A brief history
### From AJAX to $ to React

***

# What is AJAX?

***

# jQuery and Template Strings

***

# React

---

# Thinking in React
### Lifecycle methods and state management