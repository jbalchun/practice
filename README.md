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

## Tricks/Techniques
- Check this https://www.youtube.com/watch?v=GSBLe8cKu0s
### Mods
* Modulo of a negative number works like a positive number
 * -100 Mod 8 = 4 because 8 * -13 = 104

## Arrays and strings

## Backtracking/ State games

## BFS/DFS, problems solved w/ stack/queue + while loops, also memoization

## Binary Trees, traversals etc.

## Bit Manipulation magic

## Dynamic Programming (emphasis on bottom up/tabulation)

### 6.006 Lectures

* Best way to do something, optimization
* Exhaustive search, typically polynomial time
* Careful brute force
* Subproblems + reuse the answers
* What are the subproblems?

***
#### Lecture 1
* Example 1: fibonacci, compute the nth num
 * Naive fib is exponential time
  * T(n) = T(n-1) + T(n-2) + O(1), at least 2T(n-2), ie 2^(n/2)
 * Memoized DP
  * fib(k) only recurses the first time it's called
  * Only need to call n times
  * There's a way to do lg(n) for fib fyi
 * Bottom up DP
  * Falls out of top down
  * Equivalent to a top sort of a simple DAG

* Example 2: Shortest Paths
 * Guessing: Try all, reduce to best
  * Single source shortest path from S to V
  * Must start one node away from S, or end one node away from V
   * shortest is delta from s-> u + w(u,v)
   * Minimize over all edges of shortest from s to v
   * Naively infinite over cyclic, V+E over DAGs

#### Lecture 2

* DP always reduces to a dag
* 5 Easy steps to DP!
 * Define subproblems
 * Guess (part of solution)
  * num subproblems, num choices for guess
 * Relate subproblem solutions
  * Make sure subproblems are acyclic
 * Recurse and Memoize, or Bottom up DP table
 * Solve the original problem

 ***

*Text justification,
 * Prompt:
  * Given some text, split it into "good lines"
  * Greedy is not optimal ie, as many words as you can fit
  * Text is a list of words, there's a quantity: badness(i-j)
  * badness tells you how bad it is to use words i->j as a line
   * If they don't fit, badness = Infinity
   * Otherwise = (page width - total width)^3
 * Brute Force: try all possible line breaks, 2^n
  * Guess where the second line starts?
 * Subproblems: Suffixes [i:]
  * Subprobs: n
 * Guess: Where to start 2nd line
  * At most n-i choices
 * Relation: Recurrence: DP[i] =
  * Min(
   * for j in range(i+1,n+1)
   * Dp(j) + badness(i-j)
  * For every line, min of DP
 * Topo order n -> n-1, DP(n) = 0
  * Total time: O(n^2)
 * Original Problem:
  * Solved in quadratic time
 * Hard part, what to guess and what are the subproblems
* Blackjack
 * Perfect information blackjack
 * I know the whole deck, should i hit or stand?
 * Guess: how many times should i hit
  * num of choices is n at most
 * Subproblem, suffix Ci:, max winnings given these cards onward.
 * Recurrence:
  * BJ(i) =  max(
   * outcome {-1,0,1}
   * + BJ(j) for( numHits in range(i,n)), if it's a valid play
 * Longest path in a DAG, win the most, longest edges
 * Cubic in the worst case.

#### Lecture 3

* Subproblems for strings or sequences
 * Used suffixes x[i:] n
 * Prefixes x[:i] n
 * All substrings x[i:j], n squared

* Parenthesization : Matrix multiplication
 * Optimal evaluation of associative expression
 * Col x Row x Col
  * (Col x Row) x Col = O(n^2)
  * Col x (Row x Col) = O(n)
 * Guess: last multiplication
  * If I know optimal up until that, I'm good
  * Recurse on each subproblem
 * Optimal parenthesization of Ai..Aj-1
 * Num choices for k O(j-i+1) approx O(n)
 * Recurrence:
  * DP(i,j) = min(
   * DP(i,k)+DP(k,j) + cost
   * for k in range(i+1-j)
   * time is approx O(n^3)

* Edit Distance:
 * Given two strings, x and y
 * What's the cheapest sequence of character edits to convert x into y
 * Someone can weig[ht the char edits, ie typo likeliness
 * LCS is an edit distance, insert delete = cost 1,
  * Replace is infinity if c doesn't equal c prime
 * Subproblem: x[i:] and y[j:] for all i and j
  * subproblems = n^2
 * Guess:
  * Start at first chars
  * Do one of 3 choices
 * Recurrence: DP(i to j)=min(
  * 1: Cost of replace + DP(i+1,j+1)
  * 2: cost of insert y[i] + DP (i, j+1)
  * 3 : cost of delete x[i] + DP(i+1,j)

* Knapsack
* https://www.youtube.com/watch?v=8LusJS5-AGo
 * Subproblems
  * Suffixes (arbitrary)
  * Subproblems have a remaining capacity
  * Num subproblems = O(n*s)
 * Guess: is item i in subset or not?
  * 2 choices
 * Recurrence:
  * Dp(i,x) = max(
   * DP(i+1,X)
   * DP(i+1,X-Si)+Vi))
 * Psuedopolynomial
  * Polynomial in the numbers in input


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

## JS Debounce
https://davidwalsh.name/javascript-debounce-function
* Debounce solves the issue of firing off too many events to the server on repeated calls
* Examples include autocorrect, suggestions etc.

```javascript
//debounce from underscore
function debounce(func, wait, immediate) {
	var timeout;
	return function() {
		var context = this, args = arguments;
		var later = function() {
			timeout = null;
			if (!immediate) func.apply(context, args);
		};
		var callNow = immediate && !timeout;
		clearTimeout(timeout);
		timeout = setTimeout(later, wait);
		if (callNow) func.apply(context, args);
	};
};

//This will only fire once every quarter second
var myEfficientFn = debounce(function() {
	// All the taxing stuff you do
}, 250);

```

## JS, closures and syntax
https://www.reddit.com/r/webdev/comments/3f7q3q/been_interviewing_with_a_lot_of_tech_startups_as/

### Bind, apply and call
* **Bind**
 * Creates a new function that has it's 'this' bound as the first param

```javascript
 var Button = function(content) {
   this.content = content;
 };
 Button.prototype.click = function() {
   console.log(this.content + ' clicked');
 }

 var myButton = new Button('OK');
 myButton.click();

 var looseClick = myButton.click;
 looseClick(); // not bound, 'this' is not myButton - it is the global object

 var boundClick = myButton.click.bind(myButton);
 boundClick(); // bound, 'this' is myButton
```
 * Can also preset some params like below (or all params)
```javascript
var sum = function(a, b) {
  return a + b;
};

var add5 = sum.bind(null, 5);
console.log(add5(10));
```


### Functions (general)
http://www.permadi.com/tutorial/jsFunc/index.html
* Named functions vs variable instantiation
* Named is defined at parse time, var at run time.
```javascript
<script>
  // Error
  functionOne();

  var functionOne = function() {
  };
</script>

<script>
  // No error
  functionTwo();

  function functionTwo() {
  }
</script>
```

### Functional Aspects: Currying, partial application etc

#### Partial application and currying
http://bonsaiden.github.io/JavaScript-Garden/#function.closures
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
- Left is more robust.

##### Partial application from anywhere

##### Currying
-Transform a function of n arguments into a chain of N functions w/ one argument

```javascript
function curry(fn,n){

  //use the function's length is n is left out
  if(typeof n !== 'number'){
    n = fn.length;
  }

  function getCurriedFn(prev){
    return function(arg){
      var args = prev.concat(arg);

      if(args.length < n){

      return getCurriedFn(args);
      } else {
        return fn.apply(this,args);
      }

    };

  };

  return getCurriedFn([]);
}

```
```javascript
var i = 0;
function a(arg1,arg2,arg3){
  return ++i + ': ' + arg1 + ', ' + arg2 + ', ' + arg3;
}

var b = curry(a);


```

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
## Node stuff
http://blog.modulus.io/absolute-beginners-guide-to-nodejs
* Node is not a webserver
* Not like apache, not really an HTTP server
* All it is is a javascript runtime, a way to run js on your computer
* Can run "node" and get a js shell
```
>console.log('hello')
//prints 'hello' and undefined, all return values are also logged
```
* Otherwise provide it javascript
```
 node hello.js
```
* Created a simple web server that just serves "hello world"
* If you want actual web server functionality you need to build it!
 * Can use express or koa for this
 * After `npm install express` this is enough to serve html
 ```javascript
 var express =require('express'),
 	app = express();

 app.use(express.static(__dirname + '/public'));

 app.listen(8080);
 ```
* It's sloppy to have everything in one file, which is why we have modules
 * You can include local files just like modules, via path instead of a name
* Follow up: Rest service, http://www.qat.com/simple-rest-service-node-js-express/

## React, redux etc

### Thinking in React
https://facebook.github.io/react/docs/thinking-in-react.html

* Starting w/ a mock, and some JSON data from an API call
```
[
  {category: "Sporting Goods", price: "$49.99", stocked: true, name: "Football"},
  {category: "Sporting Goods", price: "$9.99", stocked: true, name: "Baseball"}
];
```

* 1, Break the UI into a component hierarchy
 * Logically seperate out UI components, let the mock drive this
 * (might be photoshop layers)
 * Single responsibility principle, component should do one thing
 * If your model is good, it'll translate well
 * Components are nested FilterableProductTable has Searchbar, ProductRow beneath it etc
 * Example structure:
 ```
 FilterableProductTable
  SearchBar
  ProductTable
    ProductCategoryRow
    ProductRow
 ```
* 2, Implement the components statically in React
 * Sample component below:
 ```javascript
 var SearchBar = React.createClass({
   render: function() {
     return (
       <form>
         <input type="text" placeholder="Search..." />
         <p>
           <input type="checkbox" />
           {' '}
           Only show products in stock
         </p>
       </form>
     );
   }
 });
 ```
 * Now time to implement. Build a version that renders the UI from the model w/o interactivity
 * Static version: A lot of typing, no thinking
 * Interactive version: A lot of thinking, no typing
 * To build the static version:
  * Render the data via props
   * props pass data from parent to child
  * Build components top down or bottom up. Big projects = bottom up
  * Once done you'll have a library of components that only have a render method
  * Component at the top of the hierarchy takes your data model as a prop, passes props down
  * Simply change the data and call render again, changes propogate down
  * 2 types of model data in React, props and state

* 3, Identify the minimal representation of UI State
 * UI is made interactive by triggering changes to the data model via **state**
 * DRY, minimal set of mutable state
  * Ex, don't store the length of a list as a seperate variable, just calc it
  * 3 q's
   * Is it passed via props? not state
   * Does it change over time? If not, then it's not state
   * Can you compute it based on other state/props? not state
  * Final state for this simple filter list
   * Search text the user entered
   * Value of checkbox
    * NOT the filtered list, can be derived from search text and model

* 4, where should your state live?
 * Once we know the minimal state, we need to decide which component owns/mutates it
 * One way data flow down the hiearchy
 * For each piece of state:
  * Identify every component that renders something based on the state
  * Find a common owner component (A single component above all that use the state)
  * Either the common owner, or an even higher component should own that
  * If you can't find one, create a new component where it would be to hold the state.
   * In this example, the table and the search bar depend on the search text
   * Therefore one level up, FilterableProductTable (root) owns it
* 5, add the inverse data flow
 * FYI ReactLink makes this easier
 * When a user changes the form, state is updated.
 * FitlerableProductTable passes a callback to SearchBar that fires when the state is updated
 * Use onChange to be notified of it


## Rest/Ajax

## Harvard lecture 6

## Harvard lecture 7 AJAX
* XMLHttpRequest is an object
 * Has a callback function
 * Server can respond w/ XML or JSON (XML is bloated)
 * open() connection, then send()
 * readyState,(4isdone) tells you what state the request is in (sending, receiving, done)
 * responseText is what the server sent back
 * status, 200 is ok, 404 doesn't exist, 401,403 etc.
 * 4 and 200 are good!
* Same origin policy, can't just hit other web servers directly
 * Workarounds: CORE, you can use our data
 * Yahoo query language, YQL



# Systems Design

## Blueprint (Hired in Tech, url shortener as an example)

### Step 1: Constraints and use cases

- First thing you do is identify the use cases the system needs to satisfy
- Don't make assumptions when you can ask
- Url example, maybe we only serve 1000 users (urls) but these url's will get millions of hits
- Do we need to apply statistics?

#### From example video,
#### Use cases :
http://www.hiredintech.com/system-design/the-system-design-process/

-Want to brainstorm a bunch, then agree what's in scope and what's out of scope.
1) Shortening: take a url, return a shorter one.
2) Redirection: take a short url redirect to original url
3) Custom urls
4) High availability

Out of scope:
4) Analytics
5) Automatic link expiration
6) Manual link removal
7) UI vs API

#### Constraints:
- Note this is very in depth, maybe go half this deep, or twice as fast

1. How many requests per month? Scale down to second
2. How many urls per month? Scale down to second

- You may be asked to estimate (new tweets per day = 500 mil, etc, look up MAU's) .5->1bn
- Twitter users generate half a billion tweets per day, 15b tweets per month
- All shortened urls 1.5 b per month
- 80/20 rule, top 3-5 have 80 percent, rest all have 20 percent
- Somehow we are shortening 100M urls per month

****

- How many requests are we handling monthly, off that 100M?
- 20% of URL's generate 80% of traffic
- Get to 1B requests per month
- 10% from shortening, 90% from redirection
- ~400 requests per second. 40 shortens and 360 redirects
***
- **Data estimate ~5 years** 5 years x 12 months x 100M = 6bn urls in 5 years
- Bytes per url? 500. **1 byte ~ 1 char**
- Hash size for 6 billion urls? log base 62 (6bn) = only about 6 chars, 6 bytes
- 3TB for all urls, 36gb for hashes, over 5 years
- **Writes per second** 40 writes per second(shortens) * (500+6) = 20kb
- Data reads per second = 360 * 506  = 180k per second

****

#### Abstract Design:
1. Application service layer (serves requests)
..* shortening service, check if it's already hashed, make if not and return
..* redirection service,
2. Data storage layer (keeps track of hash to url mappings)
..* acts like a big hash table, stores new mappings and retrieves a value given a key

hashed_url = convert_to_base62(md5(original_url+random_salt)).slice(0,6);

#### Understanding bottlenecks:
Consider:
1. Load balancing
2. Distributed DB
3. Caching

***

Two Challenges:


1.Traffic
..* Our calls here are simple, basically just wrappers to access. Commodity hardware is ok
2. Amount of data
..* We do have a lot of data and we need to serve these url's quickly. Think harder about data!

-Bottlenecks:
-Traffic should be fine, data will be more interesting.

- **Always making tradeoffs**

#### Scalability:
- https://youtu.be/-W9F__D3oY4

Consider:
- Vertical Scaling
- Horizontal Scaling
- Caching
- Load balancing
- Database replication
- Database partitioning
- Sharding: http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html
- Scalability for dummies: http://www.lecloud.net/tagged/scalability
- Actual architectures: http://www.hiredintech.com/system-design/sample-architectures/

***

- Everything is a tradeoff
- Constraints Time, budget, knowledge, complexity, tech.

***

Back to url example:

* Stateless traffic, not that difficult
* One machine should be able to do 1 request per second, otherwise load balancer + other machine

* Application Service Layer
 * Start w/ one machine, add a load balancer + cluster over time
  * Traffic may be "spiky", load balancer let's us auto-add machines when we need them (EC2)
  * Redundant, more availability, which we had highlighted as a requirement
* Data store layer ( tougher problem to solve)
 * Billions of fairly small objects
 * No relationships between the objects
 * Reads are likely 9x more frequent than writes (360 vs 40)
 * 3 TB's of urls, 36 GB of hashes
 * NoSQL or relational? (either case is valid)
  * MySQL
   * Mature, widely used,
   * Sharding, master/slave, master/master, used by massive websites
   * Index lookups are very fast (as fast as NoSQL)
   * define tables:
    * Mappings: hash: varchar(6) original_url: varchar(512)
    * 3TB is ok for MYSQl, but lookups might be slow
     * Create a unique index on the hash (36GB+)
     * Keep index in memory
      * Option 1: Vertically scale the MySQL machine
      * 64 GB machine is about 500 a month
      * Option 2: Otherwise, partition the data, 5 partitions, 600GB of data, 8GB of indexes (shards)
       * What do you partition on? First char of hash  % no. of partitions
     * Master-slave (reading from slave, writes to master)

   ***
* Working strategy
 * Use one MySQL table w/ two varchar fields
 * Create a unique index on the hash in memory to speed lookups
 * Vertically scale MySQL machine for a while, eventually partition the data
  * Partition by taking first char of hash mod the num of partitions
 * Think about a master slave setup


***

* Wrap up, the interviewer could expand in any direction
* Try to know the basic trade offs of all of these technologies
 * NoSQL vs Relational
 * Sharding/partitioning
 * Indexing
* Steps:
 * Use Cases, priorities
 * Constraints
 * Abstract Design
 * Bottlenecks
 * Concrete Design
 * Scalability

### Harvard SQL https://www.youtube.com/watch?v=Xq5lvvBvA1U
* MySQL is a database server, install on server, service on a port
* SQLite use SQL w/o a DB, just a binary, .db, mocks a db
* Varchar uses variable space, char is locked in to definition
 * Chars are slightly faster
 * Text is for big docs etc

### Harvard PHP https://www.youtube.com/watch?v=h2Nq0qv0K8M
* PHP structured app, you hit the web server (Apache usually)
 * Web server goes to file system and gets an html/php page
 * PHP server has a plugin that reads the php code in the html file and does something with it
* PHP lecture ES75
* PHP is interpreted rather than compiled
 * Interpreted is fast development, slow execution
 * PHP can cache upcodes to speed up interpretation
 * Thousands of hit per second are when you hit the breaking point
* PHP is extremely accessible
* Create PHP blocks inside the html, dropping in and out of php mode
* When you do a $GET PHP puts them in the url
* Get VS Post
 * Post: Posted params are not in URL, data sent after header
 * Conceals arguments, some data shouldn't get logged in URL all the time
 * URLS might be too long etc.
* Forms submit to a PHP file which then handles it on the server
* XPath for traversing xml


#### Harvard Lecture
-https://www.youtube.com/watch?v=-W9F__D3oY4

* Things to consider when selecting hosting
 * VPS vs shared web host
 * VPS: your own copy of the server software (via a hyperviser)
 * VPS is a selected slice, shared hosting means resources are just sloppily shared
 * Box owner could always access your data if they want
* AWS EC2 can autoscale and build more vm's as traffic increases

* Vertical scaling:
 * Disk, RAM, CPU cycles
 * Throw money at the problem, more stuff on one machine
 * There is a ceiling to how many CPU's etc on one machine
 * 4 things at once on a quad core (duh)
  * Threads within that
 * SATA, SAS(serial attached scuzi 15k rpm), (parallel ATA is older) hard drive types
 * SSD's are generally way smaller and more expensive but performant

* Horizontal Scaling
 * Commodity hardware, a bunch of them
 * Inbound http request, but multiple web servers, which?
 * Interpose a black box, the load balancer.
  * Return IP of load balancer (public IP)
   * Servers have private IP's, the rest of the world doesn't need to see them, easier to find
  * Web servers can all be identical (uses a lot of disk space)
   * Could also be dedicated, this is images, this is videos, this is html. Load balancer decides
  * Load balancing via round robin, sequential wrapping, 1,2,3,1 etc
   * Basically a DNS server, no communication (ie no asking how busy are you?)
   * Drawbacks: get a power user on one server, they all accumulate on one server for some reason
   * OS/browsers cache DNS lookups, so that power user keeps returning
   * DNS server can give a "Time to live" for the cache value, but that might be days
   * Sessions: If our back end is PHP:
    * Load balancing breaks session super globals
    * Sessions are stored on the server, so your cookie doesn't work
    * If we diversified our servers we fine, but that doesn't provide redundancy, only works to a point* Need to keep sending Alice back to server 1 for her session. this is a problem
    * Have a file server storing session for sharing state? Sessions on the load balancer?
     * This is a weakness on our topology, everything depends on this one, no redundancy
    * Could use RAID: Redundant array of independent disks. RAID0 -> RAID10 etc
     * Assume multiple hard drives
     * RAID 0 2 HD's of identical size, write here, write there, etc, called striping
     * RAID 1 mirrors across 2 HD's, if one dies, you are good.
      * RAID 10 is 4 drives, RAID 5 and 6 are 3 or 4 drives, one is for redundancy, less overhead
     * Multiple power supplies, RAM, etc, hot swap everything.
   * Use HAProxy, ELB, Hard: Barracuda, Citrix, make load balancers: Harvard's is $20k, 100k is easy for a pair
   * Storing all info in cookies is doable, but sketchy
    * You can store which server they were sent to? Weird, exposes our structure
    * Could just have some id that the load balancer knows corresponds to a specific server
    * Protect them from spoofing cookies to generate targeted traffic
  * PHP is interpreted, so gets a bad wrap as slower
   * PHP accelerators, cache op-codes with some open source software like XCache
   * Like .py vs .pyc for python
  * Caching
   * Craigslist as an html sheet, generate a page dynamically. They are storing html
    * Apache is great at just spitting out bits from disk, static content
    * Tons of redundancy being stored, same parts of template, header footer etc.
    * Impossible to change the aesthetics of the page
   * MYSQL querycache
    * add query_cache_type = 1. Query answers are stored
    * MYSQL is a server on a ram.
   * Memcached is software on a server that let's you store anything in RAM
    * Let's all different languages hook in
    * Disk is slow, fast to serve up. Store in a table w/ indexes
    * KeyVal store, vs DB is much faster even if it's a mem database
    * If user is null in cache, you can hit the DB
    * Eventually cache is so big you can't keep it on the machine
    * GC? LRU. Memcached does this automatically
   * Inno DB? MY ISAM? Does a DB support transactions?
    * Transaction, one logical unit of work that either passes entirely or fails
    * Archive tables are compressed, so slow access but smaller, no selects
   * DB's typically offer replication
    * Master, with slaves (1 or more)
     * Slaves get a copy every time a master is changed
     * If Master dies, there are 3 identical backups, promote
     * Facebook: more read heavy than write heavy
      * Selects go to 2,3 or 4, writes go to Master 1
      * Can add more and more read servers, slaves are redundancy or read balancing
      * Still one point of failure to writes, if Master goes down, time to promote
       * Can have a Master-Master, they write back and forth to each other, or mirror
      * Potential Architecture
       * Network of clients
        * Load balancer (point of failure, can do active-active among a pair, heartbeats)
        * Web servers
         * All direct to Master(s) for writes (point of failure)
         * All to another load balancer for reads (point of failure)
          * Slaves for reading
      * Partitioning:
       * FB: Different server for each school
       * What about an A-M cluster and N-Z cluster
        * 2 load balancers, send them to a different set of slaves
      * Don't want devs to have to know anything about topology
   * Multiple datacenters
    * AWS has availability zones
     * West coast, asia, europe etc
    * DNS based load balancing
     * Send to different load balancers via DNS
    * If you have way too many users it is really hard to set up
   * Security:
    * From outside world, in: TCP: 80 in, and 443 for SSL, allow another port for SSH
    * Offload SSL to LB, keep traffic in datacenter unencrypted, just http, don't need certs on all boxes
    * Expensive load balancers handle all that
    * Web servers to DB's TCP 3306 (MYSql)
    * Need firewalls as well
    * Least-privilege


### Relational DB's

#### How Databases work
http://coding-geek.com/how-databases-work/

* Time complexity is important, O(n^2) is slow etc
* Merge sort is used by databases a lot
 * Merge sort can be done in place
 * Can run distributed on hadoop
* Can build tree indices for things if you can establish order among keys
* Range query, uses a B+ Tree
 * Only the lowest nodes store information
 * Upper nodes route, ie <80, <398, <40, etc.
 * Twice as many nodes as a normal binary tree
 * Lowest nodes are linked to their successsors
  * Query for 40 -> 100
  * Search for 40, then follow links to successors until 100, search costs M + log(N) where M is the number of successors
 * Needs to be self ordered and self balanced
  * Log(n) insertion and deletion
   * "Too many indexes is bad" because you slow down fast insertion/update/deletion
* Hash tables
 * A key
 * A hash function, to give location of bucket
 * A function to compare keys within the bucket
 *Want to spread out hashes
 * Advantages of a hash table over an array
  * Hash tables can be half loaded into memory (just keys) w/ bucket read from disk
  * Arrays use contiguous mem space (tough if large)
  * Custom keys
* Core database components
 * Process manager
  * pool of processes/threads
 * Network manager
 * File system manager (Disk I/0)
 * Memory manager. DB's have a ton of RAM to avoid disk i/o, this manages all of that
 * Security manager
 * Client Manager
* Database tools
 * Backup Manager
 * Recovery Manager
 * Monitor manager (monitor a db)
 * Administration Manager (storing table metadata, names etc)
* Query Manager
 * parser (checks validity)
 * rewriter (preoptimize)
 * optimizer (optimizes the query)
 * executor (compile and execute query)
* Data Manager
 * Transaction mngr
 * Cahce mngr
 * Data access mngr

* Aside on optimization based on Sqlite (there's a lot more detail than these notes, just some points here)
* https://www.sqlite.org/optoverview.html
 * Where clause analysis
  * Where is broken up and we check if there's any index we can use
  * Indices are useful for =, <,>, etc
  * Order matters in and statements
 * Joins
  * Some joins (inner joins) can be freely reordered, Left outer cannot be
  * Useless joins are removed
  * Joins are basically nested for loops with where clauses, so the order does matter, depends on the data.
   * Often can run ANALYZE for the db to test which join order is faster
 * Subqueries
  * Subqueries are very inefficient so the optimizer will work to flatten them into the original query

* Statistics
  * blocks of memory are 4 or 8 kb, so 1 kb will still take up 8 likely
  * Stats for each col, distinct vals, length of data, range of data
   * Example: 1000 dist first names, 1M dist last names
   * Hence, join on last name first, because it's more likely to be unique, will have to do less work
   * The heavy filtering is done on the more unique column
* Optimization
 * Cost based optimization
 * Temp indexes (dynamic)
 * Table scans are more expensive that an index scan
 * Cost of A JOIN B is not the same as B JOIN A
 * Ways to join
  * Nested loop join,
   * for each in outer table, look at all rows in inner and see if there's a match
  * Hash Join O(N+M)
   * Put all elements from inner into a hash table in mem
   * Get elemnts of outer one by one, hash each elemnt to find the bucket of the inner relation
  * Merge join
  * Selecting one of these depends on memory, size of datasets, indexes, if the result is sorted, threads etc
 * A 3 way join has to decide between all these methods at each join, and order.
  * DP, Greedy, Genetic etc can all be used to optimize this
* Data Manager
 * transactions
* Cache Manager
 * Mem is 100 - 100k times faster than disk
 * Prefetching, can read query, know which data you need and load that onto RAM, then use it sequentially from buffer to execute
 * Buffer pool of memory that is filled on an LRU basis
 * buffer /cache hit ratio is calculated.
 * LRU-K is a type of LRU
 * Write buffers also exist
* ACID
 * Atomicity: All or nothing transactions, even if it lasts 10 hours it can be rolled back
 * Isolation: If 2 transactions run at the same time, it shouldn't matter who finishes first, same result
 * Durability: once a transaction is committed, the data stays in the db no matter what
 * Consistency: Only valid data is written to the db
 * **Notes:**
 * Pure Isolation is too expensive, there are 4 levels of isolation instead
 * Serializable: (highest level of isolation) each transaction has its own world **SqLite**
 * Repeatable read: If one transaction adds new data and finishes first, the others will see it. Only see new data, old data stays the same **MySQL**
 * Read committed: See updates/inserts/deletes that are committed after repeated reads (non repeatable read) **Oracle, Postgres**
 * Read uncommitted: See intermediate, non-committed states, dirty read
* **Concurrency Control**
 * Writes on the same data cause issues
 * Running transactions one by one is too slow
 * **Solved by**:
 * Monitor all ops on all transactions
 * Check if 2 or more trans are in conflict (same data)
 * Reorder to reduce size of conflicts
 * Execute conflicting parts in a certain order while non conflicting run in parallel
 * **Locks**
 * Exclusive: if I need data anyone else that wants it can wait
 * Shared: if I need to read, I share lock, if I need to write, I wait for shared locks to end and exclusive lock
 * Deadlock detection: checking for cycles in a graph. Can timeout or precheck w/ two phase locking
 * **Data Versioning**
 * Every transaction can modify data at the same time, they each get a version of the data
 * If there's a conflict of versions, one transaction is rolled back, possibly re run


### Indexing
http://stackoverflow.com/questions/1108/how-does-database-indexing-work
http://use-the-index-luke.com/sql/anatomy/the-tree
* Data is stored in blocks on disk. These blocks are accessed in their entirety
* Structured like a linked list, a section for data and a pointer to the next node
* If a field is non unique, requires N size search
* On the other hand, a sorted field has logN access

* **What is indexing**
* Indexing is a way of sorting a number of records on multiple fields
* Example table, 4 fields amounting to 204 bytes per row, 1024/204 = 5 rows per block
```
Field name       Data type      Size on disk
id (Primary key) Unsigned INT   4 bytes
firstName        Char(50)       50 bytes
lastName         Char(50)       50 bytes
emailAddress     Char(100)      100 bytes
```
 * Searching on the id field (sorted) drops access from 500k (N/2) to 20
 * Firstname is not sorted or a key, need full table scan of 1M rows
 * Therefore we might want to create an index on this, which is basically a sorted table in mem w/ keys and pointers
 ```
Field name       Data type      Size on disk
firstName        Char(50)       50 bytes
(record pointer) Special        4 bytes
```
  * With this index, block access cuts down from 300k to 20
  * However, we need 300k blocks in memory now
  * Index is a waste of space if there are a lot of dupes
  * Also two indices on a table means a single write is 3 write operations
  * In practice indices are B Trees


### Principles of fast search

* Sharding- by splitting the database into a lot of small pieces, it is not necessary for a server to hold the entire database and search it. Instead, queries are directed to an appropriate shard by the frontend servers.
* Replication- by having the data available on thousands of servers, less waiting time is required to retrieve data. Moreover, queries can be searched in parallel and the quickest responses returned to the user.
* Caching- There are a lot of searches that are very common (e.g. "E3 2014"). Instead of looking up the results every time, the results are fetched once and cached for some period of time.
* Hardware- Retrieving data from a hard disk is slow. Google has enough servers now that they can keep the database shards in RAM instead of reading from disk.

### Scalability for Dummies

*

### Normalization, NoSQL and consitency
http://www.sarahmei.com/blog/2013/11/11/why-you-should-never-use-mongodb/
* This answer talks about some tradeoffs in denorm: http://meta.stackexchange.com/questions/120016/how-is-nosql-and-data-denormalization-used-on-stack-overflow-stack-exchange
 * key: can I avoid this query? (cache etc)
 * can I improve this query? (denorm,good sql, good tools etc)
* Commonly a SQL database can be denormed, then triggers are implemented to maintain consitency
* How Mongo works
 ![](http://www.sarahmei.com/blog/wp-content/uploads/2013/11/Screen-Shot-2013-11-09-at-7.09.27-PM.png)
 ```
  tv shows have many
	seasons have many
		episodes have many
			reviews
			cast members
 ```
* This would be a 5 table join in SQL, with a table for each object, foreign keys etc
* Mongo would model it as a set of hashes, hashMap of shows, with a hashmap of seasons, hashmap of episodes etc.
 * Some metadata at top level, then the list of the next object
* Document storage works for the above example, but it falls apart when you are repeating entities
 * A social graph for example. A user has a list of friends, but those friends are also users
 * You could represent this in Mongo, but data would be duplicated/denormalized
 * If we make a change to a user, we need to update it everywhere
 * Alternatively we could just reference keys, but then we lose the efficiency and simplicity of the document
 * Good sign the data is relational
* With Mongo, you will eventually become inconsistent, it's basically a massive cache and writes will fail
* Even with "ideal" tv case, say you want to click on an actor and look back at all of their movies
 * Still stuck w/ dupes

## Java stuff

## Tomcat/threads/JDBC

### Connection pools
* Opening a db connection is expensive, we want to do it as seldom as possible
* A connection pool automatically keeps a bunch of connections open and hands you the best(?)

### Unix stuff
* Mac vi guide: http://commandlinemac.blogspot.com/2008/12/vim.html


### My issue
* Bad:
 * Each trade was opening it's own database connection in a thread
 * The database connections were overflowing. The connections were being closed but the threads weren't
* Fix:
 * Daemon thread that just loops through all trades w/ one connection and checks, constantly.
  * Daemon doesn't prevent JVM from exiting
  * low priority etc

## Code as Craft, how to search for "Geeky"

* BROAD QUERIES
* Too many options, daunting
* Need to help surfers w/ broad queries https://codeascraft.com/2015/07/29/targeting-broad-queries-in-search/
* Developed a heuristic using basic statistics at runtime
* Simple method is performant, easy to debug, works on multiple languages
* Start by taking the percentage of items w/ the search term from each broad category (jewelery,  accessories)
 * Apply Shannon entropy
 * Entropy is a way of measuring broadness
  * If the results set is low entropy, dive into subcategory and repeat
  * Entropy values are normalized based off the number of items in the category
* Trade off between big data signals power vs architectural costs

## Code as Craft as a whole

* A lot of writing on process, engineering efficiency, training and learning
 * Dojo process article
  * Onboarding
  * In house networking
  * Knowledge transfer
  * Practice Communicating
  * Training
  * Fun/Enjoyment
* Also a lot of interesting technical analysis https://codeascraft.com/2015/07/29/targeting-broad-queries-in-search/
 * Entropy/search
 * Calculate entropy, or broadness of results, if we don't satisfy min
  * Drill down into biggest and recalculate

## Why Etsy as a product?

* Enabling creators, global connections
* Interesting problemset, scale, distributed
* High visibility, tangible payoff
* Independence, tremendous power to individuals


## Technical retrospectives

* NGO company
* Result Failed

* Initial Reaction:
 * Thought I had done well, immediately recognized the method needed to solve the problem
 * Expressed concern over my design because it was repetitive
 * Was able to reasonably refactor the design into something that worked, but not super confidently
* Likely reasons why I failed:
 * Didn't answer the clarifying question very well ( what happens if I enter the same color)
  * Really think about edge cases before acting done
 * Spoke about refactoring concerns but didn't do it without being walked through
  * If you know something's ugly and there's time left then fix it!
 * Keep an eye out for functional if you are going to talk about it
  * Iterate through an array and change each item


## Reading list

* http://searchengineland.com/how-google-instant-autocomplete-suggestions-work-62592



</content>
</snippet>