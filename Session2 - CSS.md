# Session Two - Drapes

# Basic CSS, if such a thing exists...

As we've already seen, you can use the style attribute in html to add a look and feel to text, however became clear those would be inflexible and quickly get cumbersome. Thus bringing us to CSS's inception, in 96'. Its original aim was as a means of sharing these styles, without repeating yourself over and over.

In the modern web development world, its involvement has become a lot more complicated. Pre-processors for CSS like sass and less, add features to CSS making your stylesheets much simplier. Server side templating and react have also significantly reduced dependancy on CSS directly, and as such, css has been forced to innovate in order to remain relevent.

However, all the alternatives at their heart build apon CSS in some way. As a result, understanding it is especially useful when things go wrong.

## Programming?

Previously we learned about HTML, a format that transfers text with mark-up that provides meta-data. Like HTML, CSS isn't programming either. The goal of CSS is collaborative, but where HTML tells the browser what to render, the CSS tells the rendering engine how to render.

To do this rules are designed, called selectors, that match against specific elements of your page. Then during rendering, property changes attached to that rule are applied to that element. Changes might change the colour, move, or completely hide an element, or even animate it. Changes that CSS make are (almost) entirely visual. If on your internet adventures you've ever seen a very odd, bland looking page, that's often because the CSS hasn't loaded properly.

# Rulesets

The typical structure of a css document is a big collection of rulesets. A ruleset contains all the information that the rendering engine needs to set the look and feel of a specific element.

To give a basic example, a simple css document might look something like this:

```css
/*
	This is a comment in a css document.
	The parser will ignore anything inside the two slashes and stars.
	They can span multiple lines, or be one line long.
	There's no single line comment.
*/

span {
  /*
		This is the selector, this tells the renderer that you want to render this 
		rule onto span tags. The selector acts as a constraint, matching a specific 
		element based on a few rules.
	*/
  background: cornflowerblue;
  /*
		This row is a declaration.
		The declaration contains a property to be changed and a value to change 
		it to.
	*/

  color: ;
}
```

On the face of it CSS is pretty simple, but there's lots of different ways to select a specific element. On top of that there's hundreds of different properties you can change, all with their own caviats, expectations and oddities. We'll get to some of those in a minute.

However, CSS is also not without its legacy. For example, there's a collection of predefined colours like `CornflowerBlue` from above, but due to a historical hang up, `DarkGrey` is actually lighter than `Grey`. The quirks in css will often feel never ending, and how the rules and quirks of the rendering engine interact can quickly make CSS an absolute beast. Where CSS begins to get complicated is that selectors are dependant on the DOM, and when rulesets all begin to interact with each other. Our main stylesheet is over 18k lines. Its coverage however, on any given page, is usually less than 50%. This means that over half the css loaded on a page is doing nothing to that page.

There's no cheat code, mastering CSS is something that can be quickly explained, but will simply take time, and experience. Regardless, working with CSS often becomes a case of managing complexity.

# Selecting multiple elements

Selecting multiple elements is pretty simple. Similarly to HTML, CSS largely ignores excessive whitespace, so applying an additional selector is as simple as putting a comma between them.

```css
span,
p {
  background: DarkMagenta;
  color: #fff;
}
```

This just means the selector will match both `<span>` and `<p>` tags.

# Values

You'll also notice i've added a new rule, and this has an odd looking value in it, rather than a reader friendly name. While I could've used the word `white` in the spot of `#fff`, for academic reasons I've opted to instead use a hex color code. In the case of a colour, there's a couple of different formats you can use, to choose abitrary colours at will.

Each property that can be set, outlines the format for the value that can be used, and sub values. Hopefully you'll get a hang of the shape of values used most regularly with time.

# Dirty hands

If we go back to our HTML from previously, we can start to make it prettier by creating a `<style>` tag in the head. There are other ways to add style, and CSS to a page, but for now, we'll embed it into the page directly.

# Selector Rulesets

Selectors come in a couple of different flavours. We've already seen the element selector above. The different types allow for some exceptionally advanced behaviour without much extra legwork. This is part of the reason CSS is so popular. The other reasons are a mystery to me.

The selectors you'll use the most initially are class and id selectors, and you'll probably use these more than the combinators we will get to in a minute.

These are relatively simple, to select a given element `<div id="my-id" class="my-class"></div>` by its id, you'd use `#my-id`, leading the id with a hash. Similarly, you'd select it via its class `div.my-class` with a period.

The mechanics behind class and Id differ, slightly. Traditionally an id should be unique, Meaning there should only be oneelement id on a page, whereas a class can have multiple. Browsers generally won't complain about all sorts of validation issues, preferring instead to render something.

As you'll see, you can combine selectors to select a single element with more than one constraint like `div#my-id.my-class`.

There's a couple more selectors, the attribute selector, allows selection based on a specific attribute in the html, so, for example `div#my-id` and `div[id="my-id"]` would be equivilent, while div[id] would select any element that has an id defined. Attribute selection can have more more complicated rules, but I have to look them up when I need them.

Finally we have pseudo selectors, these are niche selectors, but they are often more useful than attribute selectors, and generally hard to describe as one specific use. The `:hover` selector is by far the most widespread of these selectors. This selector matches whenever the mouse hovers over the element in question.

# Combinators

On its own, Selectors would be pretty limiting. So, as the name suggests, Combinators combine selectors. They allow the styling to adapt to the structure of the document.

The simplest, and by far the most important combinator is the decendant combinator. You'll remember that every tag in HTML must be closed, and that elements can contain other elements. The decendants combinator simply selects tags contained within a given tag. So, for example, the selector `div a` would match the a tag below.

```html
<div>
  <p>
    <a>selected</a>
  </p>
</div>
```

This differs a bit from the child combinator. The child combinator uses an angled bracket (>), and a selector using the child combinator would look like `div > p > a`. This duality is probably quite unexpected to a newcomer, so it's important to recognise this distinction.

There's a couple more combinators, both of them refer to sibling relationships. The adjacent sibling combinator uses a plus (+) and selects an element that is directly next to the other element in the structure, while the general sibling is denoted with a tilde (~) and selects elements that share the same parent.

You may notice the complete lack of a parent combinator, ie, the opposite of the child combinator. A combinator using the counterpart angled bracked (<) seems pretty intuative right? well, it doesn't exist in CSS, and is likely never coming. Recently, ways to acheive the same goal have been added, but that requires thinking about the problem from a slightly different perspective. Rather than selecting a child, and walking up, this is implemented through the use of a `:has` pseudo selector, looking for specific children. There's a whole bunch of other pseudo selectors like this, so we won't talk much more about them.

And that's it for selectors. That's everything you need, or could possibly need to know about them.

# Boxes

Elements exist as boxes. These boxes are unavoidable, and in Web Dev, we refer to them as the box model. The way an element is drawn is mercy to the box model.

```css
/*
	Here we have a ruleset, we're going to use this ruleset to introduce the 
	box model, since it's intrinsic to rendering elements. The box model is 
	made of several different components you'll see referred to in css. There's 
	lots of properties to introduce to understand the box model, so we're going 
	to break them down one at a time.
*/
div.box {
  display: block;
  height: 200px;
  width: 400px;
  padding: 0.1em;
  padding-left: 0;
  background: #555;
  border: solid #8b008b 2px;
  margin: 0 auto;
}

div.box {
  display: block;
  /*
		display sets the layout mechanism used by the element. when we've been 
		working with elements in html, we've been unwittingly using this 
		property. Span, for example, has a default value of inline. Div, 
		however, defaults to block, so this property actually does nothing, and 
		you might even see it crossed out in the inspector, indicating that the 
		property isn't active.
	*/

  height: 200px;
  width: 400px;
  /*
		These properties set the size of the box in pixels. You can also set 
		flexible sizes using properties prefixed with min- and max-.
	*/

  padding: 0.1em;
  /*
		The padding creates a space around content rendered within the element. 
		We've set the value to .1em. Em is a typography term, relative to width 
		of an M. We'll find a whole bunch more units while working.

		The padding contributes to the overall width and height of the element, 
		meaning changing the padding will affect how much space the content 
		inside the box has to paint in.
	*/

  padding-left: 0;
  /*
		We can pad a specific direction using a suffix. All of these prefixes 
		and suffixes are predefined properties in the css spec though, you 
		can't invent your own.

		You'll notice we've got no padding here, and there's no units. You can 
		include units when writing zero, but this is perfectly fine because in 
		css, every zero is the same. 0px is exactly the same size as 0em.
	*/

  background: #555;

  border: solid #8b008b 2px;
  /*
		The border is usually the visible edge of the element. In this case, 
		we've created a solid Dark Magenta border of a given width. The Border 
		doesn't contribute to the size of the element, but that can be changed 
		with a specific property.
	*/

  margin: 0 auto;
  /*
		The margin is the final part of the box model, nearly home dry. The 
		margin sits outside the border, and is used to  seperate an element 
		from its neighbours. Margin never contributes to the element size.

		We're seeing two values here. And yet in padding we only saw one?
		well, some properties, like padding, can actually take multiple values, 
		corrisponding to the four directions starting at the top and going 
		around the box clockwise. This is handy shorthand, but you may want to 
		use the suffix version if you only need to replace one value.

		Since there's only two, css will repeat them. In this case, we have no 
		margin at the top and bottom, and something on the left and right, but 
		what does auto do?
		
		auto is a fancy value, it makes the margins take up as much space as is 
		left over, so in this case, the box appears in the middle.
	*/
}
```

# One more thing, Specificity

When two or more property values collide, the browser is presented with a problem. Which does it use? The browser uses a concept called Specificity to choose a single value to use. Specificity in practice is exceptionally complicated, and very difficult to diagnose. Just knowing that it exists behind the scenes will save you headaches.

# Exercises

- Style the previous page.
- Build a flyout menu.
- Make the contents menu toggleable

```

```
