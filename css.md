# CSS

**Contents**

1. [Structure](#structure)
2. [Selectors](#selectors)
3. [Properties](#properties)
	1. [Property Ordering](#property-ordering)
	2. [Vendor Prefixes](#vendor-prefixes)
4. [Values](#values)
5. [Media Queries](#media-queries)
6. [Commenting](#commenting)
7. [Best Practices](#best-practices)


## Structure

There are plenty of different methods for structuring a stylesheet. With the CSS in core, it is important to retain a high degree of legibility. This enables subsequent contributors to have a clear understanding of the flow of the document.

- Use tabs, not spaces, to indent each property.

- Add two blank lines between sections and one blank line between blocks in a section.

- Each selector should be on its own line, ending in either a comma or an opening curly brace. Property-value pairs should be on their own line, with one tab of indentation and an ending semicolon. The closing brace should be flush left, using the same level of indentation as the opening selector.

**Correct:**

```css
#selector-1,
#selector-2,
#selector-3 {
	background: #fff;
	color: #000;
}
```

**Incorrect:**

```css
#selector-1, #selector-2, #selector-3 {
	background: #fff;
	color: #000;
	}

#selector-1 { background: #fff; color: #000; }
```


## Selectors

With specificity, comes great responsibility. Broad selectors allow us to be efficient, yet can have adverse consequences if not tested. Location-specific selectors can save us time, but will quickly lead to a cluttered stylesheet. Exercise your best judgement to create selectors that find the right balance between contributing to the overall style and layout of the DOM.

- Similar to the [WordPress Coding Standards](http://codex.wordpress.org/WordPress_Coding_Standards) for file names, use lowercase and separate words with hyphens when naming selectors. Avoid camelcase and underscores.

- Use human readable selectors that describe what element(s) they style.

- Attribute selectors should use double quotes around values

- Refrain from using over-qualified selectors, div.container can simply be stated as .container

**Correct:**

```css
#comment-form {
    margin: 1em 0;
}

input[type="text"] {
    line-height: 1.1;
}
```

**Incorrect:**

```css
#commentForm { /* Avoid camelcase. */
    margin: 0;
}

#comment_form { /* Avoid underscores. */
    margin: 0;
}

div#comment_form { /* Avoid over-qualification. */
    margin: 0;
}

#c1-xr { /* What is a c1-xr?! Use a better name. */
    margin: 0;
}

input[type=text] { /* Should be [type="text"] */
    line-height: 110% /* Also doubly incorrect */
}
```


## Properties

Similar to selectors, properties that are too specific will hinder the flexibility of the design. Less is more. Make sure you are not repeating styling or introducing fixed dimensions (when a fluid solution is more acceptable).

- Properties should be followed by a colon and a space.

- All properties and values should be lowercase, except for font names and vendor-specific properties.

- Use hex code for colors, or `rgba()` if opacity is needed. Avoid RGB format and uppercase, and shorten values when possible: `#fff` instead of `#FFFFFF`.

- Use shorthand (except when overriding styles) for background, border, font, list-style, margin, and padding values as much as possible. (For a shorthand reference, see [CSS Shorthand](http://codex.wordpress.org/CSS_Shorthand).)

### Property Ordering

Above all else, choose something that is meaningful to you and semantic in some way. Random ordering is chaos, not poetry. In WordPress Core, our choice is logical or grouped ordering, wherein properties are grouped by meaning and ordered specifically within those groups. The properties within groups are also strategically ordered to create transitions between sections, such as background directly before color. The baseline for ordering is:

- Display
- Positioning
- Box Model
- Colors and Typography
- Other

Things that are not yet used in core itself, such as CSS3 animations, may not have a prescribed place above but likely would fit into one of the above in a logical manner. Just as CSS is evolving, so our standards will evolve with it.

Top/Right/Bottom/Left (TRBL/trouble) should be the order for any relevant properties (e.g. `margin`), much as the order goes in values. Corner specifiers (e.g. `border-radius: * * * *`) should be `top-left, top-right, bottom-right, bottom-left`. This is derived from how shorthand values would be ordered.

Another method that is often used, including by the Automattic/WordPress.com Themes Team, is to order properties alphabetically, with or without certain exceptions.

**Example:**

```css
#overlay {
    position: absolute;
    z-index: 1;
    padding: 10px;
    background: #fff;
    color: #777;
}
```

### Vendor Prefixes

Vendor prefixes should go longest (`-webkit-`) to shortest (unprefixed). Values should be right aligned with spaces after the colon provided that all the values are the same across all prefixes.

**Preferred method**

```css
.koop-shiny {
    -webkit-box-shadow: inset 0 0 1px 1px #eee;
    -moz-box-shadow:    inset 0 0 1px 1px #eee;
    box-shadow:         inset 0 0 1px 1px #eee;
    -webkit-transition: border-color 0.1s;
    -moz-transition:    border-color 0.1s;
    -ms-transition:     border-color 0.1s;
    -o-transition:      border-color 0.1s;
    transition:         border-color 0.1s;
}
```

**Not preferred:**

```css
.okay {
    -webkit-box-shadow: inset 0 0 1px 1px #eee;
       -moz-box-shadow: inset 0 0 1px 1px #eee;
            box-shadow: inset 0 0 1px 1px #eee;
}
```

**Bad:**

```css
.bad {
    -webkit-box-shadow: inset 0 0 1px 1px #eee;
    -moz-box-shadow: inset 0 0 1px 1px #eee;
    box-shadow: inset 0 0 1px 1px #eee;
}
```

**Special case for CSS gradients:**

```css
.gradient {
    background: #fff;
    background-image: -webkit-gradient(linear, left bottom, left top, from(#fff), to(#000));
    background-image: -webkit-linear-gradient(bottom, #fff, #000);
    background-image: -moz-linear-gradient(bottom, #fff, #000);
    background-image: -o-linear-gradient(bottom, #fff, #000);
    background-image: linear-gradient(to top, #fff, #000);
}
```


## Values

There are numerous ways to input values for properties. Follow the guidelines below to help us retain a high degree of consistency.

- Space before the value, after the colon

- Do not pad parentheses with spaces

- **Always** end in a semicolon

- Use double quotes rather than single quotes, and only when needed, such as when a font name has a space.

- 0 values should not have units unless necessary, such as with transition-duration.

- Line height should also be unit-less, unless necessary to be defined as a specific pixel value. This is more than just a style convention, but is worth mentioning here. More information: http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/

- Use a leading zero for decimal values, including in `rgba()`.

- Multiple comma-separated values for one property should be separated by either a space or a newline, including within `rgba()`. Newlines should be used for lengthier multi-part values such as those for shorthand properties like box-shadow and text-shadow. Each subsequent value after the first should then be on a new line, indented to the same level as the selector and then spaced over to left-align with the previous value.

**Correct:**

```css
/* Correct usage of quotes */
.class {
    background-image: url(images/bg.png);
    font-family: "Helvetica Neue", sans-serif;
}

/* Correct usage of zero values */
.class {
    font-family: Georgia, serif;
    text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.5), 0 1px 0 #fff;
}
```

**Incorrect:**

```css
/* Avoid missing space and semicolon */
.class {
    background:#fff
}

/* Avoid adding a unit on a zero value */
.class {
    margin: 0px 0px 20px 0px;
}
```


## Media Queries

Media queries allow us to gracefully degrade the DOM for different screen sizes. If you are adding any, be sure to test above and below the break-point you are targeting.

- It is generally advisable to keep media queries grouped by media at the bottom of the stylesheet.

	- An exception is made for the wp-admin.css file in core, as it is very large and each section essentially represents a stylesheet of its own. Media queries are therefore added at the bottom of sections as applicable.

- Rule sets for media queries should be indented one level in.

- The example below uses pixels, but we focus on em-based media queries for [many](http://blog.cloudfour.com/the-ems-have-it-proportional-media-queries-ftw/) [reasons](http://css-tricks.com/why-ems/).

**Example:**

```css
@media all and (max-width: 699px) and (min-width: 520px) {

	/* Selectors */

}
```


## Commenting

- Comment, and comment liberally. If there are concerns about file size, utilize minified files and the SCRIPT_DEBUG constant. Long comments should manually break the line length at 80 characters.

- A table of contents should be utilized for longer stylesheets, especially those that are highly sectioned. Using an index number (1.0, 1.1, 2.0, etc.) aids in searching and jumping to a location.

- Comments should be formatted much as PHPDoc is. The [CSSDoc](http://cssdoc.net/) standard is not necessarily widely accepted or used but some aspects of it may be adopted over time. Section/subsection headers should have newlines before and after. Inline comments should not have empty newlines separating the comment from the item to which it relates.

**For sections and subsections:**

```css
/**
* #.# Section title
*
* Description of section, whether or not it has media queries, etc.
*/

.selector {
    float: left;
}
```

**For inline:**

```css
/* This is a comment about this selector */

.another-selector {
    position: absolute;
    top: 0 !important; /* I should explain why this is so !important */
}
```


## Best Practices

- Stylesheets tend to get long in length. Focus slowly gets lost whilst intended goals start repeating and overlapping. Writing smart code from the outset helps us retain the overview whilst remaining flexible throughout change.

- If you are attempting to fix an issue, attempt to remove code before adding more.

- Magic Numbers are unlucky. These are numbers that are used as quick fixes on a one-off basis.

**Example:**

```css
.box {
	margin-top: 37px
}
```

- DOM will change over time, target the element you want to use as opposed to “finding it” through its parents. Example: Use `.highlight` on the element as opposed to `.highlight a` (where the selector is on the parent)

- Know when to use the height property. It should be used when you are including outside elements (such as images). Otherwise use line-height for more flexibility.

- Do not restate default property & value combinations (for instance `display: block;` on block-level elements).
