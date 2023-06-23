# Session Two - Fireworks with functions

## Programming?

Programming! Now we're actually programming. But first, A bit of a history lesson.

Most websites from the 90s and early 00s didn't use javascript, or if they did, they made very minimal use of it. There were a variety of reasons for this, but the major reason was compatabiliy. In the early days, differences between browser vendors, and even versions, would cause major headaches for developers, and this is why Internet Explorer often recieved a lot of flack.

Since then, a lot of work has been done by the various browser vendors in cooperation with WaSP and W3C to provide complianct browsers. Not only that, but the onset of browsers that automatically update to the latest version, generally speaking, incompatability is now only a concern with brand new features.

The majority of browsers now use some form of Chromium for their implementation, with Blink acting as a Rendering engine and V8 for javascript. Views within the development community are still very mixed due to the chromification of all the browsers. Some view it as a good thing due to the shared implementation provided, others express their concerns with google's vested interests and biases. There are some hold outs though, most notably Firefox still uses their own implementation called Gecko, and Safari uses Webkit, which chromium originally forked for blink, so there's still hope for competition.

Obviously, we've been following the path of history to some extent, but I've no plans to worry about compatability, unless you specifically want to. In your adventures coding javascript you may see legacy code that had to deal with these issues though, so it's good to be aware of their existance.

## Overview

Javascript is a versatile programming language developers use to add interaction to a website. Javascript is also considered relatively beginner friendly so long as we ignore some of the more powerful features of javascript.

The community for javascript is booming, and as a result, many developers have written APIs (Application Programming Interfaces) which provide all sorts of additional features to program with. Some are small, solving a specific problem a dev had, others are massive and address a common theme. These come in a couple of forms, as Thrid party Libraries (like jQuery) that offer additional functionality to make development easier, and frameworks (like React) that provide tools which require your code to follow a specific structure or pattern. Browsers also provide APIs as standard.

Initially, we won't use any third party APIs, partly to avoid shortcuts, partly to provide an appreciation for where these libraries can help, and allow us to later build skills in choosing libraries.

Today is going to get a little bit heady with programming concepts. There's a whole bunch of concepts that all need to be understood, largely in unison, but i've tried to break them down as much as possible.

Unlike pervious sessions, the topics covered today are foundational to programming. It's okay if it doesn't make sense to start with, with time and practice it will click, but the ideas today will eventially become second nature, so if you're ever unsure, I invite you to ask me more.

## Hello World

Javascript is likely the technology any developer thinks of when they think of the web, because it's where you breath life into modern websites.

So lets get started. Firstly, create an element in our header, called `script`. The `script` tag can either be used to embed code within the body, or load a file, we're going to write code on the page just to get started quicker.

Within the script element, we're going to call a function called `alert`. Functions are blocks of code. Calling a function is relatively simple, we simply type the name of the function, and add a pair of parenthasis `()` after it, which contain any arguments we want to pass. We're going to display the classic programming idiom, so we need to pass the string `"hello world"` to the alert function.

```js
//this is a comment
alert("hello world");
```

A lot of things have happened at once, and we've used a couple of concepts already for this seemingly simple example.

What we've done here is created what's called a statement. A statement is a single piece of code. The semicolon marks the end of a statement. It's optional, so some people omit it, but automatic semicolon insertion can sometimes cause confusion, so I've included them in my examples.

We've also created our first instance of the primative type `string`. We can verify this with the `typeof` keyword, and we should be returned a string with the value `string`. We'll get to the implications of primative and reference types later when we work with referece types.

The double quotes `"` around our string are no accident, they're the way we declare string literals in javascript. We could have also used a single quote `'` however many languages use the single quote to denote a single character instead, so javascript devs tend to reserve the single quote for either that purpose, or to avoid escaping a double quote `\"` inside a string.

You'll also have noticed, like html, and css, the editor has highlighted our code with fancy colours.

## Variables

To make statements more exciting, we're going to need a whole bunch of language features. Probably the most important are places to put values. These are called variables. When we assign to a variable, the cpu stores that variable somewhere in memory.

There's two ways to declare variables in javascript, originally the `var` keyword was used, however javascript has recently introduced the `let` keyword, which changes the behaviour of the variable slightly. These changes make variable declaration more consistant with other languages, so for the sake of similicity we're going to stick with the `let` keyword for now.

So, `let` a variable, and call it `message`. Next we're going to alert the message variable and see what it's value is.

```js
let message;
alert(message);
```

The alert displays undefined, meaning we need to give it a value. So lets assign our string to it using the assignment operator `=` followed by the original string.

```js
let message = "hello world";
alert(message);
```

Our alert should now work like before again. This highlights how development can get complicated, we've changed one line of code, but we've had an effect on the code as a whole. In future, we'll talk about how to manage complexity.

Now, this is pretty boring, so lets ask for a name to say hello to. We can easily do this by calling the input counterpart to the alert function. This is called `prompt`, and will return user input we can assign to a variable. We can then alert this value.

## Operators

We've already used one operator, the assignment operator, there's a whole bunch of operators, to say hello to somebody, we're going to use another operator, called the concatinate operator `+`. It uses the plus sign and concatinate is just a fancy way of saying the operator is used to combine two strings together into one string. So if we call `prompt` and concatonate it to our previous string we should get a message back.

```js
let message = "hello " + prompt();
alert(message);
```

Great, there's a wide array of operators, but most programmers use them often enough that they will only look up the obscure ones. You'll be familiar with the most common arithmatic operators, since they match the mathematical symbols: addition `+`, subtraction `-`, multiplication `*` and division `/`. These operators follow similar rules of bodmas to their mathematical counterparts, and round brackets `()` can be used if order is unclear.

There's also bitwise operators, and logical operators which we will discover as we go.

## Control Flow

To keep things simple, we've only been scripting. By the traditional definition, this means we've been writing code as a simple sequence of operations. This changes now. We're going to graduate to treating javascript as a functional language. We will see elements of Object orientated programming today, but we'll opt to take them for granted for now.

You'll notice that if we don't enter a value into the prompt box, the program just runs normally. In programming we call this an edge case. This means it's something that doesn't happen often which we want to avoid.

This is where Control Flow comes in.
There's three main components to control flow:

1. Subroutines - We've already used these, when calling `alert` and `prompt`, but we've yet to write our own. Subroutines are core to every app. Subroutines are the more academic name for a function, and they represent a sequence of statements packaged together.

2. Branches - We're yet to use these. Branches are just a complicated way of saying that the code makes a decision called a conditional, and then executes different code based on the result of that condition. We usually use the `if` statement to acheive this, but other constructs like the `switch` statement also introduce branching into code.

3. Iteration - Iteration is a bit like a branch, but the code block multiple times instead of once. This is done with a few different kinds of language features, we're going to start with the `while` loop and touch the `for` loop, since these are the most traditional methods of looping, but there's other variaties of loops we will look at when we introduce reference types in a later lesson.

## Conditional statements

The way to branch in most programming languages is with the `if` statement. The `if` statement looks a little like a function, but it has a condition in `()` and body of code associated with it in `{}` called a code block.

So, lets use this knowledge to build an if statement that checks if the user typed input. We'll need to put the result of our alert into a seperate variable before building the string

```js
let name = prompt();
if (name) {
  let message = "Hello " + name;
  alert(message);
}
```

We could also complain when a name isn't supplied by pairing the `if` block with an `else` block or chain multiples together with `else if`.

```js
let name = prompt();
let message = "Hello ";

if (name) {
  message += name;
} else {
  message = "Surely you have a name";
}

alert(message);
```

In this case, we've used a `falsy` value to avoid doing anything when `name` is empty. You can also drop the curly brackets when you only want one line. Generally only do this when the entire expression fits on a single line:

```js
// Like this
if (name) alert("hello " + name);

// Instead of
if (name)
  alert("hello " + name);
```

There's a whole bunch of operators for working with conditional expressions. There's even one that behaves like an if statement. We'll discover more of them as we go along.

## Loops

Iteration is the way we repeat a similar, or identical task multiple times.
We're going to use the fibbonaci sequence to practice this.

First though, lets introduce our primary weapon, the `while` loop.
The while loop is similar to the `if` statement. The major difference being that the body of the statement runs from top to buttom, and when it reaches the bottom, it jumps back up to the top and retests the condition.

So, the fibonacci sequence is the previous two terms added together. The goal of our code will be to add together the previous two numbers starting with 0 and 1 to produce a new number. We're also going to switch to using `console.log` instead of `alert` to make running our code a little friendlier.

```js
let last = 0;
let current = 1;

while (current < 100) {
  let result = last + current;
  last = current;
  current = result;
  console.log(result);
}
```

Suppose we want the first ten terms, instead all the numbers below 100? how might we modify this code to acheive that? We could do:

```js
let last = 0;
let current = 1;
let i = 0;

while (i < 10) {
  let result = last + current;
  last = current;
  current = result;
  console.write(i + ": " + result);
  i++;
}
```

However, the `for` loop allows us to put all the important parts into the round brackets. The for expression looks like `for (let i = 0; i != 10; i++)` The first statement in a for loop allows us to decare variables, the second tests a condition after each iteration, and the third allows us to modify a value. It's common to see for loops in code because they show an original coder's intent.

```js
let last = 0,
  current = 1;

for (let i = 0; i < 10; i++) {
  let result = last + current;
  last = current;
  current = result;
  console.write(i + ": " + result);
}
```

This new example is functionally the same, ie it does the same thing, but it isn't the same in the strictest sense, due to a property of how variables declared with the `let` keyword differ from if those variables had been declared with `var`. That is their availability in Block scope. When a variable is declared with `let`, the variable is only available from within the block `{}` it was declared within. This means in the example above `i` is undefined outside the for loop, wereas if we used `var`, it would be accessable throughout the function it is declared.

Javascript developers use the `let` keyword because this behaviour matches other programming languages, and `var` provides a lot of unique ways to shoot yourself in the foot. Those mistakes used to be avoided by declaring all variables at the start of a function.