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