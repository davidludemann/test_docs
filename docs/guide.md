# Coding Standards

## Overview

This document serves as a complete overview of Carroll Bradford's coding standard for CSS and the Javascript language.

The issues in this document cover not only aesthetic formatting issues, but also coding standard conventions.

## Javascript

#### General Rules

-   Use `lodash` library where possible.
    -   Lodash has a lot of **advance** Array / Object manipulation. Don't try to re-invent the wheel stringing together javascript `maps` and `filters`.

#### Variables

-   Use `const` and `let` for all variables. Avoid `var`. This prevents variables being re-assigned which lead to difficult bugs to fix. If a variable **needs** to change use `let`. `let` provides block scoping rather than function scoping.

*   Group all your consts and then group your lets. This allows for better readibility.

```javascript
// Bad
let i;
const items = ["beach", "lake"];
let name = "string";
const len;

// Good
const len;
const items = ["beach", "lake"];
let i;
let name = "string";
```

```javascript
// Bad
var username = "username";

// Good
const username = "username";
```

Example of block scope vs functional scope

```javascript
function () {
    if(true){
        const a = 1
        let b = 1
        var c = 1
    }

    console.log(a) // Reference Error
    console.log(b) // Reference Error
    console.log(c) // 1 - This could easily start leading to deep bugs
}

```

#### Objects

-   User Object spreading `...` to assign new values to an object.

```javascript
//Bad ಠ_ಠ
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // This mutates the object

// Good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 };
```

#### Arrays

-   Use array.push() instead of direct assigment for adding onto an array.

```javascript
const someArray = ["apples", "oranges", "pears"];

// Bad
someArray[3] = "banana";

// Good
someArray.push("banana");
```

-   Use array spreading to copy arrays

```javascript
const fruits = ["apples", "bananas", "pears"];

// Bad
const fruitCopy = [];
for (var i = 0; i < fruits.length; i++) {
    fruitsCopy[i] = fruits[i];
}

// Good
const fruitCopy = fruits.map((fruit) => fruit);

// Best
const fruitCopy = [...fruits];
```

#### Destructing

-   Use object destructing when accessing multiple properties of an object. Destructuring saves from creating temporary references (saves memory), and from repetitive code.

```javascript
const nameString = getNameString({ firstName: "John", lastName: "Doe" });

// Bad
function getNameString(user) {
    const firstName = user.firstName;
    const lastName = user.lastName;

    return `${firstName} ${lastName}`;
}

// Good
function getNameString({ firstName, lastName }) {
    return `${firstName} ${lastName}`;
}
```

#### Strings

-   Use single quotes `''` for strings.

```javascript
// Bad
const name = "John Doe";

// Bad - Only use string literals for interpolation
const name = `John Doe`;

// Good
const name = "John Doe";
```

-   Use string template strings instead of concatenation when programmatically building strings.

```javascript
const name = "John Doe";

// Bad
const string = "Good morning, " + name + ".";

// Good
const string = `Good morning, ${name}.`;
```

#### Functions

-   Use arrow functions for anonymous function calls. It will automatically execute functions in the context of `this`, and has a more concise syntax.

```javascript
let someNumbers = [1, 2, 3, 4];

// Bad
let modifiedNumbers = someNumbers.map(function (number) {
    return number * 5;
});

// Good
let modifiedNumbers = someNumbers.map((number) => {
    return number * 5;
});

// Best (if you have one parameter)
let modifiedNumbers = someNumbers.map((number) => number * 5);
```

## CSS & Convention (U.M.C.E)

#### Overview

We will be using a specific naming convention for our css classes. This class naming convention was designed to promote quick reading and writing of classes. The goal is to be able to quickly read a class and know exactly what it is doing, and who wrote it. Rules and Examples will be provided below.

#### Rules

---

##### General CSS Rules

-   Keep CSS properties lowercased

    ```css
     {
        // Bad
        color: #e5e5e5;

        // Good
        color: #e5e5e5;
    }
    ```

-   Use shorthand properties where possible

    ```css
     {
        // Bad
        border-top-style: none;
        padding-bottom: 2em;
        padding-top: 2em;
        padding-left: 1em;
        padding-right: 1em;

        // Good
        border-top: 0;
        padding: 2em 1em;
    }
    ```

-   Follow the following template in terms of spacing, tabing, and formating.
    ```css
    * {
        background: green;
        padding: 1em;
        margin-top: 1em;
    }
    ```
-   Group Sections by comments if applicable

```css
// =====================================
// HEADER & NAVIGATION
// =====================================
.cbb__module__navigation {
    ...;
}

// =====================================
// DUMPSTER
// =====================================
.cbb__module__dumpster {
    ...;
}

// =====================================
// BIDS
// =====================================
.cbb__module__bids {
    ...;
}
```

##### U.M.C.E Rules

-   We only use a double underscore `__` and dash `-` to seperate words.
    -   Double Underscore `__` will be used to seperate identifiers
    -   Dash `-` will be used to seperate compound nouns and adjectives.
-   Each Prefix is ALWAYS required.
-   We will use 3 types of dom elements. (hiarchical order).
    -   Layout (`layout`)
    -   Module (`mod`)
    -   Component (`comp`)
-   Write css classes in heirarch order
    -   Example:
    ```html
    <div class="cbb__comp__data-entry mr-1"></div>
    ```
-   Everything MUST be lowercase. No capital letters anywhere

#### Structure

---

The basic structure is as followed:

> **{prefix}\_\_{type}\_\_{identifier}**

-   **prefix**: To distinguish between internal frameworks and third parties.

-   **type**: This will be one of the 3 available types (layout, module, component).

-   **identifier**: Descriptive name that will easily describe what the target is. Compound adjectives & nouns will be seperated by a dash `-`

##### \*\*App Specific Notes on Theming\*\*

The `theme.sass` will already contain the majority of theme options. It will export SASS and CSS variables to be able used in custom CSS styles. This will automatically style imported components from PrimeFaces.

When creating components use the color variables from `theme.sass`.

If a custom element is being created, you may drop the `type` and do the following:

> **{prefix}\_\_{identifier}**

```css
.cbb__btn {
    ...;
}
```

#### Examples

---

```css
==================================
// LAYOUT, MODULE, COMPONENT 
==================================
.cbb__layout__main-page {
    ...;
}
.cbb__mod__navigation {
    ...;
}

.cbb__comp__navigation-bar {
    ...;
}

.cbb__comp__navigation-link {
    ...;
}

==================================
// THEMING
==================================
.cbb__btn {
    ...;
}

==================================
// MODIFIERS
==================================
// Bad
.cbb__btn-active {
    ...;
}

// Good
.cbb__btn .-active {
    ...;
}
```

##### Things to keep in mind

-   Follow a utility style approach. Try to write a class that could be generalized and used through out the codebase.
    -   For example a card class would be the same throughout, but there might be small changes in the indidual elements inside. Make one class for the card, and one class for the element instead of making two classes to style the container, and two for the different elements inside.
    -   Use only a utility classes from bootstrap instead of creating one.
        -   For example if you need just a margin-right of 1em, favor adding the class `mr-1` instead of making a new class name, and entry in the css file.
-   Avoid CSS Hacks
    -   If you have to hack something, re-think the approach.
    -   Hacks should be considered last resort as they will hurt in the long run.

##### Practical Example

The following example shows every use case of the 5 types, and a utility approach.

```html
<main class="cbb__layout__main-page">
    <header class="cbb__mod__header">
        <nav class="cbb__comp__navigation">
            <li class="cbb__comp__navigation-link">Home</li>
            <li class="cbb__comp__navigation-link">Construction</li>
            <li class="cbb__comp__navigation-link">Dumpsters</li>
        </nav>

        <div class="cbb__comp__navigation-btns">
            <button class="cbb__btn">Settings</button>
            <button class="cbb__btn ml-1">Logout</button>
        </div>
    <header>

    <section class="cbb__mod__data-feed">
        <div class="cbb__comp__data-entry cbb_theme_card">
            <h1 class="cbb__comp__data-entry-header">Entry Title</h1>
            <p class="cbb__comp__data-entry-content">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                Morbi ornare rhoncus lacus vitae rhoncus.
                In hac habitasse platea dictumst.
            </p>
        <div>
        <div class="cbb__comp__data-entry cbb_theme_card">
            <h1 class="cbb__comp__data-entry-header">Entry Title</h1>
            <p class="cbb__comp__data-entry-content">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                Morbi ornare rhoncus lacus vitae rhoncus.
                In hac habitasse platea dictumst.
            </p>
        <div>
    <section>
</main>
```

## Final Word!

Be consistent! Treat coding as a book. Code with the intention someone **will** read your code. Make it easy for the next person to quickly look at your code and start adding onto the work.
