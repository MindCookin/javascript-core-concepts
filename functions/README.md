# Functions

> _"The best thing about Javascript is its implementation of functions. It got almost everything right. But, as you ahould expect with Javascript, it didn't get everything right."_ Douglas Crockford

### function are objects

Functions in Javascript are just like any other JS Object. They inherit from `Function.prototype` (who also inherit from `Object.prototype`).

### invocation and `this` keyword

When executing a function _as is_ (Function Invocation Pattern) `this` keyword is bind to the global object.

When the function is stored as an object's property, we will execute the function _as a method_ (Method Invocation Pattern). Then `this` is bound to the object at invocation time

When a function is invoked with the `new` prefix, then a new object is created (with a hidden link to the function's prototype) and `this` will be bound to that new object. This is the Constructor Invocation Pattern

> There are some drawbacks with the Constructor Invocation Pattern #TODO

When a function is invoked with `apply` or `call`, you can choose the `this` binding at execution time.

### binding `this`

You may create a function instance binding `this` dynamically at execution time. This is particularly useful with callback functions. It is important to notice that a new instance of the function will be created when executing bind.
