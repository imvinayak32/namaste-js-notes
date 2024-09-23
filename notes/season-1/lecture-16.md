# Episode 16 : JS Engine Exposed, Google's V8 Architecture

* JS runs literally everywhere from smart watch to robots to browsers because of Javascript Runtime Environment (JRE).

* JRE is like a big container which has everything which are required to run Javascript code.

* JRE consists of a JS Engine (❤️ of JRE), set of APIs to connect with outside environment, event loop, Callback queue, Microtask queue etc.

![JS Engine EXPOSED 🔥 Google's V8 Architecture 🚀 _ Namaste JavaScript Ep  16 1-34 screenshot](https://github.com/user-attachments/assets/a7e7a195-cab2-4ee7-b55f-754795373ec1)

* Browser can execute javascript code because it has the Javascript Runtime Environment.

* Node.js also have JRE, containing all these components as well. but the name for API's may change or could be similar as console, setTimeout

* ECMAScript is a governing body of JS. It has set of rules which are followed by all JS engines like

> Chakra (Edge)
>
> Spidermonkey(Firefox) {first javascript engine created by JS creator himself}
>
> v8 (Chrome) (Node.js)

* Javascript Engine is not a machine. Its software written in low level languages (eg. C++) that takes in high-level code in JS and spits out low level machine code.

> v8 is written in C++

### Code inside Javascript Engine passes through 3 steps : 
> **Parsing**, **Compilation** and **Execution**

#### 1. **Parsing**
* Code is broken down into tokens. In "let a = 7" -> let, a, =, 7 are all tokens. Also we have a syntax parser that takes code and converts it into an AST (Abstract Syntax Tree) which is a JSON with all key values like type, start, end, body etc (looks like package.json but for a line of code in JS. (Check out astexplorer.net -> converts line of code into AST)

![JS Engine EXPOSED 🔥 Google's V8 Architecture 🚀 _ Namaste JavaScript Ep  16 11-51 screenshot](https://github.com/user-attachments/assets/02fd2ede-45c0-4ed3-b7e6-433436fbd111)

#### 2. **Compilation**
* JS has something called Just-in-time(JIT) Compilation - uses both interpreter & compiler. Also compilation and execution both go hand in hand. The AST from previous step goes to interpreter which converts high-level code to byte code and moves to execeution. While interpreting, compiler also works hand in hand to compile and form optimized code during runtime.JS used to be only interpreter in old times, but now has both to compile and interpreter code and this make JS a JIT compiled language, its like best of both world.

![JS Engine EXPOSED 🔥 Google's V8 Architecture 🚀 _ Namaste JavaScript Ep  16 16-35 screenshot](https://github.com/user-attachments/assets/0bf4a4a3-b1e1-4e70-8a3f-b12ade2e653a)

 **Does JavaScript really Compiles?** The answer is a loud **YES**. More info at: [Link 1](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md#whats-in-an-interpretation), [Link 2](https://web.stanford.edu/class/cs98si/slides/overview.html), [Link 3](https://blog.greenroots.info/javascript-interpreted-or-compiled-the-debate-is-over-ckb092cv302mtl6s17t14hq1j). 
    
#### 3. **Execution**
* Needs 2 components ie. Memory heap(place where all memory is stored) and Call Stack(same call stack from prev episodes). There is also a garbage collector. It uses an algo called **Mark and Sweep**.
    ![JS Engine Demo](/assets/jsengine.jpg)

#### GiF Demo
![JS Engine Demo](/assets/jsenginegif.gif)

* Companies use different JS engines and each try to make theirs the best.
    * v8 of Google has Interpreter called Ignition, a compiler called Turbo Fan and garbage collector called Orinoco
#### v8 architecture:
![JS Engine Demo](/assets/jsengine.png)
