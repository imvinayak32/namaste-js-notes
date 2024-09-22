# Episode 9 : Block Scope & Shadowing in JS

## Block?
* Block aka *compound statement* is used to group multiple JS statements together into 1 group. We group them within {...}

Why **Block**?
* We combine multiple Js statements in block, so that it can be used where Js excepts a single statement.
* if (condition) single_statement;
* To use multiple statements here, we can use like this - 

  ![image](https://github.com/user-attachments/assets/72d4727f-fe88-42b8-aed3-c2297d20dde6)


## Block Scope?
* what all variables and function we can access inside a block, is know as block scope
```js
{
    var a = 10;
    let b = 20;
    const c = 30;
    // Here let and const are hoisted in Block scope,
    // While, var is hoisted in Global scope.
}
```
![image](https://github.com/user-attachments/assets/a59dec32-02c2-4332-9392-e956c0a5ca76)

```js
    {
        var a = 10;
        let b = 20;
        const c = 30;
    }
    console.log(a); // 10
    console.log(b); // Uncaught ReferenceError: b is not defined
```
* Reason?
  * In the BLOCK SCOPE; we get b and c inside it initialized as *undefined* as a part of hoisting (in a seperate memory space called **block**)
  * While, a is stored inside a GLOBAL scope. 

  * Thus we say, *let* and *const* are BLOCK SCOPED. They are stored in a separate mem space which is reserved for this block. Also, they can't be accessed outside this block. But var a can be accessed anywhere as it is in global scope. Thus, we can't access them outside the Block.

## Shadowing?

```js
    var a = 100;
    {
        var a = 10; // same name as global var
        let b = 20;
        const c = 30;
        console.log(a); // 10
        console.log(b); // 20
        console.log(c); // 30 
    }
    console.log(a); // 10, Why??
```
* Reason - 
    * Initially 'a' is in global space (a = 100)
    * When a = 10 line is run, a is not created in block space, but replaces 100 with 10 in global space itself.
    * As var is associated with Global Execution Context itself.
  
* So, If one has same named variable outside the block, the variable inside the block *shadows* the outside variable. **This happens only for var**

* Let's observe the behaviour in case of let and const and understand it's reason.
    ```js
    let b = 100;
    {
        var a = 10;
        let b = 20;
        const c = 30;
        console.log(b); // 20
    }
    console.log(b); // 100, Both b's are in separate spaces (one in Block(20) and one in Script(another arbitrary mem space)(100)). Same is also true for *const* declarations.
    ```
    ![Block Scope Explaination](/assets/scope.jpg "Lexical Scope")


* Same logic is true even for **functions**
    ```js
    const c = 100;
    function x() {
        const c = 10;
        console.log(c); // 10
    }
    x();
    console.log(c); // 100
    ```

What is **Illegal Shadowing**?

* ```js
    let a = 20;
    {
        var a = 20;
    }
    // Uncaught SyntaxError: Identifier 'a' has already been declared
    ```
    * We cannot shadow let with var. But it is **valid** to shadow a let using a let. However, we can shadow var with let.
    * All scope rules that work in function are same in arrow functions too.
    * Since var is function scoped, it is not a problem with the code below.
        ```js
        let a = 20;
        function x() {
            var a = 20;
        }
        ```
