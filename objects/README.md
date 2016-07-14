# Objects

We can understand Javascript as an object based language.

### Objects are dynamic

Creating an object is as easy as writing `{}`. An object is, roughly, a key-value structure where *keys* can be **names**, **strings** or **numbers** and *values* can be any valid structure.
```
var object = {}
var object_built_with_name = {name: 'this is a name'}
var object_built_with_string = {'name': 'this is a string'}
var object_built_with_number = {0: 'this is a number'}

object.name // undefined
object_built_with_name.name // 'this is a name'
object_built_with_string.name // 'this is a string'
object_built_with_number.name // 'this is a number'
```

You can also create an object with [the "new" keyword](http://stackoverflow.com/questions/1646698/what-is-the-new-keyword-in-javascript). For example `var new_object = new Object();` or `var new_object = new Object;`. This last sentence may sound weird to non javascript developers. See [binding "this" keyword]() #TODO

We may augment the object with new properties/methods dynamically. For non "name" keys, they should be wrapped into brackets. If the property already exists, it will be updated

```
var object = {}
object.name = 'dynamically created property'
object['string ^name*$'] = 'string properties can have just any character in it.'
object[0] = 'number keys should be wrapped into brackets also'
object[0] = 'now I override old property with this text'
```

Updating has also [some peculiarities]() that come with prototype inheritance. #TODO

### (Nearly) everything is an object.

Well, this is really not true. In JavaScript there are 5 primitive types: `undefined`, `null`, `boolean`, `string` and `number` that definitely are not objects. But they act as so [in certain circumstances](https://javascriptweblog.wordpress.com/2010/09/27/the-secret-life-of-javascript-primitives/).

```
var aBoolean = true;

// booleans have methods
aBoolean.toLocaleString() // "true"

// you can add properties dynamically to booleans, but they won't be saved
aBoolean.newMethod = function() {console.log("newMethod")}

// but...
aBoolean.newMethod // undefined
```

In a nutshell, you can create a "boolean object" that "inherits" from "boolean", and so act as an object that have boolean properties and the flexibility of objects.

```
var aBoolean = new Boolean(true);

// "booleanic" objects have methods
aBoolean.toLocaleString() // "true"

// and dynamic properties/methods
aBoolean.newMethod = function() {console.log("newMethod")}
aBoolean.newMethod // "newMethod"

aBoolean.newProperty = "new property";
aBoolean.newProperty // "new property"
```



- _Reference_: Always passed by reference, never copied
- _Prototype_: Prototype chain. Linking retrieval. **Delegation**
- _Reflection_: hasOwnProperty
- _Enumeration_: for in // for + array of properties
- _Delete_: will never touch prototype(test), and will reveal elements hidden in the prototype chain. In arrays, use slice.
- _Global Abatement_: Use var MYAPP, CommonJS or AMD
- _Loose typing_: typeof
- _Arrays as an "integer key" object_ no typeof Array
- _Variable Hoisting_
