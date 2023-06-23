# Session 4 - Functions and Combining Web Tech

First, we're going to introduce functions, and use a couple of exercises to refresh everything we learned in the previous session. After, we'll take a look at how everything we've learned so far can be combined.

## The Function

We've talked about functions for a little bit, we've called a few, and we've also called a method (a function that exists within the context of an object), but now we're going to write our own function.

What is a function? A function is a block of code, that we can pass in values, the function then performs some sort of operation, and can optionally return a result or throw an error. We're going to use the fibbonaci sequence again to practice them i.e. `0 1 1 2 3 5 8`

There are two syntaxes for declaring functions, the regular function declaration and arrow functions. Arrow functions are more compact, but we'll use those when we're comfortable with regular functions since they have some minor differences. Function definitions vary from language to language, in javascript `function` keyword indicates that a function is being declared, followed by the name of the function, and then brackets `()` which contain a list of parameters to pass in.

So, lets wrap our fibbonacci sequence in a function:

```js
function fibonacci(terms) {
  let last = 0,
    current = 1;

  for (let i = 0; i < terms; i++) {
    let result = last + current;
    last = current;
    current = result;
    console.write(result);
  }
}
```

We can then call it like our functions previously using `fibonacci(20)` and we should get the same output we saw previously.

The part `(terms)` in brackets is called the parameters, these are values we pass in from the outside world. Athough we can access variables outside a function, we generally only do this when we work with closures, which we'll talk about when we introduce arrow functions. This approach helps with encapuslation, a concept we'll touch on later.

## Exercises

We're far from done with javascript, but with the basics laid out, now is a great time to practice with some exercises that introduce more concepts:

1. Explore - Could we use the addition assignment operator when calculating the fibonacci sequence? Why or why not?

2. Fizzbuzz - fizzbuzz is a counting game where for every multiple of 3, you say fizz, for every multiple of buzz you say buzz. Write a program that prints a game of fizzbuzz to the console up to 100. The remainder `%` operator will help you in this classic interview question. as `current += last;` in our `fibonacci` function instead? Why or why not?

3. Reversing - Given a string, reverse the letters in that string using the accessor `[]` operator to get each character. Then reverse the words checking for spaces with the equality `==`, `!=` operators. Finally Explore how you'd do this more easily with built-in functions.

4. Recursion - Looping isn't the only way to create the fibonnacci sequence, you can also use a programming concept called recusion, where the function is called within itself. Create a new version the `fibonacci` function which calls itself to calculate the value of a single term in the sequence. From the perspective of performance, why might this version be worse?


## Putting it all together

We're very much not done with any of the technologies. There's a lot of language features in javascript alone to wrap your head around, but now is good a time to put the pieces together. We've already seen how css and html can work together, it's pretty difficult not to! However, currently, we have no idea how javascript fits into the mixture.

## Two ways to add javascript

We saw with css that there's two ways to attach css to a page. Inline, using the `<style>` tag, and downloaded as a seperate file using the `<link>` tag.

We can also do this with javascript. We already know we can add inline code using the `<script>` tag like so:

```html
<html lang="en-GB">
  <head>
    <title>My Title</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <style>
        body {
            width: 550px;
        }
    </style>
    <script>
        alert("wily fox");
    </script>
  <body>
    <p>
      The quick brown fox
      <strong>
        jumps
      </strong>
      over the lazy dog.
    </p>
  </body>
</html>
```

Now, you might think we'd use the `<link>` tag to add a javascript file. That would be a perfectly reasonable assumption, too easy. Instead we use the `<script>` tag again, but this time we include a `src` attribute:

```html
<script src="yourcode.js">
```

The browser will then load a file located at the source path provided, and execute the contents of the file. Great, how do we modify a webpage using javascript? With something called the DOM.

## Counter

So let's quickly use the DOM. Firstly, create a goal: Make a button that counts how many times it is pressed.

Create a document, and put a button on the page. How do we detect presses? Well one of the simpliest ways to connect up a button, with javascript is through the associated html attributes. In this case, we want to use `onclick` to call a function whenever we click. We can then assign a function we've created, to this attribute, so that it is called when we click. In computer science, we typically refer to functions used in this way as event handlers, or listeners, since we intend to attach them to events like `onclick` and often their function name will reflect that with some sort of convention, such as putting `handler` in the name.

Next, we need to keep a track of the value. There's lots of ways to skin a cat. For this one, for the sake of simplicity, we're going to use a variable outside the function.

Previously we learned about the let function. If you forget to let a variable, you inadvertently create a global variable. This means the value is exactly the same absolutely everywhere that the variable is used, except maybe if you let that variable within the context first. As a result, forgetting to define a variable with let before asigning it is a great way to shoot yourself in the foot.

## Dom

An object model is a data structure that can be used by a program to inspect and manipulate data. The Document Object Model, or DOM for short, is a special kind of Object Model. We've touched on this before, but now is a good time to provide a little more detail. When the browser opens a webpage, it downloads the html, and as the data is streamed in while the DOM is constructed.

The DOM is an representation of the html document, it's tags, attributes and structure, parsed out from the string that consitute a file. This data structure makes it much easier to inspect and modify the html programatically, both for you as a developer, and the browser during rendering. Since the browser will recognise any changes to you apply to the dom, and rerender the page, this makes changing pages easy.

## Interacting with the dom

Finally, we want to display that value on the screen. To do that, first we need the element from the dom to edit its contents. To do this, we first need a way to locate the element. By adding an `id` attribute to the tag we can then select the element by calling `document.getElementById()`. This will return an object that acts as a proxy to the dom. So let's do that.

## Caviats

Script tags come with one other major caveat. Code execution begins as soon as the script tag is parsed. This sounds all well and good, but what it means is that code can execute before the dom is fully constructed.

We sidestepped this issue by adding the OnClick event to the html itself. This makes it impossible for the javascript to error before the document is completely loaded. Lets try demonstrating this issue, by instead getting out button and attaching our click handler programatically instead. 

To do this, we can use either `element.addEventListener("click", listener);` or `element.onclick = listener;` on the element we got before to attach to it. Hopefully, we should find our code no longer works properly.

How do we resolve that? well, there's two solutions, the quick and dirty solution is to simply move the script tag to the bottom of the page. This means the browser won't find and execute our code until after the element we're interested in is accessible in the dom.

This works well to begin with, but long term, we might encounter a situation where we don't specifically control where on the document our tag lives. It's common to encounter this kind of problem in libraries. So how do we get around this? There's a whole bunch of different ways. Generally these solutions have one thing in common, attaching to an event and running any code dependent on our document there instead. One way to do this is adding an event listener to  the `window` object to be called when the `loaded` event is fired.

## Objects

We've been inavoidably using objects for a while now, but I'm going to touch on those a little bit just for some context for now and then next time we'll look at them in more detail.

At it's most basic, objects are containers, for both data values, and methods. Methods look just like functions, but they operate within the context of the object, so they have access to any values defined on that object.

We've already seen how we can use the accessor operator `.` to get members, the fancy name for both values, and methods.

We can see this if we take an object we've worked with already like `window` and type its name into the console. If we expand the result, we'll see values, and some functions. If we take a look at our `document` we'll see a big long list of all the events that can be attached. We're going to pretend any of the complexities here, like `<prototype>` don't exist for now. 

Where objects become powerful is in a concept called encapsulation. This means we create objects with a specific goal in mind, and aim to reduce side effects (changes outside objects) by using proper oop. We also mentioned about doing this in functions, the idea being that a function does a self contained thing, rather than effecting lots of values.

Next time, we're going to introduce two that are built into javascript, soon enough we'll be writing our own

## exercise

We're going to create a basic calculator. We're going to use the eval function, simply because the `eval` function is a method of writing code best avoided, and as we work with with the exercise it should gradually become clear why `eval` is so dangerous.

## Resources

1. https://youtu.be/q1qKv5TBaOA - How principled coders outperform the competition - Gives a great overview of best practices. Some things to think about long term.

2. How JavaScript Works - Dennis Crockford - Worth reading if it's anything like it's predicessor, "Javascript The Good Parts" from the same author.

3. https://github.com/getify/You-Dont-Know-JS - You Don't Know JavaScript - Available as both a paper tome and free online.