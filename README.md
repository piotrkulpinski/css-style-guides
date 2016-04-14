CSS Style Guides
==================

## Table of contents

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
- Avoid specifying units for zero values, e.g., `margin: 0` instead of `margin: 0px`.

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

## Sass

### Z-index

### Variables

grouped

### Mixins

reusable

### Declaration order

Rule sets should be ordered as follows: `@extend` declarations, `@include` declarations without inner `@content`, properties, `@include` declarations with inner `@content`, then nested rule sets.

**Bad**

```scss
.fatal-error {
  img {
    ...
  }

  background-color: #f00;
  @extend %error;
  @include status-box();
}
```

**Good**

```scss
.fatal-error {
  @extend %error;
  @include status-box();
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