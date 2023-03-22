---
title: "How Asynchronous JavaScript Works: A Deep Dive into Its Execution Process"
datePublished: Wed Mar 22 2023 07:28:50 GMT+0000 (Coordinated Universal Time)
cuid: clfjd5ilm000109le5fwj386b
slug: how-asynchronous-javascript-works-a-deep-dive-into-its-execution-process
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678883766730/9b2aa249-25c9-4694-ac7d-0dae74917ca3.png
tags: javascript, event-loop, callstack, javascript-engine, javascript-runtime-environment

---

# Overview

If you are an aspiring JavaScript developer, you will likely be asked whether JavaScript is synchronous or asynchronous.

And when you look around for the answers, you might get mixed answers for it. Some considered that JavaScript is synchronous while others say that it is asynchronous.

Then, what is the correct answer? Is it synchronous or asynchronous? Well, at its base JavaScript is synchronous but somehow it can be manipulated to work asynchronously.

But, how does it all happens? So, In this blog, we will dive deep and will try to understand how JavaScript is executed under the hood asynchronously.

# Understanding Synchronous and Asynchronous

In JavaScript, both synchronous and asynchronous are different ways of executing the code.

## Synchronous

Synchronous codes are executed in order, one statement at a time. Each statement must finish its execution before the next one is executed.

Think of it as a running race track, but only with one single track for all the athletes. Once the athlete at the very first reaches the finish line, then only the next athlete can start the race and so on.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678358435868/3add72c4-1c79-4842-aecc-abbb46f3f839.png align="center")

## Asynchronous

Asynchronous codes are executed out of order, multiple statements at a time. All the statements can be executed parallelly.

Think of it as a regular running race track, each track for each athlete. Here, the athletes don't have to wait for the other athletes to start the race.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678359015874/e61101a0-8506-43f5-8a03-f804ffea0ed9.png align="center")

# Understanding JavaScript Engine

JavaScript engines are programs that help in executing the JavaScript code. They are typically responsible for compiling the JavaScript code from human-readable to machine-readable instructions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678423651817/78c033f8-cf8c-4029-8767-af1ae40353b3.png align="center")

There are several JavaScript Engines. Some of the most popular ones are :

* **V8**: It was developed by Google for use in the Chrome browser and is also used in Node.js.
    
* **SpiderMonkey**: It was developed by Mozilla for use in Firefox.
    
* **Chakra**: It was developed by Microsoft for use in the Edge browser.
    

## How JavaScript Engine Compiles the Code?

JavaScript Engines have to go through multiple phases to compile the code from human-readable format to machine-readable format. So that, the computer can understand and executes the code.

When we give our code to JavaScript Engines, it has to go through - *parsing*, *compilation* and *execution*.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678434888387/da876979-74be-4a8e-a9fe-c7b331c22d3f.png align="center")

> Every JavaScript Engine might have different algorithms to execute the code. However, the fundamentals of how JavaScript code is parsed, compiled, and executed are generally the same across different JavaScript engines.

### **Parsing Phase**

During parsing, JavaScript Engines break down the code into its tokens such as keywords, identifiers, or operators. These tokens are used to form the Abstract Syntax Tree(AST) which is the high-level representation of the source code.

Let's take an example and see how it looks when it gets converted to Abstract Syntax Tree.

```javascript
const hw = 'hello world';
console.log(hw);
```

The above code will be broken into individual tokens during a process called tokenization.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678451410625/fcc5e515-cf83-4b47-bb56-a975851c4fad.png align="center")

These tokens and the source code are then used to generate the Abstract Syntax Tree(AST).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678462514410/f14057f1-031d-40b6-8c10-a7dc2a3df004.png align="center")

See Abstract Syntax Tree in JSON format below.

[open GitHub Gist](https://gist.github.com/sobitp59/2edf4ade0a749dd5be9c2a5e4c118e16)

### **Compilation Phase**

During compilation, JavaScript Engine takes the Abstract Syntax Tree(AST) and turns it into low-level bytecode that the computer understands. Let's see how it does.

In the beginning, JavaScript Engines uses interpreters to compile the code. The interpreter makes debugging easier because it stops and updates whenever it finds an error. But the interpreter works slower as it has to translate the code line-by-line.

> An interpreter reads and executes the code line by line. As each line gets interpreted, it is executed by the computer, and the interpreter proceeds to the next line and so on.

To overcome the interpreter's inefficiency, JavaScript Engines started using compilers along with interpreters. Compilers are fast but debugging the code was slower.

> A compiler translates the entire source code into machine language before it is executed.

And this is what we called a Just-in-Time(JIT) compilation. JIT uses the best of both interpreter and compiler. JIT compilers make debugging easier because of the interpreter and faster because of compilers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678513512905/816dc117-8a21-491d-9e06-66c515897b99.png align="center")

### **Execution Phase**

In most JavaScript engines, the compilation and execution of code happen concurrently and hand-in-hand, rather than in a strict sequential order.

As the code gets compiled, the JavaScript engine **starts the execution** before it has finished compiling the entire program and this is possible because of the JIT compiler.

In the execution phase, we have three important components - the **call stack**, the **memory heap** and the **garbage collector**. Let's understand each of them in the next section.

## Understanding CallStack and Memory Management

When the code reaches the execution phase, it is the job of the call stack, memory heap and garbage collector to ensure that the programs run smoothly and efficiently.

So, what are their jobs, let's understand each of them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678557083645/0ffbfe07-bf79-42af-a98b-ce1ff2f29ad9.png align="center")

### **Understanding Call Stack**

When we say JavaScript is a **single-threaded language**, it means that it has only **one call stack**. The call stack can do only one thing at a time.

The job of the call stack is to track the execution context of a running program and it does by keeping track of all the functions that currently running.

It is based on Last-In-First-Out(LIFO) data structure, which means that the most recently called function is the first to be executed and the last to be completed.

So, whenever there’s a function call it gets pushed to the top of the stack. After it finishes executing it is removed from the top of the stack.

### **Understanding Memory Management**

JavaScript Engines manage the memory for us, removing the burden of explicitly allocating and deallocating memory unlike we do in other programming languages like C or C++. Let's understand in brief how JavaScript Engines manage memory.

The three phases of the memory life cycle are allocation, utilization, and deallocation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678630902792/1844ea98-5715-4d9d-b0ca-4b61835eeb9d.png align="center")

* **allocation**: reserving memory for a particular object or data structure.
    
* **utilization**: use of that memory by the program, which may involve reading from or writing to the memory.
    
* **deallocation**: releasing the memory when it is no longer needed, to make it available for other uses.
    

JavaScript Engines can allocate memory in two places, either on the stack or a memory heap.

### Stack

All the primitive values like *strings*, *numbers*, *booleans*, *undefined*, and *null* are stored on the stack.

When we pass a variable having primitive values as a reference to a new variable, a copy of the value is passed to the new variable. So, changing the value of the new variable will not affect the one that is passed as a reference.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678713079160/d46a126a-8865-4af5-98f4-ec6fc30581b5.png align="center")

In the above example,

* We have assigned `buy vegetables` (a primitive value) to variable `todoOne`.
    
* Then we created another variable `todoTwo` and assigned it with the variable `todoOne`.
    
* Here, the copy of the value of the variable `todoOne` i.e. `buy vegetables` is assigned to the variable `todoTwo`.
    
* Then, we redeclared the variable `todoTwo` with `exercise : 500 skipping`. Here, re-declaring the variable `todoTwo` will not affect the variable `todoOne`.
    
* So, when we consoled the variable `todoOne`, its value remained the same.
    

### Memory Heap

All non-primitive values like arrays, objects or functions are first stored on the heap and then passed as a reference to the stack.

When we pass a variable having non-primitive values as a reference to a new variable, the reference of the memory location is passed to the new variable. So, changing the value of the new variable will also affect the one that is passed as a reference.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678713120023/633e99e0-7ba8-4612-98d8-25af097c39c0.png align="center")

In the above example,

* We have assigned an object (a non-primitive value) to variable `userOne`.
    
* Then, we created another variable `userTwo` and assigned it to variable `userOne`
    
* Here, the reference of the variable `userOne` will be assigned and not a copy of it.
    
* So, when we changed the property `name` of the variable `userTwo` , the property(`name`) of variable `userOne` also got changed.
    

Now, we also need to de-allocate the memory that is not in use, and this is done by **Garbage Collector**. It works by periodically finding and removing the objects that are no longer referenced by the program.

Till now, we have only understood how JavaScript Engine works under the hood from parsing, compiling, and executing to memory management. But where does it all happen? And that's what we will be learning in the next section.

# Understanding JavaScript Runtime Environment

As human beings, we need some environment to work effectively. For example, to study, we need a quiet environment, books, etc. To cook food we need a kitchen provided it has all the necessary items to cook food like gas stoves, groceries, water, etc.

It also applies to JavaScript Engine as well. JavaScript Engine cannot work independently, it needs some environment. And that environment is called **JavaScript Runtime Environment(JRE)** for JavaScript Engines.

JavaScript Runtime Environment(JRE) provides all the necessary components to JavaScript Engine so that it can work effectively. **And you know what, it's the** **JRE only that manipulates JavaScript to work asynchronously**.

First, let's discuss the important components of the JavaScript Runtime Environment and then we will discuss how these components work together with JavaScript Engine.

## Core Components of JavaScript Runtime Environment

The core components of the JavaScript Runtime Environment(JRE) are JavaScript Engine itself, which we have discussed earlier and the **Web APIs**, **microtask queue**, **callback queue**, and the **event loop**. Let's discuss each of them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678883821415/955e2254-fd23-403d-bafd-c35ce86bdd6d.png align="center")

### Web APIs

Web APIs are a set of built-in interfaces and functionalities provided by the Javascript Runtime Environment(JRE) to interact with external systems like servers, databases and other web services.

These Web APIs help in **handling asynchronous operations** like making a network request, processing large amounts of data, animating elements on a web page, etc.

There are several built-in interfaces and functionalities, let's discuss some of them.

* [DOM API](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model): Document Object Model(DOM) API helps in accessing and manipulating the elements and attributes of an HTML or XML document in real-time.
    
* [Console API](https://developer.mozilla.org/en-US/docs/Web/API/Console_API): Console API helps in performing debugging tasks, such as logging messages or the values of variables at set points in your code, etc.
    
* [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API): Fetch API helps in making HTTP requests to retrieve resources from servers without blocking the main thread.
    
* [setTimeOut](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout): This method allows us to schedule the execution of a function after a certain amount of time has passed.
    

### Callback Queue and Microtask Queue

A callback queue is a data structure that stores a queue of callback functions waiting to be executed. It is based on First-In-First-Out(FIFO) data structure which means the first in the queue will be the first to execute.

A microtask queue also stores a queue of callback functions waiting to be executed but the one with the **higher priority**. The callback functions with higher priority are the ones that came through **Promises**, **mutation observer**, **queueMicrotask**, etc.

### Event Loop

Event Loop helps in executing the callback functions that are waiting on the callback queue. It does this by constantly checking the call stack and the event queues(callback queue and microtask queue).

The event loop checks if the call stack is empty or not and if it is then it checks if any callback functions are waiting to be executed in the callback queue or microtask queue.

And if there are any callback functions to be executed, it takes the first callback function from the queue and pushes it to the call stack.

The event loop then waits for the call stack to be emptied again so that it can push the next callback function in the queue. It does until all the callback functions are executed.

## How JavaScript Runtime Environment Works?

So far, we have discussed and understood the JavaScript Engine and the core components of the JavaScript Runtime Environment(JRE). But how do all these work together? Let's find out with the help of an example.

> **Remember:**
> 
> 1. When the JavaScript Engine goes through the code, it first creates a **Global Execution Context(GEC)** and put it on the Call Stack. The global execution context includes information about the global scope, such as global variables and functions.
>     
> 2. And whenever a function is invoked it creates a new **Execution Context(FEC)** for that function and put it on the Call Stack. The function execution context includes information about the local scope of the function, such as its arguments and local variables.
>     
> 3. All synchronous operations must complete their execution before the asynchronous operation gets executed.
>     

In the example below, we have defined four functions `greetUser()`, `delayedBy20ms()`, `getMovie()` and `letMeRun()`.

* `greetUser()` function has a variable `message` assigned with `hello user! welcome to moviehub` and simply consoling the value.
    
* `delayedBy20ms()` function returning `setTimeOut` method to delay the execution by 20 milliseconds.
    
    > Syntax of setTimeout:
    > 
    > setTimeout(callbackFunction, delayInMilliseconds);
    > 
    > * **callbackFunction**\- a function containing a block of code
    >     
    > * **delayInMilliseconds**\- the time after which the function is executed
    >     
    
* `getMovie()` function is returning a promise that fetches some movies from the server.
    
* `greetUser()` function has a variable `run`assigned with value `let me run please!!` and it also simply consoling the value.
    

```javascript
function greetUser(){
     const message = 'hello user! welcome to moviehub';                              
     console.log(message); 
};

function delayedBy20ms(){    
    return setTimeout(() => {    
        console.log('I will be print at least after 20 milliseconds!!')
    }, 20);
};

function getMovie(movieName){
    return new Promise((resolve, reject) => {
        if(movieName === 'inception'){
            resolve({data : 'here is your movie from the server!'})
        }else{
            reject({message : 'movie not found!!'})
        }
    });
};

function letMeRun(){
    const run = 'let me run please!!';
    console.log(run);
};


greetUser();

delayedBy20ms();

getMovie('inception')
.then((response) => console.log(response.data))
.catch((error) => console.log(error.message));

letMeRun();
```

### **Phase 1: When programs execute for the first time**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679294240364/38d0c7e2-996b-43c4-95f7-5a2347a5cc82.png align="center")

Do you remember what will happen when JavaScript Engine goes through the code? Let's find out.

1. So first, a Global Execution Context(GCE) is created and pushed in the Call Stack.
    
2. The Global Execution Context will hold information about all the functions' definitions and variables.
    
3. Also for each function, a function object is created and stored in the memory heap. This function object will contain the function's code and any variables declared within that function.
    

### **Phase 2 : When greetUser() function is invoked**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679407016401/be21372d-8efa-4fd4-92e4-d7f006533870.png align="center")

After defining all the functions in the global execution context, now all these functions will execute when they are invoked. So, first, we are invoking `greetUser.` Let's understand what will happen when it gets invoked.

1. First, an execution context of `greetUser` function will be created and pushed to the call stack. The execution context includes the variable `message` and value `hello user! welcome to moviehub`.
    
2. `greetUser` function is consoling the variable `message`. It will be pushed into the call stack and tries to find the value of the variable in the execution context.
    
3. When it gets the value of `message`, it simply prints in the console.
    
4. Since `greetUser` function finishes its execution, its execution context will be destroyed.
    
5. Then, `greetUser` function is popped off from the call stack.
    

Now the program moves to the next line of code.

### Phase 3: When delayedBy20ms() is invoked

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679407393918/1ea87984-0c00-4132-989b-23b682085694.png align="center")

1. When `delayedBy20ms` function is invoked, a new execution context is created and it will be pushed to the call stack. It is returning a `setTimeout` method.
    
2. When `setTimeout`method is invoked a new execution context for `setTimeout` is created and will also be pushed in the call stack. Inside the `setTimeout` execution context, we have a **callback function** and a **timer** of **20 milliseconds**, which says that the `setTimeout` method will be executed at least after 20 milliseconds.
    
3. Since `setTimeout` is an asynchronous operation provided by Web APIs, it will not execute immediately. So, the callback function and timer (20 ms) will be moved to Web APIs.
    
4. Meanwhile, the execution context of `setTimeout` will be destroyed.
    
5. Then `setTimeout` method will be popped off from the call stack.
    
6. Then the execution context of `delayedBy20ms` function will be destroyed.
    
7. And finally, `delayedBy20ms` pops off from the call stack.
    
8. Now, when the timer of 20ms expires the callback function moved to the callback queue
    
9. The event loop is continuously checking if there is any function in the callback queue ready to be executed. But the call stack is not emptied yet, so the callback function will wait in the callback queue till the call stack is empty.
    

### Phase 4: When getMovie() function is invoked

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679405324807/7bd90050-4f17-4cc0-9308-b8c28f20899d.png align="center")

1. Now `getMovie()` the function is invoked, a new execution context for it will be created and it will be pushed into the call stack. It holds the argument `movieName` and value `inception` and also it is returning a promise.
    
2. Since `getMovie` function is returning a `promise`, so when the promise executes a new execution context will be created and it will be pushed into the call stack. The execution context includes `value` which is initially `undefined`, `status` which is `pending` and function definitions when the promise is resolved and rejected.
    
3. As **Promise** is an asynchronous operation, it will be moved to Web API.
    
4. The execution context of **Promise** will be destroyed
    
5. And it will be popped off from the call stack.
    
6. Now the execution context of `getMovie` function will also be destroyed.
    
7. And then popped off from the call stack.
    
8. The **Promise** waits in the Web API till it gets a response from the server.
    
9. When it gets the response from the server `value` will be the data returned from the server, `status` changes to `resolved` from `pending`.
    
10. Based on whether the promise is resolved or rejected, a callback function is pushed into the microtask queue. In this case, the callback function is `(response) => console.log(response.data).`
    
    > Q. Why Promise is pushed into the microtask queue and setTimeout into the callback queue?
    > 
    > A. Because Promise has **higher priority** than setTimeout.
    
11. The event loop is still checking if there is any task to be executed from the microtask or callback queue and also if the call stack is empty or not. Since the call stack is not emptied yet it cannot execute the callback functions that are ready to be executed.
    

### Phase 5: When letMeRun() function is invoked

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679405344407/da23d24b-e301-477b-bfe8-f8964fbe940d.png align="center")

1. When `letMeRun()` is invoked a new execution context will be created and pushed into the call stack. The execution context includes the variable `run` and its value `let me run!!.`
    
2. `letmMeRun` function calling the `console.log(run).` So it will be pushed into the call stack and tries to find the value of the variable `run` in the execution context.
    
3. When it gets the value from the execution context, the value will be printed on the console.
    
4. Now, the execution context of `letMeRun` function will be destroyed.
    
5. Then `letMeRun` function will be popped off from the call stack
    
6. Since there is nothing to execute anymore the global execution context will also be popped off from the call stack.
    

### Phase 6: When the microtask queue executes

Now we have one callback function(Promise) in the microtask queue and one callback function(setTimeout) in the callback queue.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679405369262/1e289611-a42f-48c8-8ac8-c617118d5753.png align="center")

1. The event loop finds that the call stack is empty and also there is one callback function in the microtask queue and one callback function in the callback queue is ready to be executed.
    
2. Since the callback function(Promise) resides in the microtask queue have higher priority, therefore it will execute first.
    
3. When the callback function executes, a new execution context is created and pushed into the call stack. The execution context includes arguments `response` and value `{data : 'here is your movie from the server!'}`.
    
4. Now `console.log(response.data)` is invoked, it gets the value from the execution context.
    
5. The value `here is your movie from the server!` is printed on the console.
    
6. The execution context of the callback function is destroyed.
    
7. And finally popped off from the call stack.
    

### Phase 7: When the callback queue executes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679405396319/e7d1c9e6-bec0-4b74-950e-6331d3328dbf.png align="center")

1. Again event loop finds that the call stack is empty and there is a task in the callback queue ready to be executed.
    
2. The callback function gets executed.
    
3. So, a new execution context is created. Then it is pushed into the call stack. The execution context includes an argument `1` and value `i will be print at least after 20 milliseconds!!`.
    
4. Now, console.log() is called, it gets the value from the execution context.
    
5. Then the is printed on the console.
    
6. The execution context of the callback function is destroyed.
    
7. And finally, the callback function is popped off from the call stack.
    

### The output

After executing all the programs we get the output as :

```plaintext
hello user! welcome to moviehub
let me run please!!
here is your movie from the server!
i will be print at least after 20 milliseconds!!
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679405452834/f6ef676b-30d4-484f-abdb-0881ada3dbf5.png align="center")

Even though we have executed the code in the order below, we get the output in a different order, and this is how the JavaScript Runtime Environment gives an illusion of asynchronicity.

I hope now it makes sense to you whenever you get the output as the above one.

```javascript
// ORDER OF INVOCATION OF THE FUNCTIONS
greetUser(); //1

delayedBy20ms(); //2

getMovie('inception') //3
.then((response) => console.log(response.data))
.catch((error) => console.log(error.message));

letMeRun(); //4
```

# Conclusion

I know this was a long article but I hope you have read all the sections carefully. We learned a lot of things, aren't we? So let's quickly recap what we have learned so far.

* JavaScript at its base is synchronous, but with the help of **JavaScript Runtime Environment(JRE),** it can work asynchronously.
    
* Every browser has a JavaScript Engine, and the runtime environment is the browser itself.
    
* JavaScript Engine helps in parsing, compiling and executing the code.
    
    * During parsing, code breaks down into small tokens and it gets converted to Abstract Syntax Tree(AST).
        
    * During compilation, the AST is converted into the bytecode.
        
    * During execution, JavaScript Engine executes the code as the code gets compiled.
        
* We don't need to worry about memory management in JavaScript.
    
    * JavaScript Engine takes care of all these, from allocation to utilization to de-allocation.
        
    * All the primitive values like *strings*, *numbers*, *booleans*, *undefined*, and *null* are stored on the stack.
        
    * All non-primitive values like arrays, objects or functions are first stored on the heap
        
* The core components of the JavaScript Runtime Environment are:
    
    * Web APIs: it helps in interacting with external systems like servers, databases, etc.
        
    * Microtask Queue: it stores a queue of callback functions waiting to be executed with a higher priority.
        
    * Callback Queue: it stores a queue of callback functions waiting to be executed after the microtask queue becomes empty.
        
    * Event Loop: it helps in executing the callback functions that are waiting on the callback queue by constantly checking if the call stack is empty or not.
        

While writing this article I came to know about so many amazing things and my love for JavaScript increases even more. I hope this article helped you too to understand how Asynchronous JavaScript works under the hood.

Additionally, I welcome your feedback. If you come across any areas that require correction or you just want to connect, feel free to contact me via email at sobitwrites@gmail.com.

---

**References and Useful Resources**:

* [JavaScript the Hard Parts by CodeSmith](https://www.youtube.com/watch?v=fOdcuDigxfw)
    
* [JavaScript Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)
    
* [JIT Compiler by Programming With Avelx](https://www.youtube.com/watch?v=svJerixawV0)
    
* [JavaScript's Memory Management Explained by Felix Gerschau](https://felixgerschau.com/javascript-memory-management/)
    
* [Abstract Syntax Tree(AST) viewer](https://astexplorer.net/)