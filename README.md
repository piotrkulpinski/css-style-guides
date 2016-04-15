CSS Style Guides (Work in progress)
==================

<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Golden Rule](#golden-rule)
- [Scaffolding](#scaffolding)
	- [Box-sizing](#box-sizing)
	- [Normalize](#normalize)
- [Syntax](#syntax)
- [Organization](#organization)
- [Naming conventions](#naming-conventions)
	- [Module naming](#module-naming)
	- [State rules](#state-rules)
	- [Consistency](#consistency)
- [Declaration order](#declaration-order)
- [Vendor prefixes](#vendor-prefixes)
- [Shorthand notation](#shorthand-notation)
- [Comments](#comments)
- [Sass](#sass)
	- [Variables](#variables)
	- [Mixins](#mixins)
	- [Z-index](#z-index)
	- [Extends](#extends)
	- [Declaration order](#declaration-order)
	- [Operators](#operators)
	- [Nesting](#nesting)
		- [Elements](#elements)
		- [BEM nesting with `&`](#bem-nesting-with-)
		- [Un-nesting with *'parent selector'* `&`](#un-nesting-with-parent-selector-)
		- [Nesting pseudo-classes and pseudo-elements with `&`](#nesting-pseudo-classes-and-pseudo-elements-with-)
	- [Comments](#comments)
- [Editor preferences](#editor-preferences)

<!-- /TOC -->

## Golden Rule

Conform these guidelines at all times. Every line of code should appear to be written by a single person, no matter the number of contributors.

## Scaffolding

Scaffolding refers to the global resets and dependencies.

### Box-sizing

We reset `box-sizing` to `border-box` for every element. This allows us to more easily assign widths to elements that also have `padding` and `border`s.

### Normalize

We use custom-build normalize file for improved cross-browser rendering. It helps to correct small inconsistencies across browsers and devices.

## Syntax

- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it so keep it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Always include single space after commas within `rgb()`, `rgba()`, `hsl()`, `hsla()` and `rect()` values.
- Always prefix property values or color parameters with a leading zero (e.g., `0.5` instead of `.5` and `-0.5px` instead of `-.5px`).
- Lowercase all hex values, e.g., `#bada55`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Always use long hex values, e.g., `#ffffff` instead of `#fff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`.
- Use single or double quotes consistently. Preference is for double quotes, e.g., content: `""`.
- Avoid specifying units for zero values, e.g., `margin: 0` instead of `margin: 0px`.
- Use single colon for **[pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)** and double colon for **[pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)**, e.g., `.btn:hover {}` and `.btn::before {}`.

**Bad**

```css
.selector, .selector_secondary, .selector[type=text] {
  margin:15px;
  padding:0px 0px 15px;
  background-color:rgba(0,0,0,.5);
  box-shadow:0px 1px 2px #CCC,inset 0px 1px 0px #FFF
}
```

**Good**

```css
.selector,
.selector_secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0, 0, 0, 0.5);
  box-shadow: 0 1px 2px #cccccc, inset 0 1px 0 #ffffff;
}
```

## Organization

- Organize sections of code by component.
- Use consistent white space to your advantage when separating sections of code for scanning larger documents.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.

## Naming conventions

### Module naming

Naming conventions in CSS are very useful in making your code more strict, more transparent, and more informative.

A good naming convention will tell you and your contributors

- what type of thing a class does;
- where a class can be used;
- what (else) a class might be related to.

We use **BEM** methodology for naming CSS modules.

BEM splits modules classes into three groups:

- Block: The sole root of the module.
- Element: A module part of the Block.
- Modifier: A variant or extension of the Block.

Elements are delimited with two (2) underscores (`__`), and Modifiers are delimited by one (1) underscore (`_`).

```css
.article {}
.article__title {}
.article_featured {}
```

Two-part Block/Element/Modifier names are delimited by one (1) hyphen (`-`).

```css
.image-card {}
.image-card_modifier-name {}
```

For more information about BEM naming conventions check out it's [documentation](https://en.bem.info/method/naming-convention/).

### State rules

Use the `is-` prefix for state rules that are shared between CSS and JS (`.is-active`, `.is-visible`, etc.).

### Consistency

Keep consistent class names throughout every project. That means if you name a header class in one project `.page-head`, use the same name in every other project instead of `.header`, `.head`, etc.

**Bad**

```scss
/* Project 1 */
.page-head {}

/* Project 2 */
.header {}
```

**Good**

```scss
/* Project 1 */
.page-head {}

/* Project 2 */
.page-head {}
```

## Declaration order

Related property declarations should be grouped together following the order:

1. Positioning
2. Box model
3. Typographic
4. Visual

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, hence they come last.

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```

## Vendor prefixes

Don't use vendor prefixes in your code. You should always have [autoprefixer](https://github.com/postcss/autoprefixer) enabled in the project, which takes care of prefixes for the standard CSS3 properties. It uses [Can I Use](http://caniuse.com/) database.

However, please note that some popular properties (like `-webkit-appearance` or `-webkit-font-smoothing` are not a part of standard and need to be written with prefixes by you).

## Shorthand notation

Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values. Common overused shorthand properties include:

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Often times we don't need to set all the values a shorthand property represents. Excessive use of shorthand properties often leads to sloppier code with unnecessary overrides and unintended side effects.

## Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name.

If you're forced to use any hack within your code, put an explanation or source somewhere near as a comment.

## Sass

### Variables

grouped

### Mixins

reusable

### Z-index

`z-index` values should be stored in a well-defined variable groups at any time. No `z-index` value should be written in number notation. Take some time to think about project layers and define clear value groups.

**Bad**

```scss
.header {
  z-index: 1;
}

.footer {
  z-index: 9999;
}
```

**Good**

```scss
$zindex-header: 5;
$zindex-footer: 10;

.header {
  z-index: $zindex-header;
}

.footer {
  z-index: $zindex-footer;
}
```

Keep `z-index` values divisible by `5` and equally spaced (`5`, `10`, `15`). This will allow you to easily add sub-layer positions using Sass operators.

```scss
$zindex-header: 5;

.header {
  z-index: $zindex-header;
}

.header__title {
  z-index: ($zindex-header + 1);
}
```

### Extends

Avoid using Sass `@extend` functionality unless it's absolute necessary. It's always better to create module modifier which will extend main module styles.

**Bad**

```scss
.status {
  background-color: #EEE;
}

.status_error {
  @extend .status;
  color: #F00;
}
```

```html
<div class="status_error">Error</div>
```

**Good**

```scss
.status {
  background-color: #eeeeee;
}

.status_error {
  color: #ff0000;
}
```

```html
<div class="status status_error">Error</div>
```

### Declaration order

Rule sets should be ordered as follows: `@extend` declarations (if necessary), `@include` declarations without inner `@content`, properties, `@include` declarations with inner `@content`, then nested rule sets.

**Bad**

```scss
.error {
  img {
    ...
  }

  background-color: #f00;
  @extend %status;
  @include status();
}
```

**Good**

```scss
.error {
  @extend %status;
  @include status();
  background-color: #f00;

  img {
    ...
  }
}
```

### Operators

For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.

**Bad**

```scss
.selector {
  margin-bottom: $variable*2;
}
```

**Good**

```scss
.selector {
  margin-bottom: ($variable * 2);
}
```

### Nesting

Avoid unnecessary nesting. Just because you can nest, doesn't mean you always should. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.

#### Elements

I find this to be the most common form of nesting and is probably just fine for most sites. It’s not necessarily bad, but nesting like this makes your CSS more specific. It also doesn’t force you to write reusable components, which is what you want for building most websites.

```css
.selector {
  h1 {}
  span {}
  a {}
}
```

Consider rewriting that code to something like:

```css
.selector-heading {}
.selector-subheading {}
.selector-permalink {}
```

Those classes have lower specificity, more meaningful selectors, and are component-based.

#### BEM nesting with `&`

Nesting for BEM is helpful at first, but comes as a cost. While it can save you a few bytes it makes the code less readable (especially with longer Blocks) and it's hard to find Elements or Modifiers by their class names.

```css
.block {
  &__element {}
  &_modifier {}
}
```

Instead, keep it simple and just write it all out:

```css
.block {}
.block__element {}
.block_modifier {}
```

Easy to read, easy to search, and with no sacrifice to your compiled CSS.

#### Un-nesting with *'parent selector'* `&`

The un-nesting example is perhaps the most confusing way to nest CSS.

```css
.child {
  .parent & {}
}
```

When used at the end of a nested selector, the `&` puts everything to the left of it before the parent selector. So the above example compiles to `.parent .child {}`. This is confusing in a few ways:

- The `&` puts that selector at the beginning of the top-most parent.
- It’s the opposite of how regular nesting works.
- It clouds your vision of the compiled CSS.

Rather than go that route, try something like this:

```css
.child {}
.child_modifier {}
```

The result is a component-based approach with lower specificity and clearer insight into what your compiled CSS will be.

#### Nesting pseudo-classes and pseudo-elements with `&`

Nesting with pseudo-* feels like the only practical way to nest your CSS.

```css
.btn {
  &:hover,
  &:focus,
  &:active {}

  &::before {}
}
```

What makes it different from the previous example is that this is all one element and class, just with different states. It’s not multiple half-classes that do different things.

### Comments

Begin each Sass file with block comment containing group name and name of the file/module:

```css
/*
** Module - Heading
** -----------------------------------------------------------------------------*/
```

Block comments should be started with one of those 5 prefixes:

- Common
- Module
- Utility
- Setup
- Vendor

## Editor preferences

Set your editor to the following settings to avoid common code inconsistencies and dirty diffs:

- Use soft-tabs set to two spaces.
- Trim trailing white space on save.
- Set encoding to UTF-8.
- Add new line at end of files.

Each project should have .editorconfig file in the main directory set to meet guidelines described above. Learn more about [EditorConfig](http://editorconfig.org/).

```
[*]
charset = utf-8
indent_style = space
indent_size = 2
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
```


**Bad**

```scss
```

**Good**

```scss
```
