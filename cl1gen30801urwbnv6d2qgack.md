## variable shadowing in javascript 👥

# Introduction 🐥

Hello everyone, this article is going to be very short but also important. Before reading this blog, please read my previous blog on [Scope, Scope-Chain, and Lexical Environment in JavaScript](https://sobitprasad.hashnode.dev/scope-scope-chain-and-lexical-environment-in-javascript). So, in this blog we will talk on ***shadowing in javascript***, what is ***illegal shadowing***. So, please read this blog carefully, because it will help you in your web dev journey. So, let's start.

# Variable Shadowing in JavaScript 👀

In my previous blog, we have talked a lot about scopes in javascript like global, local, and block scope. Now, let's understand shadowing with the help of an example. We will use the `var` and `let` keywords,
as `let` and `const` behave the same in variable shadowing so we will skip `const` here.

## variable shadowing with `var` keyword 🦉
```javascript
var a = 10; // variable declared in global scope
{
    var a = 100; // variable declared inside a block
}
console.log(a);
``` 
So, what will be the output here 🤔? Before answering, let's understand the above code. We have declared two variables with the same name `a` one in the global space and one inside the block, and we are consoling `a` in the global scope. So, now you can tell me your answer. If your answer is `100`, congratulations 🥳, it's the right answer. But why we are getting `100` even though we have written `console.log(a);` in the global scope. This is because, both the variables are pointing to the same memory location i.e. both are pointing to the Global Memory Scope. 

So, what is variable shadowing here? Here, the variable inside the block is shadowing the variable in the global scope. In simpler terms you can say, a variable in block scope is hiding the value of the variable in global scope with its shadow and printing its own value. But what if we write the variable declared inside the block, in a function. Let's see

```javascript
var a = 10; // variable declared in global scope
func();
function func(){
    var a = 100; // variable declared inside a function
}
console.log(a);
``` 
So, here output will be `10`, Why? Because both the variables are stored in different memory spaces. As keyword `var` is a function/local scoped i.e. variable declared inside the function can be accessed inside that function only, we will not be able to access it outside its boundary. And here, the variable `a` inside function fails to shadow the variable `a` in the global scope.

## variable shadowing with `let` keyword 🦚

Let's understand this with the above example only. 


```javascript
let  a = 10; // variable declared in global scope
{
   let a = 100; // variable declared inside a block
}
console.log(a);
``` 
So, here our output will be `10`, we should print `100` are you saying? No, it's not like that in the case of `let`, because `let` is a block-scope type i.e. if we declare a variable with `let` inside any block whether inside a function, inside an if-else, or inside a while/for loop, we will never be able to access `let` outside that block. As `let` is a block-scope type, in the above example both the variables have different memory spaces and the variable inside the block is not able to shadow the variable in the global space.

# Illegal Shadowing in JavaScript 🧛‍♀️

To understand illegal shadowing we will use `var` and `let` keywords in our example. So, let's try to understand illegal shadowing.

```javascript
    let a = 10; // variable declared in global scope using `let` keyword
    {
      var a = 100; // variable declared inside a block using `var` keyword
    }
   console.log(a);
```
Now, here we will get an error `Uncaught SyntaxError: Identifier 'a' has already been declared`. Although here both the variables are pointing to the global memory space, the variable `a` inside the block fails to shadow the variable `a` from the global space.  This is said to be illegal shadowing.

But what if we swap the keywords `let` and `var` or write the var `a` in a function instead in a block. So, let's see.

## Example 1: Swapping variables `let` and `var` in the above example

```
var a = 10; // variable declared in global scope using `var` keyword
    {
      let a = 100; // variable declared inside a block using `let` keyword
    }
  console.log(a);

```
Here, we will get `10` in the console and not an error, but why? Because, both the variables are pointing to separate memory spaces. Although, the variable inside the block will not shadow the variable in the global space, because `let` has its own separate memory space.

## Example 2: Writing variable `var` inside a function in the above example

```javascript
    let a = 10; // variable declared in global scope using `let` keyword
    func();
    function func(){
      var a = 100; // variable declared inside a block using `var` keyword
    }
   console.log(a);
```
Here, we will also get `10` in the console because variable `a` inside the function and variable `a` outside the function is pointing to the different memory location,s and here also var `a` inside the function will not shadow the variable declared with `let` keyword.

So, that's it guys for this blog. I will be very glad if you let me know any suggestions/corrections in any of my blog articles. If you find this article helpful, say hi to me on [LinkedIn](https://www.linkedin.com/in/sobit-prasad/) 🌸





