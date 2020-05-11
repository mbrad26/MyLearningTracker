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