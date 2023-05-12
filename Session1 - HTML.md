# Session One - Foundations
## Notes for Learning

Stop me if i get either too obvious, or too technical.

Important to not get frustrated.

Early on, I expect you'll have fewer questions, just because you won't know what to ask. Ask me any questions you have anyway, as we go along.

I'll do my best to answer them, and anything i can't answer, we can look at docs. There's no shame in having to look things up. The field is far too big to know everything all the time. I still make mistakes, i still have to look things up constantly over a decade later. I still have to look up the structure of an html document when creating a new one.

I'm sure it'll be a lot to take in, especially the later concepts, but don't worry too much. Best of luck to the both of us, I know I need it.

# very quick html overview

Introduced in '92, HyperText Markup Language is the main language of the internet. HTML, while a language, isn't programming. We won't get to any programming until javascript, but html will act as a light introduction to the topic of webdev. Since html is less technical, I've added a little bit of computer science to set the scenes.

## setup github account

Go through procress of creating a github account and pages repo

## tags

All html is made of elements. Opening tag, content and closing tag.

```html
	<p>
		The quick brown fox jumps over the lazy dog
	</p>
```

## nesting

Tags can also be nested. Any tag that is opened must be closed before its parent tag. Show examples of valid and invalid html.

```html
<p>
	The quick brown fox
	<strong>
		jumps
	</strong>
	over the lazy dog
</p>
```

## attributes

Attributes can be used to modify a tag's behaviour.

```html
<p style="color:red">
	The quick brown fox jumps over the lazy dog
</p>
```

## void

Finally, void elements have no closing tag.

```html
<img src="./image.png" alt="description />
```

Some tags mandate that the tag be a void element. `img` and `input` are probably used most often. A slash in a regular opening tag is ignored. It cannot be used to close elements like `script`. Some variaties of markup, like xml and react allow any tag to be a void tag.

## closing

the browser in general will do a lot to save you from html that doesn't validate.
when learning, this is often the main source of misconceptions among beginners.
as a result you'll see lots incorrect html, around the internet

# creating an html document

```html
<!DOCTYPE html>
<!--
	legacy preamble from the early 90s.
	
	Specifically, this element tells the browser that it's received an HTML page.
	
	This block, is a comment. Sometimes comments get used to contain things that aren't comments, silly, I know. In this case, your document likely won't work properly without the doctype.
-->
<html lang="en-GB">
	<!--
		Root element, for html, must be this type, wraps everything
	-->
	<head>
		<!--
			The head contains information about your page that isn't content for now, we're only going to use it to contain meta data, but in the future it will contain scripts and stylings
		-->
		<title>My Title</title>
		<!--
			the title that the browser displays for the page.
		-->
		<meta charset="utf-8" />
		<!--
			Sets the character set used.
			
			This is where a little history lesson might help.
			
			you almost certainly know that everything in your computer is represented by ones and zeros. It will take a while to think in those terms. The whole thing, code, stuff you type, numbers, audio, it's all a representation of ones and zeros.
			
			Some of the choices made for those representations are arbitrary, but most are convinient.
			
			In the early days of computing, when memory was at a premium, charsets were used. These were effectively little dictionaries of numbers, that matched up with a glyph, or letter. This meant that Latin characters, might use something like ASCII, while another writing system like cyrillic would have a different character set.
			
			Things got messy very quickly, so utf8 was created. The u in utf stands for unified, the idea being utf would cover as much of the character space as possible, hell, even emoji are unicode.
			
			For the most part, unicode is successful in what it does, so, suffice to say, this isn't something you need to understand now, but if you decide to take programming further, understanding the concepts behind character sets will prove essential.
			
		-->
		<meta name="viewport" content="width=device-width">
		<!--
			Later on when we get to css, we'll probably discover the concept of a viewport, for now, it's enough to understand that the viewport is a visual container above our page. Device-width is magic that forces the page to be rendered at the size of the device.
		-->
	</head>
	
	<body>
		<!--
			The body is the main rendered content. Not everything in the body is visible, but everything visible is in the body.
		-->
		<p>
			<!--
				A single Paragraph. Short reader unfriendly and esoteric naming exists throughout html. They are more abundant in older html, but unfortunately are unavoidable.
			-->
			The quick brown fox
			<!--
				Shock horror, some actual text, that appears on an actual screen. Everything prior, besides the title tag, could be considered boiler plate, since it's not really doing anything. Instead it ensures nothing breaks. 
			-->
			<strong>
				<!--
					strong is a newer tag, representing emphisis on a specific element. Prior to the existance of css, or the strong tag, we used tags to modify fonts. In this case tags like b and i to modify, text so that it is bold or italic.
				-->
				jumps
			</strong>
			over the lazy dog.
		</p>
	</body>
</html>
```

You might notice whitespace exists in abundance in the file. Browsers perform a little compression on whitespace, all whitespace, however big or small, will always be compressed into one single space in the final page. There are ways around this, and sometimes it can cause formatting problems, ones beginners encounter pretty quickly.

You're probably wondering how you create l like <. Well, the creators came up with a solution to that called character references. Character references contain an ampersand, followed by a string, and are then closed with a semicolon. For exmaple, >'s reference is &gt;. Since & triggers the start of a reference, ampersand has it's own reference too, &amp;. In computer science, this process of creating a new way of interpretting is called escaping, and we'll come across this all the time.

# Browser Mechanics

While you won't need any of this in order to write html, I'd like to go over some of the technical background.
This is mostly to act as a diversion from what I've been covering, we're going to touch on some computer science.
and to cover some technical aspects of the internet while we're otherwise not too worried about being technical.
It'll also serve to give you an idea of where else to read if you'd like to delve deeper.

## How a Browser Works (..in the 90s and beyond)

User navigates to an address.
Browser finds the server.
Browser connects to it and sends a page request.
Server processes request and sends a response.
Browser renders the response.

This whole process raises a few questions.
How computers know where to find each other?
How computers talk to?

## Where Art Thou?

The first step in navigation is a DNS lookup.
One of many acronyms in software development, DNS stands for Domain Name Server.
Domain Name Servers are servers known by their IP addresses.

IP addresses can be used to connect directly to a computer elsewhere on a network, or the wider internet.
Performing a DNS lookup is akin to looking up an address on google maps.
At its simplest, your browser says "hey, DNS, where is dns.google.com?".
The server will then reply with "you can find that at 8.8.8.8".

## Computer Linquistics

Now that we have an IP address, we need to actually talk to a server.
Underlying all communication across any network is the Internet Protocol Suite.
This suite is commonly called TCP/IP.

The internet protocol suite outlines a whole bunch of protocols and how IP addresses should be formatted.

User Datagram Protocol (UDP) is the most basic of these.
Online games will use UDP because its fast, and doesn't care if data gets lost.

Introduce Byzantine Generals Problem.

Transmission Control Protocol (TCP) is built apon UDP.
TCP adds provisions for reliable data transmission.
It does this by detecting missing messages and resending them.
And ensuring received messages are in the correct order.
How it does that for now doesn't matter, it's just enough to know that data reliably goes in one end and out the other.

HyperText Transfer Protocol (HTTP) is then built upon TCP.
HTTP defines the different methods for connecting and talking to servers directly.
Browsers send Requests like Get, with information attached to them.
Servers respond to those requests with codes, and a body of text.
You'll be most familiar with 200 (Success) and 404 (Not Found).

## Response

When a response is received, the browser can begin work.
There's many processes that take place in a very short space of time.

### Parse and Build Object Models

Firstly, the browser parses the HTML into Document Object Model (DOM).
We'll get to interact with the DOM more when we get to Javascript.
Once the DOM is created, it is scanned for resources and prioritises their loading order.
Any resources it finds the browser will also load.

Next, the browser builds  a similar object model for the css, and compiles any javascript.
I'm intentionally brushing over this because we'll get to those in context.

### Rendering

Rendering is the next major step in processing.
The Dom is Combined with the CSSOM into a render tree.
During this step, elements that don't render, like the head tag, are discarded.

Now that we have a render tree, we need to lay out the geometry of each node on the tree.
Each node is a box, so this step determines the size and position of that box.
The first time this happens, is termed a Layout.
Subsiquent modifications to the properties of an element are called Reflows.
Layout is a complicated process, and its many quirks will be the source of all kinds of headaches.
Much of web dev is avoiding and mitigating these headaches in the future.

The last step is painting or rendering.
Painting, as the name suggests, is the process of converting all the previous steps into the visuals seen on the screen.
Painting will be done in what is referred to as a framebuffer.
However, some elements, like canvas, and video, will render in a seperate layer.
To prevent continious redrawing, these elements are combined in the frame buffer in a process called compositing.

Since this is already getting quite technical,
I won't go into any more detail because I'm already deep enough in the weeds.

### Exercises

- Introduce HTML elements. Create a single page. Maybe a recipe or letter? aiming to get familiar with the basic tags.
- Introduce Anchor links. Add a contents list, link each section of text from the content list.
	-In page links.
	-Cross page links.
- Add a font.