## **Closure**

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

## **Scope**

JavaScript has traditionally had two types of scope: `global scope` and `function scope`.

```
var globalVariable = 'This is global';

function globalFunction1() {
  var innerVariable1 = 'Non-global variable 1';
}

function globalFunction2() {
  var innerVariable2 = 'Non-global variable 2';
}
```

Scopes in JavaScript are **nested** so the two new function scopes become **child scopes** of the **global scope**. This means that the code inside each function can access the global `globalVariable` variable, as if it had been declared inside the function alongside the inner variables.

When trying to access an identifier the browser will first look for the variable inside the **current scope**. If it is not found, the browser will then look in the **parent scope** of the current scope, and will keep moving up through the parent scopes until it either finds the variable, or reaches the global scope. 

If the **variable still isn’t found in the global scope**, the browser will generate a `ReferenceError`. 

What the direction of the look-up through the scope chain means is that `innerVariable1` can only be accessed inside the `globalFunction1` function, and `innerVariable2` can only be accessed inside the `globalFunction2` function. 

### **Block scope**

In JavaScript, a `block` is one or more statements within curly brackets. 

Conditional expressions, such as `if`, `for`, and `while` statements, all use blocks to execute statements based on certain conditions.

**Block scope** means that a `block is able to create its own scope`, rather than simply existing within the scope created by its nearest parent function, or the global scope. 

```
function fn() {
  var x = 'function scope';

  if (true) {
    var y = 'not block scope';
  }

  function innerFn() {
    console.log(x, y); // function scope not block scope
  }

  innerFn();
}
```
The `var` statement `is not able to create a block scope`, even when used within a block, so the `console.log` statement is able to access both the `x` and `y` variables. 

### Hoisting

JavaScript has two phases: a **parsing phase** — where all of the code is read by the JavaScript engine — followed by an **execution phase** in which the code that has been parsed is executed. 

During the **parsing phase** takes place the `memory allocation` for variables and scope creation. 

When the JavaScript engine encounters a `variable` or `function declaration` it acts as if it literally lifts (hoists) that declaration up to the top of the current scope. 

```
function fn() {
  var x;
  var y;

  x = 'function scope';

  if (true) {
    y = 'not block scope';
  }

  function innerFn() {
    console.log(x, y); // function scope not block scope
  }

  innerFn();
}
```

**`Only the variable declaration is hoisted to the top of its scope`**; the `variable assignment` still occurs at the place where we assigned the value, inside the `if` statement in this example. 

In addition to variables, `function declarations` are also **hoisted**. 

```
function fn() {
  var x;
  var y;
  function innerFn() {
    console.log(x, y); // function scope not block scope
  }

  x = 'function scope';

  if (true) {
    y = 'not block scope';
  }

  innerFn();
}
```

## **`let`**

In order to create **block scope**, we need to use either the `let` or `const` statements inside a block. 

```
function fn() {
  var variable1 = 'function scope';

  if (true) {
    let variable2 = 'block scope';
  }

  console.log(variable1, variable2); // Uncaught ReferenceError: variable2 is not defined
}

fn();
```

Because we used the `let` statement **within that block**, a new **block scope** is created within the `fn scope`.

If the `console.log` statement had been inside the **if block** as well, it would be in the same scope as `variable2` and would be able to use the **scope chain** to find `variable1`. 

### **The Temporal Dead Zone**

Regular variables created using `var` are **hoisted** to the **top of the scope** and initialized with the value `undefined`:

```
console.log(x); // undefined
var x = 10;
```

Because of **hoisting**, the code is actually understood as this:

```
var x = undefined;
console.log(x); // undefined
x = 10;
```

Variables declared with `let` are **hoisted**, but crucially, they **are not automatically initialised with the value `undefined`**: 

```
console.log(x); // Uncaught ReferenceError: x is not defined
let x = 10;
```

This `error` is caused by the **temporal dead zone (TDZ)**. 

The **TDZ** exists from the moment the **scope is initialized** to the moment the **variable is declared**. 

To fix the `ReferenceError`, we need to **declare the variable before trying to access it**:

```
let x;
console.log(x); // undefined
x = 10;
```

## **`const`**

`const` statement is used to declare a variable whose **value cannot be reassigned**. 

It behaves in a very similar way as `let` does with regard to the **TDZ**, but when being declared, a `const variable` must be initialised with a value:

```
const VAR1 = 'constant';
```

From this point on, the value of `VAR1` will always be the string `constant`. 

If we try to change the value of the variable through reassignment, we’ll see an error:

```
TypeError: Assignment to constant variable
```

If we try to create a `const variable` without initializing it with a value, we’ll also see an error; this time a `SyntaxError`:

```
SyntaxError: Missing initializer in const declaration
```

`const` variable cannot be redeclared. If we try to declare the same `const variable` more than once, we’ll see a different type of `SyntaxError`:

```
SyntaxError: Identifier ‘VAR1’ has already been declared
```

### Immutability

If we initialize a `const variable` with an **object** or an **array**, we will still be able to set the properties of the object and add and remove items to the array.
