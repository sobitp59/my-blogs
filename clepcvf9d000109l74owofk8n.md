# Understanding Var, Let and Const in JavaScript with Examples

## Overview

Unlike other programming languages, like Java and C++ where we need to specify the type of variables while declaring, it is somewhat different in JavaScript.

JavaScript limits us to declare variables only using these three keywords - the *var*, the *let* and the *const*. Also, we do not need to specify the type of variables while declaring it.

And even though, having only three ways of defining variables most beginners find it difficult to digest them.

In this blog, we'll explore var, let, and const through various examples and will try to understand the differences between them.

## A Brief History of Variables in JavaScript

Until EcmaScript2015(ES6), we were only declaring variables using the *var* keyword.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677384254482/c40ed66f-e769-49fc-8844-72cf556e2885.png align="center")

With the introduction of ES6 in June 2015, the *let* and *const* came into existence and were considered the best practice to declare variables in modern JavaScript.

## What is a Variable?

A variable is a named storage location that holds some value pointing to some memory location in the computer's memory, that we can use later to manipulate our programs.

Think of it like you are giving a name to some location in the computer's memory. This memory location can be used to store the value you wanted.

Later, if you need the value you have stored, you can simply use the name you have given to that memory location.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677304507248/9c15ddf5-08ff-4a0e-85a2-e59f2dd5b882.png align="center")

From the above figure, you can see we have three variables `var1`, `var2` and `var3` stored in memory locations 1, 3 and 5 with assigned values of `hello world`, `{....}` and `121432` respectively.

Now, whenever we need these values we can simply use the names we have assigned to those memory locations.

## Understanding Var and Let

We know that both var and let are used to declare variables, but there are some important differences that we need to consider.

We will measure the differences in terms of their *declaration*, *scoping* and *hoisting.* So, let's discuss each of them in detail with examples.

### var is re-declarable while let is not

When we declare a variable using *var*, we can re-declare that variable in the same scope multiple times.

> re-declaration refers to declaring a variable with the same name multiple times within the same scope.

```javascript
var greetUser = 'good morning!';
var greetUser = 'good afternoon!';
console.log(greetUser); // good afternoon!
```

In the above example, you can see we have two variables `greetUser` with the same name. The second `greetUser` overwrites the value of the first, so we get the output as `good afternoon!` .

This is not in the case of variables declared with *let*. This means, re-declaration is not allowed for variables declared using *let*. We will get a syntax error if we do so.

```javascript
let greetUser = 'good morning!';
let greetUser = 'good afternoon!';
console.log(greetUser); 
// SyntaxError: Identifier 'greetUser' has already been declared
```

However, we can re-initialize a variable declared using both with var and let multiple times in the same scope.

> re-initialization refers to assigning a new value to a variable that has already been declared and initialized within the same scope.

```javascript
var greetUser = 'good morning!';
greetUser = 'good afternoon!';
console.log(greetUser); // good afternoon!
```

```javascript
let greetUser = 'good morning!';
greetUser = 'good afternoon!';
console.log(greetUser); // good afternoon!
```

Also, even if we remove the keywords var and let from the above examples, we will get the same output.

```javascript
greetUser = 'good afternoon!';
console.log(greetUser); // good afternoon!
```

This is because when we use a variable without explicitly declaring with keywords var or let, it is automatically created as a global variable. However, it is not possible in [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode), we will get a reference error.

```javascript
"use strict";
greetUser = 'good afternoon!';
console.log(greetUser);
// ReferenceError: greetUser is not defined
```

### var is function-scoped while let is block-scoped

In JavaScript, scoping is used to determine the availability or visibility of a variable in a particular part of a program, based on where it is declared.

There are primarily four types of scopes in JavaScript - global, functional, block and module scope. We will discuss only the first three.

* **global scope** - a variable declared outside any function or block(inside curly braces **{}**) can be said to be in the global scope. It is visible or accessible throughout the whole program.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677434211932/2181fde1-2f4f-4460-9bf7-f267f5bc3330.png align="center")
    
    ```javascript
    var varA = 'I am in global scope';
    let letA = 'hey, I am too in global scope';
    
    function printData(){
        console.log(varA);
        console.log(letA);
    };
    printData();
    // I am in global scope
    // hey, I am too in global scope
    ```
    
    In the above code, variables `varA` and `letA` both are in the global scope and can be accessed inside any function and block.
    
* **function scope** - variables declared using the *var* keyword are functionally scoped. This means, if we declare a variable inside a function it will be accessible inside that function only.
    
    The accessibility of variables declared using *var* inside a function is limited to that function only.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677434248785/90875844-016e-48a1-8b27-b8ee9bf34a14.png align="center")
    
    ```javascript
    function printData(){
        var favoriteBook = 'the happiness hypothesis';
        console.log(favoriteBook); 
    };
    printData(); // the happiness hypothesis
    console.log(favoriteBook); // ReferenceError: favouriteBook is not defined
    ```
    
    We will get a reference error from the second console because we are trying to access the variable `favouriteBook`, which is defined inside the function `printData`.
    
* **block scope** - variables declared using the *let* keyword have block scope. This means that if we declare a variable inside any block(block refers to curly braces **{}**), we will not be able to access that variable outside that block.
    
    The accessibility of variables declared using *let* inside a block is limited to that block only.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677434297860/549326cd-3077-4e07-9473-397f9edaef24.png align="center")
    
    ```javascript
     function printSomething() {
        let x = 10;
        if (true) {
          let y = 20;
          console.log(x); // 10
          console.log(y); // 20
        }
        console.log(x); // 10
        console.log(y); // ReferenceError: y is not defined
    };
    printSomething();
    ```
    
    In the above example, we have declared two variables, `x` inside function `printSomething` and `y` inside the `if` block which again is inside the `printSomething` function only.
    
    The scope of the variable `x` is the whole `printSomething` function, while the scope of the variable `y` is limited only to the `if` block.
    
    So, when we tried to access the variable `y` (`console.log(y);`) at the very end of the function `printSomething` we get a reference error.
    

### var and let both are hoisted?

Hoisting is a mechanism that is used to move the variable and function declarations to the top of their respective scope before the code is executed.

However, the code doesn't actually re-arrange, but the JavaScript Engine finds the variables and functions and reserves memory for them before the code gets executed.

By default, variables get initialized with a value of *undefined* and in the case of functions, an actual copy of the functions is allocated.

And that's the reason when we run the code below, we get undefined and the function gets executed without any error.

```javascript
console.log(varA);
print();

var varA = 'hello shipper!'
function print(){
    console.log('hello builder!')
};
// undefined
// hello builder!
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677582919691/6d9b8263-610e-4220-9d86-0f5eb0040361.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677582969506/5a9dfb0a-c7d0-40d8-bb78-8073117655f1.png align="center")

Till now, we have been only discussing the functions and variables declared using *var*. But, what if we declared it using *let*? Will we get *undefined* or it will be an error? Are the variables declared using *let* hoisted?

And many questions might come to your mind. So, let's try to find the answers to all the questions above.

First, let's try to find whether variables declared using *let* are hoisted or not. Well, some say that *let* is hoisted while others deny it. This argument is fine since hoisting is not a globally agreed term.

However, variables declared using *let* show behavioural characteristics of hoisting. It's too get allocated with a default value of *undefined* in the memory.

```javascript
console.log(letA);
let letA = 'hello shipper!';
//ReferenceError : Cannot access 'letA' before initialization
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677593660689/0f6a5699-7c81-400f-8fd1-3ca488594279.png align="center")

If it is already allocated with a default value of undefined, then why did we get the error? And this is where **Temporal Dead Zone** comes in.

A variable declared using *let* is said to be in a "temporal dead zone" (TDZ) from the start of the block until code execution reaches the line where the variable is declared and initialized.

```javascript
console.log(letA); // I am in Temporal Dead Zone

let letA = 'hello shipper!'

if(true){
    console.log('hello batman!');
    console.log('hello spiderman!');
    console.log('hello superman!');

    console.log(shaktiman); // I am too in Temporal Dead Zone
    let shaktiman = 'hello shaktiman';
}
```

In the above example, both `console.log(letA);` and `console.log(shaktiman);` are in the temporal dead zone.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677645840046/94ef6bf3-1769-41de-b25e-d439629a4ad1.png align="center")

The TDZ for variable `letA` starts from the very top and ends on the line where it is declared and initialized. While the TDZ for the variable `shaktiman` starts from the top of the `if` block and ends where it is declared and initialized.

If we will try to access those variables in their temporal dead zone(TDZ) then it will result in a reference error.

## Understanding Const

The reason I didn't talk about variables declared using *const* earlier was that it works almost like variables declared using *let*, with some slight key differences. So, let's discuss each of them.

### Initialization

We can declare a variable with *let* without an initial value and can assign it later. But it is not possible with variables declared using *const*. It must be initialized with a value when they are declared.

```javascript
// Allowed ✅
let letA;
letA = 'hello shipper!';

// Not Allowed ❌
const constA;
constA = 'hello builder';
// SyntaxError: Missing initializer in const declaration
```

### Mutability

We can mutate a variable declared using *let* while variables declared using *const* are immutable, meaning that their values cannot be changed after they are initialized.

```javascript
// Allowed ✅
let letA = 'hello shipper!';
letA = 'hello earth!';

// Not Allowed ❌
const constA = 'hello builder';
constA = 'hello mars!';
// TypeError: Assignment to constant variable.
```

### Scope

Variables declared using *const* have the same block scope as variables declared using *let*. However, variables declared using *const* have a more restrictive scope than variables declared using *let*.

We cannot redeclare a variable declared using const within the same block, while variables declared using let can be redeclared within the same block.

```javascript
if(true){
    let iWantToBe = 'an astronaut';
    iWantToBe = 'a web developer'; // Allowed ✅

    const youWantToBe = 'a doctor';
    youWantToBe = 'a soldier'; // Not Allowed ❌
}
```

## Reason for introducing let and const

We have been declaring variables using *var* for almost 20 years, then why there was a need of introducing let and const? Some of them we have already discussed above by comparing with var. Let's discuss a few more and then we can conclude this post.

### Naming collision

As we know that variables declared using var are re-declarable in the same scope, which leads to naming collision. This can be prevented if we will use let or const as re-declaration is not allowed with let and const is even stricter than let.

```javascript
// Allowed ✅
var favoriteAnimeName = 'naruto';
var favoriteAnimeName = 'deathnote'; 

// Not Allowed ❌
let favoriteAnimeName = 'naruto';
let favoriteAnimeName = 'deathnote'; 

// Not Allowed ❌
const favoriteAnimeName = 'naruto';
const favoriteAnimeName = 'deathnote';
```

### Memory save

If we declare variables using let and const they can help to save memory by limiting the scope of variables to only the blocks where they are needed, and by allowing for the re-use of variable names within different blocks of code.

This can help to ensure that memory is used efficiently and not wasted on variables that are no longer needed.

```javascript
function calculate(numbers1, numbers2) {
    let total = 0; // declare and initialize ⚡ 'total' variable
  
    for (let number of numbers1) {
      total += number;
    }
    console.log(total);
    
    {
      let total = 0; // declare and initialize new ✨ 'total' variable
      for (let number of numbers2) {
        total += number;
      }
      console.log(total);
    }
}

calculate([1,2,3,4],[10,11,12, 13]);
// 10
// 46 
```

# Summary

In this blog, we tried to understand the three ways of declaring variables using *var*, *let* and *const*.

Variables declared using *var* are more flexible but it leads to more confusion and bugs due to its function-level scoping and hoisting behaviour.

On one hand, let allows the re-assignment, making it useful for situations where variable values may change over time.

On the other hand, const doesn't allow re-assignment, making it useful for situations where variable values should not be changed.

While I cannot say that you should completely stop using *var* and only use *let* and *const* from now on. Choosing between var, let and const will depend on the specific needs of our program.

If we understand the differences and trade-offs between these three variable declaration methods, we can write more efficient and bug-free code.

# Conclusion

I hope this article helps you to understand the differences and use cases of variables declared using var, let and const.

Share this with your friends and provide feedback to me at sobitp59@gmail.com. If you come across any incorrect information, please don't hesitate to reach out. I'm open to hearing your thoughts!

And also, I am doing the #151DaysOfCode challenge on Twitter, connect with me if you wanna join too and let's get started!

%[https://twitter.com/sobit_prasad/status/1624307436428627968?s=20]