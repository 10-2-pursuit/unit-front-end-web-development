# Introduction to the Document Object Model

## Learning Objectives

By the end of this lesson, you should be able to:

- Understand how HTML can be drawn as a tree.
- Relate HTML elements to parents, children, and siblings.
- Define the DOM.
- Explain what role the DOM plays on a web page.
- Connect an external JavaScript file to an HTML file.
- Explain what the attribute `defer` does and why it is needed.
- Identify common DOM manipulation patterns:
- Query for an element.
- Edit an element.
- Add an element.
- Remove an element.

---

## Setup

Begin by forking the following GitHub repository.

- [Starter Code](https://github.com/pursuit-curriculum-resources/starter-intro-to-dom)

> **Note**: There are two different pages to reference: dog and nameplate. The first set of questions will reference the dog page. The second will be for the nameplate.

## Dog Page

### Guiding questions

- What adjective describes native (to the browser)JavaScript methods for DOM manipulation?

- The `document.createElement()` method will create a new element. What argument does the `.createElement()` take?

- At least four different methods allow you to attach elements you've created to the DOM. What are those methods, and how do they differ from one another? (If you don't remember them, how can you look them up?)

- In your app, write code in the `script.js` file that adds a `span` element to the `h1` element currently on the page. The `span` element should come _after_ the text.

- In your app, update your code so the following text appears inside the `span` element. What attribute can you use to set this text?

```
(They're all good dogs!)
```

- Add the `underline` class to the `span` element you created with JavaScript. Did you use `.setAttribute()` or `.classList`? Why?

- Create the following HTML structure with JavaScript before adding it to the `main` element.

```html
<article>
  <img
    class="animated"
    src="https://placedog.net/500/450"
    alt="Amber, the dog."
  />
  <h2>Amber</h2>
  <p>A sweet little doggo that belongs to my friend.</p>
</article>
```

- Create another `article` element with the same structure as above. However, make the following changes:

- Change the `src` attribute to be equal to `https://placedog.net/500/441`.
- Change the name of the dog. Update the `alt` attribute and the `h2` element with the new name.
- Change the description for the dog.
- Add a `featured` class to the `article` element.

- At this point, you likely have a lot of duplicate code. What are some of the issues with having so much duplicated code?

- Can you create helper functions to help DRY up this code? Create at least one helper function now.

- Look at the following array, which contains a single object. As you can see, much of the variable data has been removed and placed in this object.

```js
const dogs = [
  {
    name: "Amber",
    description: "A sweet little doggo that belongs to my friend.",
    imageNum: 450,
    featured: false,
  },
];
```

First, add a new object to the array above that includes the name, description, and image number (i.e., `441`). Finally, set the `featured` key to be equal to `true`.

Next, loop over the array. Inside the loop, use the code you've written to create both of the articles. You can do so by substituting your hardcoded values (e.g., "Amber") with those accessed via the object.

- Reflect on what you've just accomplished. What was difficult about it? What benefit did you get?

- Add at least one more dog to the array, and watch as your list of favorite dogs grows.

![Image showing a completed dog tutorial.](../assets/completed-dog-tutorial.png)

## Nameplate

Go to the nameplate page on the websiyour appace "Your Name" with your actual name and input your birthday. (Don't worry, no one else will look at this.)

### Set up

- Connect the `script.js` file to the `index.html` page by adding a `script` element. What attributes are needed on the `script` element to do this?

- Add the following line to your JavaScript file. After clicking the "Run" button, does it log? (If not, check to make sure your `script` element is correctly formatted.)

```js
console.log("Just testing...");
```

### Guiding questions

- What does `document` represent?

- What data type is `document`? How do you know?

- What is the difference between `document.querySelector()` and `document.querySelectorAll()`? Keep in mind the following when answering this question:

- What is the functional purpose of each method?
- What is the return data type of each method?
- What argument is expected for each method?

- What is the `defer` attribute, and why is it necessary when writing JavaScript that accesses the DOM?

- In your JavaScript file, use `document.querySelector()` to select the `h1` element. Then, log out the text that is stored inside of that element.

What attributes will allow you to select the text inside of the element?

- What is the difference between the following two lines of code?

```js
document.querySelector("main").innerHTML;
document.querySelector("main").textContent;
```

- Using `document.querySelector()`, select the element with a class of `emoji`. What emoji is selected? Why?

- Is it possible to select the second emoji on the page with `document.querySelector()`? If so, how? If not, why not?

- Select all emojis on the page with `document.querySelectorAll()`. Then, loop through the returned value and log out the content of each element.

How did you choose to loop through the `NodeList`?

- Write code that removes all of the emojis from the page. Why must you use some kind of loop to do this?

- What code could you write that would remove _only_ the second emoji from the page? If possible, think of multiple ways to perform this task.

- Based on what you know, can you remove only your birthday from the page, excluding the text "My Birthday:"? If so, how so? If not, why not?
