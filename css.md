# CSS

### 1. Differentiate Class selector from ID selector?

### 2. Explain what elements will match each of the following CSS selectors:

```
div, p {}
div p {}
div > p {}
div + p {}

```

Answer:

* div, p - Selects all `<div>` elements and all `<p>` elements
* div p - Selects all `<p>` elements that are anywhere inside a `<div>` element
* div > p - Selects all `<p>` elements where the immediate parent is a `<div>` element
* div + p - Selects all `<p>` elements that are placed immediately after a `<div>` element

### 3. What are pseudo-elements?

Answer: any element that isn't self closing (e.g. `<input/>` `<br/>`) get two free bonus elements that are achieved by adding `::before` or `::after`. Bonus points if they mention it requires setting `content` to some value for them to appear.


### 4. What is the "Box Model" in CSS? Which CSS properties are a part of it?

Answer: 

* Width and height (or in the absence of that, default values and the content inside)
* Padding
* Border

Margin is related but not technically a part of it. 

Bonus points if you they know how to change how the box model is calculated (`box-sizing`) (`'content-box'` vs `'border-box'`)

### 5. How does z-index function?

Answer: Wnat to hear things like `position: absolute`, `position: relative`, "stacking context"

### 6. What is responsive design? How would you implement a responsive design?

Bonus points if they mention terms like "desktop first" or "mobile first". Double bonus points if they can articulate why "mobile first" is the preferred approach


### 7. Describe what a “reset” CSS file does and how it’s useful. Are you familiar with normalize.css? Do you understand how they differ?

Follow up questions:

* What's the difference between reset and normalize? 
* With relation to your own css file, where should the reset/normalize go? (before or after) -- Answer: before

### 8. What is the difference between inline, inline-block, and block?

### 9. Explain to me what's going on in this CSS selector:

```css
[role=navigation] > ul a:not([href^=mailto]) {

}
```