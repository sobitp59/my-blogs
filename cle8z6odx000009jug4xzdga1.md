# Why do browser consoles return undefined? Explained

# Overview

As web developers, we are blessed with consoles in the browsers to interact and debug our web pages and applications.

The most common type of console is the JavaScript console, which is found in most modern web browsers.

These consoles are built into the web browser that provides a command-line interface(CLI) for executing JavaScript commands and inspecting and debugging the state of our web pages.

In this blog, we will try to find the answer to "Why browser console returns undefined?".

# The Browser Console

The first time I interacted with the console(`press F12`) was during following a course on JavaScript on Udemy.

I performed a lot of operations and getting the results in real-time in the console felt so convenient.

But, one thing that constantly bothered me was in some operations it returns the result as expected like adding two numbers `10 + 39` gives `49`, while in other cases like after defining a function or variable it gives `undefined.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676440216021/9e26bf8c-4eaa-4ef0-8fbf-23aa921c969b.png align="center")

So, let's understand the reason behind getting `undefined`. But, before that, we have to know what `` `undefined` `` actually is.

# Understanding Undefined

In JavaScript, `undefined` is a primitive value that is assigned to variables that have been declared but have not been initialized with a value, or to function parameters that have not been provided with an argument.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676450491435/c3e746f2-b3ae-4421-bcb0-6faa8dfd831a.png align="center")

We can say that `undefined` is like a placeholder for the variables and functions' arguments in the memory space until it's not get assigned with any value or passed with any arguments in functions.

# Understanding the working of REPL and Console

The way code is executed in the console of a web browser is similar to the Read-Eval-Print Loop (REPL) methodology that is commonly used in interactive programming environments.

However, the console of a web browser is not strictly a REPL environment but it does share some similarities in terms of how code is entered, executed, and displayed.

This is different from how we code in a traditional programming environment, where we typically have to save our code to a file, compile it (if necessary), and then run it.

Now first, let's understand what each part of the abbreviation of REPL tells us:

* **Read**: Hey! I am *Read* and I help in reading the input(code) that you enter. If your input is not correct(syntactically), I will not be able to pass your input to Eval.
    
* **Eval**: Heya! I am *Eval*(not evil) and I help in evaluating the input that you gave me via *Read* so that I can determine the results for your input.
    
* **Print**: Helloo! I am *Print* and I help in displaying the result of the evaluation provided by the Eval on the console.
    
* **Loop**: Hello! I am *Loop* and I help in taking you back to the *Read* so that you continue your chit-chat(giving input) with Read.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676485591604/f459f847-a8b2-4fef-af28-036ff313d940.png align="center")

So basically, it is a type of interactive programming environment that reads the code, evaluates it, prints the result (if there is one), and then waits for us to enter more code.

# Understanding the Reason Behind Undefined

We know that because of the REPL methodology, the codes get executed immediately after we press `ENTER.`

We also know there are three steps( **Read, Evaluate and Print** ) in between before it gets ready to read our code again (basically before **Loop** ).

At the **Print** stage, it is decided what should be printed in the console by JavaScript Console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676569398260/cde1c612-5de4-4706-8619-419859345047.png align="center")

So, let's understand the different scenarios that probably might help us to understand when the JavaScript console decides to print `undefined`, and when not.

## the console.log()

In JavaScript, every function returns a value, even if there is no explicit specification of one using the `return` keyword. If no `return` statement is used, the function automatically returns `undefined` by default.

When we call `console.log()` with a value as an argument, the value is printed to the console and then `undefined` is printed because `console.log()` itself does not have a return value.

```javascript
console.log('hello world!')
// hello world!
// undefined
```

It is designed to output messages to the console, but it doesn't return a value that could be used elsewhere in the code.

So, after the value is printed to the console, the function returns `undefined` as its default return value.

## the explicit return type

Since we know that every function in JavaScript returns something. If there will be nothing, then it will be `undefined` by default.

So, let's tell the browser console explicitly what we want to return and see how it responds to us.

```javascript
function animeLists(){
    return ['naruto','attack on titans', 'one piece']
}
// undefined
// animeLists()
// ▸(3) ['naruto', 'attack on titans', 'one piece']
```

When we run the above code in the console, at first we will get `undefined`. This is because just defining a function does not produce a return value, so the console does not have anything to display as a result of the function definition.

The function definition is just stored in memory somewhere and is not executed until we call it.

In the next line, when we called the function `animeLists` and since we are explicitly telling the console to return the `['naruto', 'attack on titans', 'one piece']` using `return` keyword, we will only get the output and not `undefined`.

## the expressions

An expression in JavaScript is a combination of values, variables, and operators that can be evaluated to a single value.

It can be as simple as a single value or it can be as complex as a combination of multiple expressions.

```javascript
//01: Arithmetic Expression
2 + 3 * 4 // returns 14

//02: Function call Expression
Math.max(1, 2, 3) // returns 3

//03: Ternary operator Expression
x > y ? "x is greater" : "y is greater" // returns the greater one

//04: Boolean Expression
true === 1 // returns false
```

In all the examples above, the console does not display the value `undefined` because after reading the expression, it gets evaluated and the result is immediately printed on the console.

After printing the result, it loops back to Read so that it starts taking more inputs from us.

## the final example

Till now if you have got a little idea about how all these work from the examples above, then let's finally conclude this, understanding the example below step by step.

Before that, let's give aliases to "Read", "Eval", "Print "and "Loop" as "Mr. Read", "Mr. Eval", "Mr. Print" and "Mr. Loop" respectively.

```javascript
// Run this code in console
function greetUser(){
    const message = 'hey user! welcome to console';
    console.log(message);
    console.log('your total cost for the stay is : ');
    return 2100 - 100;
}
```

* **Step 1**: When we enter this input in the console and press `ENTER`, Mr. Read will look into our code and finds everything fine. So, he tells Mr. Eval to look into it.
    
* **Step 2**: Now, when Mr. Eval looks into the code, he finds that it is just a function definition because the function hasn't been called yet. Since there is nothing to return, Mr Eval returns `undefined` and sends it to Mr. Print.
    
* **Step 3**: The job of Mr. Print is to display whatever is received by Mr. Eval on the console. This time it was `undefined`, so he prints the same on the console.
    
* **Step 4**: Since the final result is printed for the execution of code till now, Mr. Loop will tell Mr. Read, "hey Mr. Read! you can now take another input from the user". And this process continues.
    

Till now, we have only gotten the `undefined` because we haven't called the function yet, so let's finally call the function `greetUser()` .

```javascript
greetUser(); // calling the function
```

The same process will be followed this time as well, let's understand this one as well.

* **Step 1**: After we call the function `greetUser,` Mr. Read will look into our code and reads the various commands we have given.
    
* **Step 2**: Now, Mr. Loop will evaluate our code and since we are explicitly returning with the `return` keyword, we will not get `undefined`. After evaluation, Mr. Loop sends the result to Mr. Print.
    
* **Step 3**: Now, Mr. Print displays the final result on the console.
    
    ```plaintext
    hey user! welcome to console
    your total cost for the stay is : 
    2000
    ```
    
* **Step 4**: Again, Mr. Loop will tell Mr. Read, "hey Mr. Read! you can now take another input from the user". And this process continues.
    

# Summary

* A console is a built-in tool in modern web browsers that provides a command-line interface for debugging and interacting with web pages.
    
* It is similar to the Read-Eval-Print Loop (REPL) methodology used in interactive programming environments where,
    
    * Read: It reads the input we enter
        
    * Eval: It evaluates and determines the results of the input.
        
    * Print: It prints the result on the console.
        
    * Loop: It loops back to Read so that Read can take another input.
        
* In JavaScript, every function returns a value, by default it is `undefined`. And since console.log() does not have a return value so it prints `undefined.`
    
* If we explicitly state the return value in the code then it resolves the issue of getting "undefined" as output.
    

I hope this blog helps you to understand at least the basic concept behind returning `undefined` to the console. If it does, do share it and if you want to connect with me, say Hi! [here](https://twitter.com/sobit_prasad).