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
https://www.reddit.com/r/webdev/comments/3f7q3q/been_interviewing_with_a_lot_of_tech_startups_as/
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


## React, redux etc

## Rest/Ajax



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

## Harvard Lecture
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









</content>
</snippet>