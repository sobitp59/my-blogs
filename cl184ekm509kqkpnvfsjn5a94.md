## Scope, Scope-Chain, and Lexical Environment in JavaScript

# Introduction

What comes to your mind when you heard the term ***"scope"***? It probably might be a ***"binocular"*** or if you play any battle-royale game (like PUBG, Fortnite, etc), then it might be a 2X, 3X, 4X scopes, etc, Right? Whatever it might be, let's see scope from the perspective of a battle royale game. So, from the perspective of a battle-royale game, the scope is used to see/find enemies that fall in the range of the scope, isn't it? And in JavaScript, the scope works something like this. 

Namaste everyone, in this blog article we are going to explore a bunch of things like scope, scope-chain, lexical environment, etc. But, before reading this article I will recommend you to read my blog on [JavaScript Behind The Scene](https://sobitprasad.hashnode.dev/javascript-behind-the-scene) so that you got familiar with how JavaScript works behind the scene. So, let's explore.

# Scope in JavaScript 

Scope in JavaScript is the range where we can access specific variables and functions or you can say, scopes tell us where we can access particular variables and functions in our code. So, there are basically three types of scopes in JavaScript : 
1. Global Scope 
2. Local/Function Scope
3. Block Scope

Let's explore all these scopes one by one and see how it works.

### Global Scope in JavaScript

When we declare variables or functions at the top of our code i.e. in the global space then those variables or functions are said to be in the Global Scope. We can access these variables or functions from anywhere inside our code. Let's understand this with the help of an example -


```javascript
// variables and functions declared in the global space
var globalScopeVariable = `variable "globalScopeVariable" declared in Global space`;
            console.log(globalScopeVariable);

function globalScopeFunction(){
            console.log(`function "globalScopeFunction()"" declared in Global space and accessing 
            "globalScopeVariable" below : `);
           // accessing variable "globalScopeVariable" 
            console.log(`Accessed "globalScopeVariable" : ${globalScopeVariable}`);
        }
 globalScopeFunction();

function callingGlobalScopeFunction(){
            console.log(`an another function "callingGlobalScopeFunction()" declared in Global space and 
            accessing "globalScopeFunction" below : `);
            // accessing function "globalScopeFunction()"
            console.log(`Accessed "globalScopeFunction()" : `);
            globalScopeFunction();
        }
 callingGlobalScopeFunction();

``` 

The above code might overwhelm you, but don't worry we will understand each and every line of code.
In the above example, we have declared a variable `globalScopeVariable` and two functions `globalScopeFunction()` and `callingGlobalScopeFunction()` all in the global space. And function `globalScopeFunction()` is accessing the variable `globalScopeVariable` and function `callingGlobalScopeFunction()` is accessing the function `globalScopeFunction()`, we can also access function `callingGlobalScopeFunction()` inside an another function. 

But how are we able to access the variable `globalScopeVariable` inside function `globalScopeFunction()` and function `globalScopeFunction()` inside function `callingGlobalScopeFunction()` which are not physically present inside that code. The answer is very simple, it's because we have declared all the variables and functions in the global space and thus we are able to access these variables and functions.

But what if we reverse the situation, i.e. what if we declare a variable or function inside a function and try to access that, outside the code or in the global space. What do you think? And here ladies and gentlemen come the term **Local/Function** scope, so let's explore this one as well.

### Local/Function Scope in JavaScript

First, let's understand this term, and later we will understand more deeply with the help of examples.

If we declare a variable or a function inside a function then, the scope of that variable and function is said to be Local/Function scope i.e., we can't access those variables and functions outside that function.
Let's understand this with the help of an example - 


```javascript

1   function funcOne()
2    { // start of scope of variable "varOne"
3      var varOne = `I am inside function "funcOne()"`;
4      console.log(varOne);
5
6      funcTwo();
7      function funcTwo()
8       { // start of scope of variable "varTwo"
9            var varTwo = `I am inside function "funcTwo()."`;
10           console.log(varOne);
11           console.log(varTwo);
12           
13          funcThree();
14          function  funcThree()
15           { // start of scope of variable "varThree"
16                var varThree = `I am inside function "funcThree()".`;
17                 console.log(varOne);
18                 console.log(varTwo);
19                 console.log(varThree); 
20           } // end of scope of variable "varThree"
21
22        }  // end of scope of variable "varTwo"
23 
24    } // end of scope of variable "varOne"
25        
26     funcOne();
``` 

In the above example, we have three functions `funcOne()`, `funcTwo()` and ` funcThree()`, and also we have three variables namely `varOne`, `varTwo` and `varThree`.

`funcOne()` is declared inside `funcTwo()`, `funcTwo()` is declared inside `funcThree`, and `funcThree()` is declared in the global space. And variables `varOne`, `varTwo`, and `varThree` are declared inside functions `funcOne`, `funcTwo`, and `funcThree` respectively. 

The scope of these variables starts with the opening curly brace `{` and ends with the closing curly brace `}` of their respective functions, i.e. we cannot access these variables outside that function. And same in the case of functions, in the above example, if we will try to invoke/call function `funcOne()` outside the function `funcOne()` we will get `ReferenceError`.

But, have you noticed that inside function `funcTwo()` we are trying to access variable `varOne` and inside function `funcThree` we are trying to access variables `varOne` and `varTwo` which are physically not present there. But how are we able to do it? Why we are not getting any errors? All these are possible because of the `Lexical Scope/Environment`. 

And here we will need the concept of Global Execution Context and Callstack, that's why I recommended reading [that blog](https://sobitprasad.hashnode.dev/javascript-behind-the-scene) at the beginning of this article. So guys, let's explore this one as well.

### Lexical Scope/Environment in JavaScript

We know that when we run our code, a Global Execution Context is created, and with every invocation of a function another Execution Context gets created and all these are pushed to the Callstack in order of their invocation.

But what is Lexical Scope/Environment? Don't worry we will understand this more deeply. First, let's understand how lexical scope/environment is created. So, when Global Execution Context is created, a lexical scope/environment is also created i.e. with every Execution Context there is something called `lexical scope/environment` is present with it. Let's understand this with the help of the figure below by taking the example of the code above.


![lexical-environment.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647886721490/z6pMbfGI5.png)

So, when we will run the above code a Global Execution Context is created, and `funcOne` will be assigned with whole code inside the `{ .. }` curly braces and `varOne` will be assigned with `undefined` in the memory component and when the code runs in the code component `varOne` will be assigned with its actual value i.e. `I am inside function "funcOne()` and another Execution Context is created for `funcTwo` and `funcThree` as well.

Now remember this paragraph we have discussed above
>But, have you noticed that inside function `funcTwo()` we are trying to access variable `varOne` and inside function `funcThree` we are trying to access variables `varOne` and `varTwo` which are physically not present there. But how are we able to do it? Why we are not getting any errors? All these are possible because of the `Lexical Scope/Environment`. 

So, here is the answer. **The lexical environment is the local memory along with the lexical environment of its parent.** Didn't understand? Let's go deep and understand this with the help of the code above.

In function `funcThree`, we have only declared variable `varThree`. So, when `funcThree` executes, JavaScript Engine will assign `undefined` to all the variables i.e. to `varOne`, `varTwo`, and `varThree` in the memory component. But, `varOne`, and `varTwo` are not initialized inside `funcThree`. So, the lexical environment of `funcThree` will start looking for the values of its parent i.e. inside function `funcTwo` and here we will find the value of `varTwo`. But again, the value of `varOne` is not inside function `funcTwo()`, so the lexical environment of `funcTwo` will start searching for the value of `varOne` of its parent i.e. inside `funcOne()` and when the value is found it is assigned to its respective variables. The chain of these lexical environments is known as ***Scope Chain***.

> NOTE: the lexical environment of global or window object is null. If we will try to access a variable or function which is not declared anywhere, then of course it will not be present in any of the lexical environments and we will get a beautiful error.
 
It's enough for the lexical environments, now let's head to our final destination of this article i.e. the block scope in JavaScript. 

### Block Scope in JavaScript

Before learning block scope in JavaScript, first, let's understand what a ***BLOCK*** is? So, a block in JavaScript is defined by the curly braces `{ }`, also known as the compound statement. Now, you might be wondering what is the use of *** block***, Right? So, a block is used to combine multiple JavaScript statements into a group. Now, you might have another question why do we need to group multiple JavaScript statements into a group? So, here is the answer, we need to group multiple JavaScript statements in a block so that we can use that block where JavaScript expects only one statement. If it sounds confusing don't worry, let's understand this by creating a block of statements step by step.

Step 1:We can start our block with this `{ }` curly braces. This curly braces `{ }` below is a block and a valid JavaScript code. 

```javascript
{
// I am a block
}
``` 

Step 2: Now, we can write multiple JavaScript statements inside this block `{ }`.

```javascript
{
console.log('I am inside a block');
console.log('I am also inside a block');
}
```
Step 3: Let's used the above block with the `if` where JavaScript expects only one statement, i.e. we can write an `if` statement as `if (true) console.log('I am not inside a block');` when we need a single statement, but when we need multiple statements we can use block as shown below in the code.

```javascript
if(true){
console.log('I am inside a block');
console.log('I am also inside a block');
}

//Output : 
//I am inside a block
//I am also inside a block
```

Now, as we have understood ***block***, let's dive into ***block scope*** in JavaScript. To understand block scope, let's declare three variables using `var`, `let`, and `const`.

```javascript
{
var a = 'I am var a';
let b = 'I am let b';
const c = 'I am const c';

// inside block
console.log(a);
console.log(b);
console.log(c);
}

// outside block
console.log(a);
console.log(b);
console.log(c);

//Output : 
//I am var a
//I am let b
//I am const c
//I am var a
//Uncaught ReferenceError: b is not defined
```

Now, when we run the above code we will get the error `Uncaught ReferenceError: b is not defined` i.e. while accessing the variable `b` outside the block. This is because the scope of variables `b` and `c` is inside that block only i.e. these variables are stored in the separate memory space, we cannot access variables declared with `let` and `const` outside that block. And thus, `let` and `const` is said to be ***block-scoped***.

But, if we have written the same code inside a function, we will not be able to access a single variable outside the block i.e.

```javascript
func();
function func(){
var a = 'I am var a';
let b = 'I am let b';
const c = 'I am const c';

// inside block
console.log(a);
console.log(b);
console.log(c);
}

// outside block
console.log(a);
console.log(b);
console.log(c);

//Output : 
//I am var a
//I am let b
//I am const c
//Uncaught ReferenceError: a is not defined
```

And thus, var is said to be `function/local scoped` i.e. if we declare a variable using the `var` keyword inside a function, we will not be able to access that variable outside that function. 

So, that's it guys for in this blog. I will be very glad if you let me know any suggestions/corrections in any of my blog articles. If you find this article helpful, say hi to me on [LinkedIn](https://www.linkedin.com/in/sobit-prasad/) 🌸


 










 