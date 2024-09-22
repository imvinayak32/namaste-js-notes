# Episode 10 : Closures  in JS

## Closure

* Function bundled along with it's lexical scope is **closure**.

* JavaScript has a lexcial scope environment. If a function needs to access a variable, it first goes to its local memory. When it does not find it there, it goes to the memory of its lexical parent. See Below code, Over here function **y** along with its lexical scope i.e. (function x) would be called a closure.
* Example
  
    ```js
    function x() {
        var a = 7;
        function y() {
            console.log(a);
        }
        return y;
    }
    var z = x();
    console.log(z);  // value of z is entire code of function y.
    ```
    * In above code, When y is returned, not only is the function returned but the entire closure (fun y + its lexical scope) is returned and put inside z. So when z is used somewhere else in program, it still remembers var a inside x()
    * z stores closure of y
    ```js
    // same as above one, just syntax changed
    function x() {
        var a = 7;
        return function y() {
            console.log(a);
        }
    }
    var z = x();
    console.log(z);
    ```
* Example

  ![Closures in JS 🔥 _ Namaste JavaScript Episode 10 15-30 screenshot](https://github.com/user-attachments/assets/a6e6ff42-51c7-40e3-a97f-1e596c8ab3ac)

  * When y is return it contain the reference to variable 'a', that's why output is 100.

* Example
    ```js
    function z() {
        var b = 900;
        function x() {
            var a=7;
            function y(){
                console.log(a,b);
            }
            y();
        }
        x();
    }
    z();    // 7 900
   ```

* **A closure is a function** that has access to its outer function scope even after the function has returned.
  
   ![Closure Explaination](/assets/closure.jpg "Lexical Scope")
  
* A closure can remember and access variables and arguments reference of its outer function even after the function has returned.


## Advantages of Closure:

![Closures in JS 🔥 _ Namaste JavaScript Episode 10 19-17 screenshot](https://github.com/user-attachments/assets/96e5b139-b996-4364-86b4-c8abb1790dc5)

1.  **Module Design Pattern**:
    -   The module design pattern allows us to encapsulate related
        functionality into a single module or file. It helps organize
        code, prevent global namespace pollution, and promotes
        reusability.
    -   Example: Suppose we're building a web application, and we want
        to create a module for handling user authentication. We can
        create a `auth.js` module that exports functions like `login`,
        `logout`, and `getUserInfo`.
    

      ``` js
          // auth.js
          const authModule = (function () {
            let loggedInUser = null;

            function login(username, password) {
              // Authenticate user logic...
              loggedInUser = username;
            }
            function logout() {
              loggedInUser = null;
            }
            function getUserInfo() {
              return loggedInUser;
            }
            return {
              login,
              logout,
              getUserInfo,
            };
          })();

          // Usage
          authModule.login('john_doe', 'secret');
          console.log(authModule.getUserInfo()); // 'john_doe'
      ```
      
2. **Currying**:
    -   Currying is a technique where a function that takes multiple
        arguments is transformed into a series of functions that take
        one argument each. It enables partial function application and
        enhances code flexibility.
    -   Example: Let's create a curried function to calculate the total
        price of items with tax.

      ``` js
          const calculateTotalPrice = (taxRate) => (price) => price + price * (taxRate / 100);

          const calculateSalesTax = calculateTotalPrice(8); // 8% sales tax
          const totalPrice = calculateSalesTax(100); // Price with tax
          console.log(totalPrice); // 108
      ```
      
3.   **Memoization**:
    -   Memoization optimizes expensive function calls by caching their results. It's useful for recursive or repetitive computations.
    -   Example: Implement a memoized Fibonacci function.

   ``` js
          function fibonacci(n, memo = {}) {
            if (n in memo) return memo[n];
            if (n <= 1) return n;

            memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
            return memo[n];
          }

          console.log(fibonacci(10)); // 55
   ```
4.   **Data Hiding and Encapsulation**:
    -   Encapsulation hides the internal details of an object and
        exposes only necessary methods and properties. It improves code
        maintainability and security.
    -   Example: Create a `Person` class with private properties.

   ```js
          class Person {
            #name; // Private field

            constructor(name) {
              this.#name = name;
            }

            getName() {
              return this.#name;
            }
          }

          const person = new Person('Alice');
          console.log(person.getName()); // 'Alice'
          // console.log(person.#name); // Error: Private field '#name' must be declared in an enclosing class
   ```

5.   **setTimeouts**:
    -   `setTimeout` allows scheduling a function to run after a
        specified delay. It's commonly used for asynchronous tasks,
        animations, and event handling.
    -   Example: Delayed message display.

   ```js
          function showMessage(message, delay) {
            setTimeout(() => {
              console.log(message);
            }, delay);
          }

          showMessage('Hello, world!', 2000); // Display after 2 seconds
   ```

  These examples demonstrate the power and versatility of closures in
JavaScript! 🚀

* Disadvantages of Closure:
  * Over consumption of memory
  * Memory Leak
  * Freeze browser
