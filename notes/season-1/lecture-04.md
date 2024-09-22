# Episode 4 : Functions and Variable Environments

```js
var x = 1;
a();
b(); // Hoisting.
console.log(x); // 1

function a() {
  var x = 10; // localscope because of separate execution context
  console.log(x); // 10
}

function b() {
  var x = 100;
  console.log(x); // 100
}
```

Outputs:

> 10
> 
> 100
> 
> 1

## Code Flow in terms of Execution Context

* The Global Execution Context (GEC) is created (the big box with Memory and Code subparts). Also GEC is pushed into Call Stack

> Call Stack : GEC

* In first phase of GEC (memory phase), variable x:undefined and a and b have their entire function code as value initialized

* In second phase of GEC (execution phase), when the function is called, a new local Execution Context is created. After x = 1 assigned to GEC x, a() is called. So local EC for a is made inside code part of GEC.

> Call Stack: [GEC, a()]

* For local EC, a totally different x variable assigned undefined(x inside a()) in phase 1 , and in phase 2 it is assigned 10 and printed in console log. After printing, no more commands to run, so a() local EC is removed from both GEC and from Call stack

![How functions work in JS ❤️   Variable Environment _ Namaste JavaScript Ep  4 9-56 screenshot](https://github.com/user-attachments/assets/925fc8c3-80b9-4443-973f-44bd9cc063ce)

> Call Stack: GEC

* Cursor goes back to b() function call. Same steps repeat.

> Call Stack :[GEC, b()] -> GEC (after printing yet another totally different x value as 100 in console log)

![How functions work in JS ❤️   Variable Environment _ Namaste JavaScript Ep  4 12-50 screenshot](https://github.com/user-attachments/assets/3ddd1dbc-66c0-44eb-9856-1660f16f5495)

* Finally GEC is deleted and also removed from call stack. Program ends.

* reference:

![Execution Context Phase 1](/assets/function.jpg "Execution Context")
