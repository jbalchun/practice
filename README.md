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
*More specific functions can utilize more general functions as a wrapper.
 *Manually invoke both and utilize
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


## React, redux etc

## Rest/Ajax











</content>
</snippet>