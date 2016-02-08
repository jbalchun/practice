<snippet>
  <content>
# Algos
- Arrays and strings
- Backtracking/ State games
- BFS/DFS, problems solved w/ stack/queue + while loops, also memoization
- Binary Trees, traversals etc.
- Bit Manipulation magic
- Dynamic Programming (emphasis on bottom up/tabulation)
- Graphs, connectivity, topsort, BFS and DFS.
- Implementation drills. Classic sorts and implementations for reference
- Recursive collections, permutations, combinations, exponential problems.

## Arrays and strings

## Backtracking/ State games

## BFS/DFS, problems solved w/ stack/queue + while loops, also memoization

## Binary Trees, traversals etc.

## Bit Manipulation magic

## Dynamic Programming (emphasis on bottom up/tabulation)

## Graphs, connectivity, topsort, BFS and DFS.

## Implementation drills. Classic sorts and implementations for reference

## Recursive collections, permutations, combinations, exponential problems.

#JS/FrontEnd

- AngularJS
- Html/Dom
- Css
- JS
- React
- Rest/Ajax

## AngularJS

## Html/Dom

## Css

## JS, closures and syntax

### Functional Aspects: Currying, partial application etc
#### Partial application and currying
 http://benalman.com/news/2012/09/partial-application-in-javascript/
##### Functions invoking functions
- More specific functions can utilize more general functions as a wrapper.
- Manually invoke both and utilize
```javascript
// More general function.
function add(a, b) {
  return a + b;
}

add(1, 2);  // 3
add(10, 3); // 13

// More specific functions.
function addOne(b) {
  return add(1, b);
}

addOne(2);  // 3
addOne(3);  // 4

function addTen(b) {
  return add(10, b);
}

addTen(2);  // 12
addTen(3);  // 13
```
##### Functions returning functions

- Factory pattern can be used to make a function that does something specific
- Pass in a variable that gets stuck (via closure?) to return function upon instantiation, then
call the next argument
```javascript
function makeAdder(a){
  return function(b){
   return a+b;
  }
}

var addOne = makeAdder(1);
addOne(2);  // 3
```

##### Functions accepting functions
- Here bindFirstarg takes a function and the returned factory function can then return that output
```javascript
function bindFirstArg(fn, a) {
  return function(b) {
    return fn(a, b);
  };
}

function add(a, b) {
  return a + b;
}

var addOne = bindFirstArg(add, 1);
addOne(2);           // 3
```
-You can then bind this function to itself! and create an even more generic structure.
```javascript
// More specific function generator.
//Returns a function(){ return bindFirstArg(add,b)}
//    That returns a function add(a,b);

var makeAdder = bindFirstArg(bindFirstArg, add);

// More specific functions.
var addOne = makeAdder(1);
addOne(2); // 3
```

##### Partial application
- Taking a function that accepts arbitrary number of arguments, binding values to one or more of these arguments, returning a new function that accepts the unbound arguments
- The `arguments` object is array like, zero indexed + length, but not all methods. Need to use call(slice) to make an array
- This is nuanced.. you need to slice both arguments and concatenate them in theh return statement, applied as an array

```javascript
function partial(fn /*, args...*/) {
  // A reference to the Array#slice method.
  //Need to truly think of functions as objects, can hold/use them, not like java
  var slice = Array.prototype.slice;
  // Convert arguments object to an array, removing the first argument.
  // Note: arguments still has the first on it, even though fn is in the signature. double defined..
  var args = slice.call(arguments, 1);

  return function() {
    // Invoke the originally-specified function, passing in all originally-
    // specified arguments, followed by any just-specified arguments.
    return fn.apply(this, args.concat(slice.call(arguments, 0)));
  };
}
```
- Implementation of partial
```javascript
// Add all arguments passed in by iterating over the `arguments` object.
  //basic use of arguments, easy to make a function that takes any number of args.
function addAllTheThings() {
  var sum = 0;
  for (var i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }
  return sum;
}

addAllTheThings(1, 2);            // 3
addAllTheThings(1, 2, 3);         // 6
addAllTheThings(1, 4, 9, 16, 25); // 55

// Here, because of partial's signature, it knows the first argument is fn.
// fn is applied, like fn.apply(this, args(concat(slice.call(arguments,0)));
//
var addOne = partial(addAllTheThings, 1);
addOne()                          // 1
addOne(2);                        // 3
addOne(2, 3);                     // 6
addOne(4, 9, 16, 25);             // 55

var addTen = partial(addAllTheThings, 1, 2, 3, 4);
addTen();                         // 10
addTen(2);                        // 12
addTen(2, 3);                     // 15
addTen(4, 9, 16, 25);             // 64
```
##### Partial application from the right
- You can take the arguments in any order and mess with how the function returns




### IIFE's
http://benalman.com/news/2010/11/immediately-invoked-function-expression/
- This example really sums it all up, variable i is hidden, can only be operated on through its methods
- Known as the "module pattern"
```javascript
  // Create an anonymous function expression that gets invoked immediately,
  // and assign its *return value* to a variable. This approach "cuts out the
  // middleman" of the named `makeWhatever` function reference.
  //
  // As explained in the above "important note," even though parens are not
  // required around this function expression, they should still be used as a
  // matter of convention to help clarify that the variable is being set to
  // the function's *result* and not the function itself.

  var counter = (function(){
    var i = 0;

    return {
      get: function(){
        return i;
      },
      set: function( val ){
        i = val;
      },
      increment: function() {
        return ++i;
      }
    };
  }());

  // `counter` is an object with properties, which in this case happen to be
  // methods.

  counter.get(); // 0
  counter.set( 3 );
  counter.increment(); // 4
  counter.increment(); // 5

  counter.i; // undefined (`i` is not a property of the returned object)
  i; // ReferenceError: i is not defined (it only exists inside the closure)
```


## React, redux etc

## Rest/Ajax











</content>
</snippet>