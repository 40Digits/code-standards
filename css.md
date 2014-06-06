# CSS Code Standards

**Contents**

1. Structure
2. Selectors
3. Properties
	1. Property Ordering
	2. Vendor Prefixes
4. Values
5. Media Queries
6. Commenting
7. Best Practices


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