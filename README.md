[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# HTML & CSS Overview

## Objectives

Developers should, at the end of the lesson, be able to:

- Write out the basic skeleton of an HTML page.
- Add CSS to an HTML file by linking to an external stylesheet with `<link>`.
- Explain at a high level how CSS styling works.
- Write CSS and use it to add styling to a basic page.

## Overview

Let's go over the basics of HTML and CSS! Most of you should have some
experience with this stuff already, since you completed the
myGA pre-work and each built a simple website
as part of your admissions process.

### HTML

HTML defines the structure and content of information on the page.

All HTML pages have the same basic structure:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Meta-data goes here. -->
  </head>
  <body>
    <!-- Page content goes here. -->
  </body>
</html>
```

HTML tags generally come in matched pairs, with the format `<tag> ... </tag>`.
The first tag is called the _opening tag_, while the second is called the
_closing tag_.

HTML5 encourages the use of _semantic_ tags whose names reflect their content
and role within the page.

Some of the new elements that HTML5 added are: `<section>`, `<header>`, `<nav>`,
`<footer>`, and `<main>`. These tags help us to structure our content better
and vastly improve accessibility for those who experience our content in
non-visual ways.

Historically, elements could be classified as either: **block** elements or
**inline** elements. Block elements have built-in line breaks, causing them
to automatically _stack vertically_, while inline elements wrap within their
containing elements. One way we can distinguish block elements from inline
elements is to think of block elements as relating to parts of the page,
creating "larger" structures than inline elements.

Even though the HTML5 specification provides different categories for elements,
by default, all elements behave by either creating a new line or wrapping
inside of other elements. These two characteristics are important to
understand because they determine how elements can be styled.

Inline elements are only as large as their contents such that they cannot
have `width` or `height` set with CSS (with one exception: `<img>` is
technically an inline element), and `margin` and `padding` can only be
applied to the left or right of the element. Inline elements can also
be aligned within a containing block element that has the `text-align`
property set on it (including `<img>` elements).

Examples of block and inline elements:

|    Block    |   Inline   |
| :---------: | :--------: |
|   `<div>`   |  `<span>`  |
| `<article>` | `<input>`  |
| `<header>`  | `<strong>` |
|    `<p>`    |   `<a>`    |

Here is a list of [all current elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) on MDN

#### HTML Attributes

All HTML elements are able to support attributes. Attributes vary depending on
their use, but always live within the opening tag of an HTML element.

For example:

```html
<a href="http://google.com">Google</a>
```

Here, `href=""` is an attribute.

Attributes will always follow the `attribute-name="value"` convention.

Below are a list of extremely helpful attributes that allow you to add
custom meta-information to your HTML elements. They become immensely helpful
when targeting these elements with CSS and/or JavaScript.

|                                      Attribute                                       |                                                     Usage                                                      |
| :----------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------: |
|    [`id`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id)    | Value can only be used once, elements can only have max of one ID. Creates a unique identifier for an element. |
| [`class`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class) |                       Value can be used multiple times, elements can have many classes.                        |

Here is a list of all the possble [attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes) and which elements they work with

#### HTML Best Practices: Forms and Inputs

Often websites need to get input from the user - names, addresses, and other
information. When using the `<input>` element, it should ALWAYS be wrapped in
a `<form>`. This is helpful both for accessibility (such as screen readers)
and for accessing that data using JavaScript.

For accessibility, `<input>` elements should have an `id` attribute, which is
used in combination with the `for` attribute on a `<label>`:

```html
<form>
  <label for="lastname">Last Name</label>
  <input type="text" id="lastname" />
</form>
```

### CSS

In the early days of the web, people used to style their pages using explicit
styling tags such as `<font>`, `<center>` and `<strike>` (all of which have
long been **deprecated** and should never be used today). This was inflexible,
difficult to maintain, and conflated _presentation_ with the document structure.

CSS emerged in the mid-90s as a way to make styling webpages easier. It's
core idea was to replace explicit styling in HTML with _styling rules_ which
could be applied to multiple elements; this would have the benefits of (a)
reducing duplication, and (b) separating styling instructions from content.

CSS works by selecting some group of elements (using a special reference called
a **selector**) and defining a set of properties and values to apply to that
group of elements. The general syntax for this is:

```css
selector {
  property: value;
  property: value;
}
```

A specific example is

```css
.article-header {
  height: 100px;
  width: 100px;
  background-color: green;
}
```

- This looks similar to a JS object literal; however, one important difference
- is that key-value pairs are separated by _semicolons_ instead of _commas_.

Since CSS is just a collection of style rules, one key concern is: what happens
if two rules disagree? CSS has two mechanisms to resolve these disagreements
when they come up.

The first is that, if two rules disagree about the value that a property
(e.g. 'background-color') should have, a property called **specificity**
can be calculated for each selector, and the selector with higher specificity
will win out. The short version of how specificity works is that IDs are
more 'specific' than classes, which are more 'specific' than tags, which are
more 'specific' than properties inherited from parent elements.

- Specificity is actually a very precise calculation:

  - +1000pts for each inline style attribute
  - +100pts for each ID
  - +10pts for each attribute, class, or pseudo-class
  - +1pt for each element or pseudo-element tag

- For a more detailed explanation, see this [blog
  post](http://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)
  on CSS specificity, or play around with this [CSS specificity calculator](http://specificity.keegan.st/).

The second mechanism handles when two _equally specific_ rules disagree.
In that case, the last rule that is read by the browser wins! This kind of
behavior is called "cascading", and is where the "C" in CSS comes from.

To add CSS to a page, either include it

1. Inline, within an element.

1. Between two `<style>` tags, typically in the the `<head>` of the document.

1. **Most Common** In a separate file referred to by a `<link>` tag, also
   typically in the the `<head>`. The syntax for using a `<link>` tag is
   `<link rel="stylesheet" type="text/css" href="...">` where 'href' is set to
   the location of the desired stylesheet.

#### CSS Best Practices: Selectors

1. AVOID INLINE STYLES. It's best to keep all your styles in one place, within
   one or more stylesheets.

1. USE IDs SPARINGLY. IDs should be reserved for those rare situations when
   you need to style an element _differently from every other element in your site_.
   There are a lot of selectors to use; it's rarely necessary to use an ID.

[CSS Selectors Cheat Sheet](https://gist.github.com/magicznyleszek/809a69dd05e1d5f12d01)

#### CSS Best Practices: Organizing Your CSS File

As more and more rulesets are added to your CSS file, working within it can
quickly become a challenge. Here are some things that can help make you more
efficient when working with CSS:

1. TAKE ADVANTAGE OF CASCADE, DON'T FIGHT IT. Organize the contents of your
   CSS files from the least specific to the most specific selectors. Generally,
   this means the universal selector and tag selectors belong at the top of the
   page, followed by class and attribute selectors, id selectors, and lastly,
   media queries.

1. ALPHABETIZE YOUR RULESETS AND DECLARATIONS. While it takes a bit more
   effort initially, alphabetizing your rulesets and rules will save you loads
   of time finding specific rules when you need to modify them.

1. BREAK UP LARGE FILES INTO SMALLER ONES. The [`@import` CSS-rule](https://developer.mozilla.org/en-US/docs/Web/CSS/@import)
   allows us to break up our CSS files into smaller, more manageable ones.
   Cascade still applies, so the order in which they are imported matters.
   One technique is to have a base file containing all of your tag selector
   styles, and then break up the remaining rulesets into component files
   (e.g., footer styles, form styles) and media query files.

1. LEARN CSS VARIABLES. [CSS variables (AKA, custom properties)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables)
   make it possible to reuse values throughout your CSS. This is not only
   easier than remembering or looking up values each time you need to use them,
   it can make implementing sitewide changes a relatively straightforward exercise.

1. LEARN TO USE THE DEVELOPER TOOLS. The developer tools in the browser will
   show you which rules override others; will often provide the exact filename and
   line number for the rules you want to edit; and allow you to experiment with
   styles in a non-destructive way.

#### CSS Best Practices: Colors

There are 6 different ways to specify color in CSS. They are: keyword,
hexadecimal, RGB, RGBA, HSL, and HSLA. All of these formats are reduced to
RGB/A by the browser. In general, we want to use hexadecimal colors, whenever
we aren't specifying transparency using the _alpha channel_ provided in the
RGBA or HSLA formats.

```css
.article-header {
  background-color: #008000;
  /* is better than */
  background-color: green;
}
```

#### CSS Best Practices: Fonts

We don't know what fonts are installed on our users' computers, so we always
specify a generic font family as a back up (i.e., `san-serif` or `serif`). The
generic should be the last in the list of supplied `font-family` values. Note
that specific font names are quoted, but the generic is not.

```css
.site-nav {
  /* If there's no Roboto available try Arial
    If there's no Arial use the default sans-serif
    font installed on the system.
  */
  font-family: "Roboto", "Arial", sans-serif;
}
```

#### CSS Best Practices: CSS Units

We cover [CSS units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Values_and_units) in more detail in another class, but
here's a quick overview of them and some general hints about when we use them:

|  Unit   |                                                                                                Description                                                                                                 |                                                                  Usage                                                                  |
| :-----: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------: |
|   px    |                                       Referred to as absolute units because px (pixel) units will always be the same size regardless of any other related settings.                                        |                              Most frequently with font sizes, margins, padding, max- and min- properties.                               |
| em, rem |               Relative to the current element's font-size (em), or the _root_ font-size (rem). When used to set the font-size of an element, em is relative to the element's inherited size.               | Most frequently with font sizes, margins, padding, widths or heights that may need to be changed but remain relative to other elements. |
| vh, vw  | Relative to the viewport width (vw), where one unit is equal to 1/100th of the viewport's current width, or the viewport height (vh), where one unit is equal to 1/100th of the viewport's current height. |                 Most frequently with width and height of structural page elements. Commonly used in responsive design.                  |
|    %    |                                  Percentages are relative values. What the percentage is relative to, is determined by the property associated with the percentage value.                                  |                               Most often used with width. Can be helpful to approximate intrisic sizing.                                |

### Lab: Valerie's Veggie Shop

Together we are going to look at our good friend Valerie's proposal for her
website. Valerie has been so gracious to provide us with what she wants to be
included on her website. Here are the steps we'll take to build her site:

1. Review the contents and map out our HTML structure, remember to be semantic.

1. Markup our [index.html](index.html) file using semantic tags.

1. Add CSS styles to create a beautiful design using our semantic HTML. Be careful
   to follow the best practices outlined above.

## Additional Resources

Here are some sites you might want to bookmark, if you haven't already.

- [HTML5 Cheatsheet](http://htmlcheatsheet.com/)
- [CSS Cheatsheet](http://htmlcheatsheet.com/css/)
- [Semantic HTML](https://www.pluralsight.com/guides/semantic-html)
- [HTML5 Element Flowchart](http://html5doctor.com/downloads/h5d-sectioning-flowchart.pdf)
- [Introduction to HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML)
- [Introduction to CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS)

## [License](LICENSE)

1. All content is licensed under a CC­BY­NC­SA 4.0 license.
1. All software code is licensed under GNU GPLv3. For commercial use or
   alternative licensing, please contact legal@ga.co.
