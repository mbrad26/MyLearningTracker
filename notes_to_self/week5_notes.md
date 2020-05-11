## Closure

A **closure** is the combination of a `function` bundled together (enclosed) with references to its `surrounding state` (the lexical environment). 

Consider the following code example:

```
function makeFunc() {
  var name = 'Mozilla';
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```

A closure is the combination of a function and the lexical environment within which that function was declared. 

This environment consists of any local variables that were in-scope at the time the closure was created: 
* In this case, `myFunc` is a reference to the instance of the function `displayName` created when `makeFunc` is run. 
* The instance of `displayName` maintains a reference to its lexical environment, within which the variable `name` exists. 

For this reason, when `myFunc` is invoked, the variable `name` remains available for use, and "Mozilla" is passed to alert.

```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

In essence, `makeAdder` is a function factory. 

In the above example, the function factory creates two new functions — one that adds five to its argument, and one that adds 10.

`add5` and `add10` are both closures. They share the same function body definition, but store different lexical environments. In `add5`'s lexical environment, x is 5, while in the lexical environment for `add10`, x is 10.

```
function add (x) {
  return function (y) {
    return x + y;
  };
}

var add5 = add(5);
var no8 = add5(3);
alert(no8); // Returns 8
//Whoa, whoa! What just happened? Let’s break it down:
```

* When the add function is called, it returns a function.
* That function closes the context and remembers what the parameter x was at exactly that time (i.e. 5 in the code above)
*  When the result of calling the add function is assigned to the variable add5, it will always know what x was when it was initially created.
* The add5 variable above refers to a function which will always add the value 5 to what is being sent in.
* That means when add5 is called with a value of 3, it will add 5 together with 3, and return 8.

So, in the world of JavaScript, the add5 function actually looks like this in reality:

```
function add5 (y) {
  return 5 + y;
}
```
