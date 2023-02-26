# CSS Notes

## Selectors

Selectors simply refer to the HTML elements to which CSS rules apply; 

### Universal Selector 

The universal selector will select elements of any type, hence the name “universal”, and the syntax for it is a simple asterisk. In the example below, every element would have the color: purple; style applied to it.

```
* {
  color: purple;
}
```
 
### Type Selectors

A type selector (or element selector) will select all elements of the given element type, and the syntax is just the name of the element:

```
 <!-- index.html -->

<div>Hello, World!</div>
<div>Hello again!</div>
<p>Hi...</p>
<div>Okay, bye.</div>
```

```
/* styles.css */

div {
  color: white;
}
```

Here, all three `<div>` elements would be selected, while the `<p>` element wouldn’t be.

### Class Selectors

Class selectors will select all elements with the given class, which is just an attribute you place on an HTML element. Here’s how you add a class to an HTML tag and select it in CSS:

```
<!-- index.html -->

<div class="alert-text">
  Please agree to our terms of service.
</div>
```

```
/* styles.css */

.alert-text {
  color: red;
}
```

Note the syntax for class selectors: a period immediately followed by the case-sensitive value of the class attribute. Classes aren’t required to be unique, so you can use the same class on as many elements as you want.

Another thing you can do with the class attribute is to add multiple classes to a single element as a space-separated list, such as class="alert-text severe-alert". Since whitespace is used to separate class names like this, you should never use spaces for multi-worded names and should use a hyphen instead. 

### ID Selectors

ID selectors are similar to class selectors. They select an element with the given ID, which is another attribute you place on an HTML element:

```
<!-- index.html -->

<div id="title">My Awesome 90's Page</div>
```

```
/* styles.css */

#title {
  background-color: red;
}
```

While there are cases where using an ID makes sense or is needed, such as taking advantage of specificity or having links redirect to a section on the current page, you should use IDs sparingly (if at all). 

The major difference between classes and IDs is that an element can only have one ID. An ID cannot be repeated on a single page, and the ID attribute should not contain any whitespace at all. 

### Grouping Selector

What if we have two groups of elements that share some of their style declarations? 

```
.read {
  color: white;
  background-color: black;
  /* several unique declarations */
}

.unread {
  color: white;
  background-color: black;
  /* several unique declarations */
}
```

Both our .read and .unread selectors share the color: white; and background-color: black; declarations, but otherwise have several of their own unique declarations. To cut down on the repetition, we can group these two selectors together as a comma-separated list:

```
.read,
.unread {
  color: white;
  background-color: black;
}

.read {
  /* several unique declarations */
}

.unread {
  /* several unique declarations */
}
```

### Chaining Selectors

Another way to use selectors is to chain them as a list without any separation. Let’s say we had the following HTML:

```
<div>
  <div class="subsection header">Latest Posts</div>
  <p class="subsection preview">This is where a preview for a post might go.</p>
</div>
```

We have two elements with the subsection class that have some sort of unique styles, but what if we only want to apply a separate rule to the element that also has header as a second class? Well, we could chain both the class selectors together in our CSS like so:

```
.subsection.header {
  color: red;
}
```

What .subsection.header does is it selects any element that has both the subsection and header classes. Notice how there isn’t any space between the .subsection and .header class selectors. This syntax basically works for chaining any combination of selectors, except for chaining more than one type selector. 

This can also be used to chain a class and an ID, as shown below:

```
<div>
  <div class="subsection header">Latest Posts</div>
  <p class="subsection" id="preview">This is where a preview for a post might go.</p>
</div>
```

You can take the two elements above and combine them with the following:

```
.subsection.header {
  color: red;
}

.subsection#preview {
  color: blue;
}
```

In general, you can’t chain more than one type selector since an element can’t be two different types at once. For example, chaining two type selectors like div and p would give us the selector divp, which wouldn’t work since the selector would try to find a literal `<divp>` element, which doesn’t exist. 

### Descendant Combinator

Combinators allow us to combine multiple selectors differently than either grouping or chaining them, as they show a relationship between the selectors.  

So something like .ancestor .child would select an element with the class child if it has an ancestor with the class ancestor. Another way to think of it is child will only be selected if it is nested inside of ancestor, no matter how deep. Take a quick look at the example below and see if you can tell which elements would be selected based on the CSS rule provided:

```
<!-- index.html -->

<div class="ancestor"> <!-- A -->
  <div class="contents"> <!-- B -->
    <div class="contents"> <!-- C -->
    </div>
  </div>
</div>

<div class="contents"></div> <!-- D -->
```

```
/* styles.css */

.ancestor .contents {
  /* some declarations */
}
```

In the above example, the first two elements with the contents class (B and C) would be selected, but that last element (D) won’t be.

## Common CSS Properties

### Color and Background-Color

The color property sets an element’s text color, while background-color sets, well, the background color of an element. I guess we’re done here?  

Almost. Both of these properties can accept one of several kinds of values. A common one is a keyword, such as an actual color name like red or the transparent keyword. They also accept HEX, RGB, and HSL values, which you may be familiar with if you’ve ever used a photoshop program or a site where you could customize your profile colors.

```
p {
  /* hex example: */
  color: #1100ff;
  /* rgb example: */
  color: rgb(100, 0, 127);
  /* hsl example: */
  color: hsl(15, 82%, 56%);
}
```

### Typography Basics and Text-Align

`font-family` can be a single value or a comma-separated list of values that determine what font an element uses. Each font will fall into one of two categories, either a “font family name” like "DejaVu Sans" (we use quotes due to the whitespace between words) or a “generic family name” like sans-serif (generic family names never use quotes).  

If a browser cannot find or does not support the first font in a list, it will use the next one, then the next one and so on until it finds a supported and valid font. This is why it’s best practice to include a list of values for this property, starting with the font you want to be used most and ending with a generic font family as a fallback, e.g. font-family: "DejaVu Sans", sans-serif;  

`font-size` will, as the property name suggests, set the size of the font. When giving a value to this property, the value should not contain any whitespace, e.g. font-size: 22px has no space between “22” and “px”.  

`font-weight` affects the boldness of text, assuming the font supports the specified weight. This value can be a keyword, e.g. font-weight: bold, or a number between 1 and 1000, e.g. font-weight: 700 (the equivalent of bold). Usually, the numeric values will be in increments of 100 up to 900, though this will depend on the font.  

`text-align` will align text horizontally within an element, and you can use the common keywords you may have come across in word processors as the value for this property, e.g. text-align: center.  

### Image Height and Width

Images aren’t the only elements that we can adjust the height and width on, but we want to focus on them specifically in this case.  

By default, an `<img>` element’s height and width values will be the same as the actual image file’s height and width. If you wanted to adjust the size of the image without causing it to lose its proportions, you would use a value of “auto” for the height property and adjust the width value:

```
img {
  height: auto;
  width: 500px;
}
```

It’s best to include both of these properties for `<img>` elements, even if you don’t plan on adjusting the values from the image file’s original ones. When these values aren’t included, if an image takes longer to load than the rest of the page contents, the image won’t take up any space on the page at first, but will suddenly cause a drastic shift of the other page contents once it does load in. Explicitly stating a height and width prevents this from happening, as space will be “reserved” on the page and will just appear as a blank space until the image loads.

## The Box Model

Every single thing on a webpage is a rectangular box. These boxes can have other boxes in them and can sit alongside one another.  

In the end, laying out a webpage and positioning all its elements is deciding how you are going to nest and stack these boxes.  

The only real complication here is that there are many ways to manipulate the size of these boxes, and the space between them, using padding, margin, and border. The assigned articles go into more depth on this concept, but to sum it up briefly:

- `padding` increases the space between the border of a box and the content of the box.
- `margin` increases the space between the borders of a box and the borders of adjacent boxes.
- `border` adds space (even if it’s only a pixel or two) between the margin and the padding.

