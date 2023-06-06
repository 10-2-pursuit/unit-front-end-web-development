# Introduction to CSS

Web pages use three technologies: HTML for content, CSS for style, and JavaScript for functionality. This lesson will cover the basics of CSS (**C**ascading **S**tyle **S**heets)

## Learning objectives

By the end of this lesson, you should be able to:

- Describe what CSS is and what it means that it cascades.
- Differentiate between CSS rules, selectors, declarations, properties, and values.
- Add inline styles to specific elements on an HTML page.
- Add styles to an HTML page using the `style` element.
- Add styles to an HTML page’s elements by connecting an external style sheet.

---

## Getting started

You can either read along or code along.

You can create a new `index.html` file and add the following.

```html
<body>
  <header>
    <h1>Bicycles!</h1>
    <h2>The best bike shop in town<span>!</span></h2>
  </header>
  <main>
    <section><h3>Road Bikes</h3></section>
    <section><h3>Dirt Bikes</h3></section>
    <section><h3>Electric Bikes</h3></section>
  </main>
  <aside>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam debitis
    </p>
    <p>
      harum dolore sunt, quis velit accusantium pariatur! Illo, sed nam
      similique pariatur voluptate doloremque iusto vero quod itaque
    </p>
    <p>eligendi</p>
    <p>deleniti?</p>
  </aside>
</body>
```

## What is a Cascading Style Sheet?

You learned how to add content to a web page when introduced to HTML. However, the appearance of the page was very plain. Additionally, you might have wanted to make a header's text bigger or add a different background color, or put the nav bar on the left side instead of above the main element.

Styling a web page is done with CSS (**C**ascading **S**tyle **S**heets). Cascading explains the behavior of the styling. It means that more than one style can be applied to an HTML element, and the way the element's style will be determined is by setting more general rules and then overriding them with more specific rules.

For example, you might want your web page to have all-blue text.

You could do this by setting up a rule. First, you start with a `selector`, which can be an HTML element name, and then follow it with curly braces.
To code along, you can add a `style` element in the head of your HTML file.

```html
<head>
  <style>
    /* Add rules here */
  </style>
</head>
```

```css
<style>
 body {
 }
</style>
```

You would set the property (`color`) within the curly braces and value (`blue`).

```css
<style>
 body {
 color: blue;
 }
</style>
```

This rule will cascade down from the body into all the elements inside. It doesn't matter if the text is in an `h1` element or a `p` element or if it is directly in the body or nested inside several other HTML elements.

However, you might decide that your `h1` should be orange. In which case, you would write a new declaration.

```css
<style>
 body {
 color: blue;
 }

 h1 {
 color: orange;
 }
</style>

```

This will leave all the other text on your page blue, but the `h1` tag will have orange text because the `h1` rule is more specific (make the `h1` text orange) than the `body` rule (make any text inside the `body` blue).

Over time, you'll learn good strategies for when to use more general rules and when to add more specific ones.

## Adding Style

There are three different ways to add CSS styles.

- Internal stylesheets
- External stylesheets
- Inline style

### Internal Stylesheet

In the demo above, you saw how to add an internal stylesheet. You add the `style` tag in the `head` of the HTML file. This method can be great for following a tutorial or building a small demo. However, if you create a website with multiple pages, you'd need to copy-paste all the styles from one page to another and update changes on each page.

### External Stylesheet

A strategy to deal with this is to use a single style sheet and then connect it to multiple web pages on your website.

First, create a file with the extension `.css` in the same folder as your `index.html` file.

```
touch styles.css
```

Then you must connect it using a `link` tag in the html file's head. The link file can link several types of files, so you must use the attribute `rel` with the property `stylesheet` to inform your page you are importing a stylesheet. Next, you must add the path to your CSS file.

```html
<head>
  <link rel="stylesheet" href="styles.css" />
</head>
```

You should test whether the connection is correct by starting with a very obvious declaration. Make the background of the body `orchid` color. Once you've confirmed a link, you can remove the declaration.

```css
body {
  background-color: orchid;
}
```

140 HTML colors have names (like `blue`, `red`, or `orchid`). You can learn about using colors on the web at [HTML Color Codes](https://htmlcolorcodes.com).

### Inline Style

You can write styles inside the opening HTML tags:

```html
<p style="font-weight:bold;text-align:center;">lorem ipsum</p>
```

There are two significant issues with setting up your CSS this way.

- For every additional p tag, you would need to add this code, and every time you change it, you would have to update each p tag
- Inline styles override all other CSS rules. You cannot change the rule set with an internal or external stylesheet.

There are some great ways to leverage inline styles, but we will not cover them now.

### Common styling

Here are some common properties to change

#### Text color

To change the text color, use `color`

```css
p {
  color: gainsboro;
}
```

#### Background color

To change the background color, use `background-color`.

```css
p {
  color: gainsboro;
  background-color: navy;
}
```

### Colors

Beyond the 140 named HTML colors, there are several ways to choose from myriad colors. Using a color picker like [HTML Color Codes](https://htmlcolorcodes.com) can be very helpful.

One of the most common ways to declare a color is using a hexadecimal color. Hexadecimal numbers go from 0 - 16, rather than from 0 to 9. To code 10-15 the letters a, b, c, d, e, and f are used.

- Black's hex code is `#000000` (or `#000` for short).
- White's hex code of `#FFFFFF` (or #FFF for short).
- Reddest red's hex code is `#FF0000`, the first two positions the code represent how red something is.
- Bluest blue's hex code is `#0000FF`, the last two positions represent how blue something is.
- Greenest green's hex code is `#00FF00`, the middle two positions represent how green something is.

Another way you can set color is using RGB(A) (red, green, blue, alpha), which also let's you set a range of red, green, and blue. Additionally, this property let's you set an alpha value (between 0 and 1, where 0 is none and 1 is 100%) which will allow you to make things transparent.

- Black's hex code is `rgb(0, 0, 0)`.
- White's hex code of `rgb(255, 255, 255)`.
- Reddest red's hex code is `rgb(255, 0, 0)`, the first two positions the code represent how red something is.
- Bluest blue's hex code is `rgb(0, 0, 255)` the last two positions represent how blue something is.
- Greenest green's hex code is `rgb(0, 255, 0)`, the middle two positions represent how green something is.
- Black with 50% transparency is `rgba(0,0,0, .5)`

#### Font family

To change the font style, use `font-family`:

```css
p {
  color: gainsboro;
  background-color: navy;
  font-family: sans-serif;
}
```

There are some built-in fonts. Like `serif`, a generic font with small decorations on the edges of the letters. Or sans-serif, which is a more minimalist font. Some other common ones are `cursive` and possibly `fantasy` (depedning on the built-in fonts on your computer, Macs typically have `fantasy`). These built-in fonts can also vary tremendously depending on the user's machine.

#### Font size

Font sizes can be changed with the `font-size` property. There are two main ways to size fonts. One is with pixels `px`, and the other is with `em`, a relative size. `em` is more modern and can provide better consistency across browsers, while px tends to feel more intutive to people. Users will have a set default font-size (usually around 16px) in their browser. Whatever their default is, it will be what 1em is for them. Then 0.5em would be 8px, and 23m would be 32px.

```css
p {
  color: gainsboro;
  background-color: navy;
  font-family: sans-serif;
  font-size: 12px;
  font-size: 1.5em;
}
```

What happens when there are two of the same rules? Which one "wins?" Does CSS generate error messages?

### Text-align

A pretty common thing to do is to center some text. This is as easy as setting a rule:

```css
p {
  color: gainsboro;
  background-color: navy;
  font-family: sans-serif;
  font-size: 12px;
  font-size: 1.5em;
  text-align: center;
}
```

### Borders

You can add a border around an element

```css
p {
  color: gainsboro;
  background-color: navy;
  font-family: sans-serif;
  font-size: 12px;
  font-size: 1.5em;
  text-align: center;
  border: 1px solid gold;
}
```

What is different about the border is that it takes 3 arguments. The first is the width of the border, the second is the border style and finally, the color.

A mnemonic device to remember the order is to say `1 solid gold bar` as the way you would describe a single bar of (solid) gold is the same order you would put the arguments for the border.

### Lorem Ipsum

When you build a website, you likely won't have all the text/content yet. But as you make the website, you want to ensure that what you're building looks good and the sizing is correct. You can include some placeholder text, usually called `lorem` or `lorem ipsum`. Within your text editor, you may notice if you start typing `lorem` into an HTML document, you can auto-complete it to fill an element with some lorem text.

You can also search for `lorem Ipsum generator`, which will provide several websites that generate some themed placeholder text.

### Learning as you go

The basics of CSS are simple to learn. However, there are hundreds of properties! The best way to learn beyond the basics is to use a search engine and search for what you want to accomplish and look at code examples. You will continue to encounter new rules all the time and that's normal with coding. Learning from someone else's code is a key skill.

Rules that you use regularly, you will naturally memorize. You will look up the rules you use infrequently as you need them, and that's fine!

Additionally, while it is easy to add style to a page, adding style well and creating a responsive website is complicated and takes a lot of practice and time. Throughout the rest of this course, you will be building web pages and websites, granting you plenty of opportunities to practice and improve over time.
