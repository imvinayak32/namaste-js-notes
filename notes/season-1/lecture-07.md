# Episode 7 : The Scope Chain, Scope & Lexical Environment
## Scope
* <mark>What is the scope of this variable b?</mark> that means where I can access this variable b.
* <mark>Is b inside the scope of function c()</mark> that means is that variable 'b' accessible inside c() or not.

> **Scope** in Javascript is directly related to **Lexical Environment**.

* Let's observe the below examples:
```js
// CASE 1
function a() {
    console.log(b); // 10
// Instead of undefined it prints 10, So somehow this a function could access the variable b outside the function scope. 
}
var b = 10;
a();
```

```js
// CASE 2
function a() {
    c();
    function c() {
        console.log(b); // 10
    }
}
var b = 10;
a();
```

```js
// CASE 3
function a() {
    c();
    function c() {
        var b = 100;
        console.log(b); // 100
    }
}
var b = 10;
a();
```

```js
// CASE 4
function a() {
    var b = 10;
    c();
    function c() {
        console.log(b); // 10
    }
}
a();
console.log(b); // Error, Not Defined
```

* Let's try to understand the output in each of the cases above.
  * In **case 1**: function a is able to access variable b from Global scope.
  * In **case 2**: 10 is printed. It means that within nested function too, the global scope variable can be accessed.
  * In **case 3**: 100 is printed meaning local variable of the same name took precedence over a global variable.
  * In **case 4**: A function can access a global variable, but the global execution context can't access any local variable.

## Lexical Environment
* **Lexical**: In hierarchy, In order
  > function c() is lexically sitting inside the function a()
  > 
  > function a() is lexically inside the Global scope
  
  ```js
  function a() {
      function c() {
          // logic here
      }
      c(); // c is lexically inside a
  } // a is lexically inside global execution
  ```
  
* **Lexical Environment** = local memory space + reference to lexical environment of its parent.

* Whenever an Execution Context is created, a Lexical environment(LE) is also created and is referenced in the local Execution Context(in memory space).

  ![image](https://github.com/user-attachments/assets/b48604d8-b77f-41b1-948a-057fc55dd559)

* **Let's see how it is used?**
  
  ![Lexical Scope Explaination](/assets/lexical.jpg "Lexical Scope")

* When we encountered **console.log(b)** inside function c(), it first searches b in it's local memory space, since it is not available there. So, it moves to Lexical environment of it's parent and similarly moves to next if not available there as well untill null.

* Reaching to null means we are exhausted and will give output as **not defined**

## Scope Chain / Lexical Environment Chain
* The process of going one by one to parent and checking for values is called scope chain or Lexcial environment chain.
  
  ![image](https://github.com/user-attachments/assets/18fb2971-30cd-4f0a-a823-526f83ad9eb6)

* How things happen in call stack -
    ```
    To summarize the above points in terms of execution context:
    call_stack = [GEC, a(), c()]
    Now lets also assign the memory sections of each execution context in call_stack.
    c() = [[lexical environment pointer pointing to a()]]
    a() = [b:10, c:{}, [lexical environment pointer pointing to GEC]]
    GEC =  [a:{},[lexical_environment pointer pointing to null]]
    ```
## How things look like in browser?

![Lexical Scope Explaination](/assets/lexical2.jpg "Lexical Scope")
![image](https://github.com/user-attachments/assets/de0df3b9-1a2d-4964-802b-679e9d5317a8)


* Lexical or Static scope refers to the accessibility of variables, functions and object based on physical location in source code.
    ```js
    Global {
        Outer {
            Inner
        }
    }
    // Inner is surrounded by lexical scope of Outer
    ```


* **TLDR**; An inner function can access variables which are in outer functions even if inner function is nested deep. In any other case, a function can't access variables not in its scope.
