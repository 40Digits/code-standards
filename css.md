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

- - -

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