# CSS

**Contents**

- [Structure](#structure)
- [Selectors](#selectors)
+ [Properties](#properties)
	- [Property Ordering](#property-ordering)
	- [Vendor Prefixes](#vendor-prefixes)
- [Values](#values)
- [Media Queries](#media-queries)
- [Commenting](#commenting)
- [Best Practices](#best-practices)

---
#Terminology
###Rule declaration

Name given to a selector with an accompanying group of properties.

```css
.rule {
  display: block;
  background-color: #000;
}
```

###Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, class, ID, or attributes.

```css
.element-class {
  /* */
}
[type="text"] {
  /* */
}
```

Further Reading:

- [Mozilla Developer Network: Attribute Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)
- [CSS-Tricks: Attributes](https://css-tricks.com/almanac/selectors/a/attribute/)
- [Jenkov: Attributes](http://tutorials.jenkov.com/css/selectors.html#attribute-selector)

###Properties

Properties give the selected elements of a rule declaration their styles.

```css
.some-selector {
  display: block;
  color: #000;
}
```
----------
#Syntax & Formatting

Having a standard way of writing CSS means that code will always look and feel familiar to all members of the team. Code guidelines promote consistency, ensure a better environment to work in, and help with reading and updating of code.

- SASS or SCSS
- Two (2) space indents, no tabs.
- Use dashes over camelCasing & under_scores in class names.
- Do not use ID selectors.
- Properly written multi-line CSS rules.
- One selector per line, one rule per line.
- Include a single space before the opening brace of a ruleset.
- Include a space after each comma in comma-separated property or function values.
- Include a semi-colon at the end of the last declaration in a declaration block.
- The closing brace should be on its own line.
- Use lowercase and shorthand hex values.
- A new line after the closing brace.
- Separate each ruleset by a blank line.
- Avoid writing vendor prefixed CSS.

(Disclaimer: some of the syntax guidelines will not apply to Sass syntax.)

```css
// Correct
.foo,
.bar {
  display: block;
  background-color: #fff;
  color: #000;
}

// Incorrect
.foo, .bar {
    display:block; background-color: #fff;
  color: #000 }
```

###ID Selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessary high level of specificity to your rule declarations. Most importantly, they are not re-usable.

###Quotes

Neither CSS nor Sass require strings to be quoted, but because the vast majority of other languages do require strings to be quoted, and for the sake of consistency, we believe strings should be quoted in all situations other than the few detailed below. Besides consistency, there are several other reasons for this choice:

- color names are treated as colors when unquoted
- most syntax highlighters will choke on unquoted strings
- helps with general readability

URLs:
```css
// Correct
.foo {
  background-image: url('/assets/images/image.jpg');
}

// Incorrect
.bar {
  background-image: url(/assets/images/image.jpg);
}
```

Take note: some CSS values (such as `font-family`) [should not be quoted](http://www.sitepoint.com/sass-reference/string/). These declarations (e.g.: `font-family: ‘sans-serif’`) will fail silently due to the Sass compiler expecting an identifier, not a quoted string.

```sass
// Correct
$font-type: sans-serif;
$font-type: 'Helvetica', Arial, sans-serif;

// Incorrect
$font-type: 'sans-serif';
```

###Numbers
- Never display trailing zeros.
- A 0 value should never have a unit.
- Always add a 0 before a decimal.

```css
// Correct
.foo {
  padding: 20px;
  margin: 0;
  opacity: 0.5;
}

// Incorrect
.bar {
  padding: 20.0px;
  margin: 0px;
  opacity: .5;
}
```

###Lists

Lists are the Sass equivalent of arrays. A list is a flat data structure (not to be confused with maps) intended to store values or any type.

- multiline
- always comma separated (even last item)
- always wrapped in parenthesis

(Disclaimer: while single line is correct, for legibility purposes, we are sticking with multiline. )

```sass
// Correct
$list: (
  value-one,
  value-two,
  value-three,
)
$colors: (
  red $red,
  purple $purple,
  green $green,
)

// Incorrect
$list: (value-one, value-two, value-three);
$list: value-one, value-two, value-three;
$list: 'value-one', 'value-two', 'value-three';
```

Further Reading:

- [Understanding Sass lists](http://hugogiraudel.com/2013/07/15/understanding-sass-lists/)
- [Sass maps vs nested lists](http://www.sitepoint.com/sass-maps-vs-nested-lists/)
- [Working with lists & @each loops](https://benfrain.com/working-with-lists-and-each-loops-in-sass-with-the-index-and-nth-function/)

###Maps

The Sass term for associative arrays, hashes or even JavaScript objects. A map is a data structure mapping keys.

- spaces after the colon `:`
- opening braces `(` on the same line as the colon `:`
- quoted keys if they are strings
- comma `,` at the end of each key/value
- closing brace `)` on its own new line

```sass
// Correct
$colors: (
  blue: $blue,
  gray: $gray
);
$colors: (
  blue: (
    light: #09679e,
    dark: #06486e
  ),
  orange: (
    light: #ff5316,
    dark: #e45122
  )
);

// Incorrect
$colors: (blue: $blue, gray: $gray);
```

Further Reading:

- [Using Sass Maps](http://www.sitepoint.com/using-sass-maps/)
- [Debugging Sass Maps](http://www.sitepoint.com/debugging-sass-maps/)
- [Extra Map functions in Sass](http://www.sitepoint.com/extra-map-functions-sass/)
- [Sass Maps are Awesome](https://viget.com/extend/sass-maps-are-awesome)
- [Introduction to Sass Maps & Example Usage](http://webdesign.tutsplus.com/tutorials/an-introduction-to-sass-maps-usage-and-examples--cms-22184)

###Rule Ordering
- @extend
- @include
- Regular style properties
- Nested Pseudo Classes & Pseudo Elements
- Nested Selectors

```sass
.foo {
  $scoped-variable: 'bar';
  @extend %module;
  @include type(12, 14);
  background: #000;
  &.nested-class {
    color: #fff;
  }
  &:before {
    content: "";
    @include symbols(cross);
  }
  &:hover {
    background: blue;
  }
  span {
    display: none;
  }
}
```
###State Rules

A state is something that augments and overrides all other styles. For example, an accordion section may be in a collapsed or expanded state. To indicate the sate, we may add a class indicating the state.

States are generally applied to the same element as a layout rule or to the same element as a base module class.

```html
<dl>
  <dt>
    Lorem ipsum dolor sit amet
  </dt>
  <dd class="is-open">
    Ut rhoncus tempus dolor. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  </dd>
</dl>
```

Some possible states:

- is-active
- is-hidden
- is-closed
- is-enabled
- is-open

###JavaScript Hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript specific classes to bind to, prefixed with `js-`

```html
<button type="button" class="button nav-trigger js-nav-trigger">Menu</button>
```

#Nesting Selectors

We recommend nesting selectors no more than three levels deep. However, if naming conventions are followed, you shouldn’t need to be going more than 2 deep.

```sass
.page {
  .content {
    .element {
      // STOP
    }
  }
}
```

When selectors become this long, you’re likely writing CSS that is:

- strongly coupled to the HTML
- overly specific
- not reusable

#CSS Selectors
- Avoid using ID’s for style.
- Use meaningful names: `$visual-grid-color` not `$color` or `$vslgrd-clr`.
- Avoid using the direct descendant selector `>`.
- Avoid nesting more than 3 selectors deep.
- Avoid using HTML tags in class names: `.news` not `.news-section`
- Avoid using HTML tags on classes for generic markup: `div.widgets`
- Avoid nesting within a media query.

###Reusability

With a move toward a more component-based approach to constructing UIs, the idea of reusability is paramount. We want the option to be able to move, recycle, duplicate, and syndicate components across our projects.

To this end, we make heavy use of classes. IDs, as well as being hugely over-specific, cannot be used more than once on any given page, whereas classes can be reused an infinite amount of times. Everything you choose, from the type of selector to its name, should lend itself toward being reused.

[(source)](http://cssguidelin.es/#reusability)

###Location Independence

Given the ever-changing nature of most UI projects, and the move to more component-based architectures, it is in our interests not to style things based on where they are, but on what they are. That is to say, our components’ styling should not be reliant upon where we place them—they should remain entirely location independent.

A component shouldn’t have to live in a certain place to look a certain way.

[(source)](http://cssguidelin.es/#location-independence)

###Portability

Reducing, or, ideally, removing, location dependence means that we can move components around our markup more freely, but how about improving our ability to move classes around components? On a much lower level, there are changes we can make to our selectors that make the selectors themselves—as opposed to the components they create—more portable. Take the following example:

```css
input.btn {}
```

This is a qualified selector; the leading input ties this ruleset to only being able to work on <input> elements. By omitting this qualification, we allow ourselves to reuse the .btn class on any element we choose, like an <a>, for example, or a <button>.

Qualified selectors do not lend themselves well to being reused, and every selector we write should be authored with reuse in mind.

Of course, there are times when you may want to legitimately qualify a selector—you might need to apply some very specific styling to a particular element when it carries a certain class.

[(source)](http://cssguidelin.es/#portability)

###Performance

Generally speaking, the longer a selector is, the slower it is, for example:

```css
body.home div.header ul {}
```
… is a far less efficient selector than:

```css
.global-nav {}
```

Browsers read CSS selectors right-to-left. A browser will read the first selector as:

* find all `<ul>` elements in the DOM
* check if they live inside an element with a class of `.header`
* check that `.header` class exists on a `<div>` element
* check that it lives anywhere insde any elements with a class of `.home`
* finally, check that `.home` exists on a `<body>` element

Where as the second selector: find all elements with a class of `.global-nav`

To further compound the problem, we are using descendant selectors (e.g. `.foo .bar {}`). The upshot of this is that a browser is required to start with the rightmost part of the selector (i.e. `.bar`) and keep looking up the DOM indefinitely until it finds the next part (i.e. `.foo`). This could mean stepping up the DOM dozens of times until a match is found.

This is just one reason why nesting with preprocessors is often a false economy; as well as making selectors unnecessarily more specific, and creating location dependency, it also creates more work for the browser.


#Comments

Use comments to separate logical groups of styles within a document.

- Prefer line comments `//` over `/* */` as line comments are ignored with compilers.
- Prefer comments on their own line. Avoid end-of-line comments.
- Write detailed comments for code that isn’t self-documenting:
  - Compatibility, browser-specific fixes, or fallback
  - Purpose of selector or rule set
  - Experimental properties
- Divide up sections with comment headers.


```sass
// ================================
// Style Sheet Name
// ================================

// --------------------------------
// Section Comment Header
// --------------------------------

// Single Line Comments
```


----------
#Advanced Sass
###Mixins

Mixins allow us to create re-usable parts of CSS without having to write repetitive code. However, far too often, mixins are written in a way that bloat the size of our file through duplication. A mixin therefore should only be used if an argument is present to modify the style.

```sass
// Correct
@mixin rgba($color, $alpha) {
  background-color: rgba($color, $alpha);
}

// Incorrect
@mixin button {
  display: inline-block;
  padding: 10px;
  font-size: 15px
}
```

Some examples where are `mixin()` usage is most fitting:

- Media Queries
- Keyframe animations
- Sprites & symbols
- Font & line-height properties

Further reading:
- [DRY-ing Out Your Sass Mixins](http://alistapart.com/article/dry-ing-out-your-sass-mixins)
- [The Mixin Directive](http://www.sitepoint.com/sass-basics-the-mixin-directive/)

###Placeholders

Unlike mixins, placeholders can be used multiple times without being printed out in the stylesheet. Just like `extends()`, placeholders group selectors.

Some examples where a placeholder is most fitting:

- Typography
- Re-usable chunks of properties (shadows, font styles, background styles … etc)

Further reading:
- [Understanding Placeholder Selectors](http://thesassway.com/intermediate/understanding-placeholder-selectors)
- [Dynamic Placeholders](http://advancedsass.com/articles/dynamic-placeholders-in-sass.html)

---
#Suggested

###Property Ordering

Currently there are three display styles:

1. Alphabetical Order
2. Declaration Type (position, display, colors ... )
3. [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS) (starts outside, moves inward)



|      | Alphabetical                                                        | Decelaration                                                       | Concentric                                           |
|------|---------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------|
| Pros | No argument about sorting of properties.                            | Declarations are grouped together.                                 | No argument about sorting of properties.             |
| Cons | Weird not seeing width & height or bottom & top next to each other. | Lots of room for interpretation, where does white-space belong to? | Requires time to adapt & recall order of properties. |

Focusing on alphabetical or concentric requires recollection or time to sort accordingly. Utilizing declaration leaves some room for interpretation. However, declarations are grouped together and just as easy to find. There’s no hard rule set on ordering, especially when most rule declarations contain on average 5–8 properties.

Here is a suggested declaration order:

- Display
- Positioning
- Colors & Typography
- View: Opacity & Visibility
- CSS3: Animations, Transforms, Transitions
- Miscellaneous: Pointers, Overflows, Scrolling …
- Z-index

###Naming Conventions

Naming conventions in CSS are hugely useful in making your code strict, transparent, & more informative. A good naming convention will be able to tell you:

- what type of thing a class does
- where a class can be used
- what else a class might be related to


Additionally you can prefix your class names with the type of pattern they belong to. This makes it fundamentally easier to associate not only the place your styles are located at, but JavaScript too.

| .comp-          | for components                                                         |
|-----------------|------------------------------------------------------------------------|
| .mod-           | for modular elements comprised of components                           |
| .sec-           | for sections inside of a container                                     |
| .landing-       | for indicating the content container (without global header or footer) |
| .page- / .node- | for indicating the page                                                |

An example below:

- We have a body class of .page-about in case we need to add high level styles
- We’re using `.global-` prefix on the global header and footer
- If we need to add specific styling to the about content, we can do so through `.landing-about`. Or if we need to over-write component or module styles that are a bit unique or different on the about page. We can do so through `.landing-about` without going on the high level body class.
- Our banner is reused on all content pages. We use the `.mod-` prefix indicating that.
- Our content specific to the about page like history, timeline, & team will not be used on any other pages. Because of that we’ll prefix it with `.sec-`

```html
<body class="page-about">
  <header class="global-header"></header>
  <article class="landing-about">
    <header class="mod-banner"></header>
    <div class="mod-slider"></div>
    <div class="sec-history"></div>
    <div class="sec-timeline"></div>
    <div class="sec-team"></div>
  </article>
  <footer class="global-footer"></footer>
</body>
```

Because of our prefixing, we’re able to nest less within the Sass, but also able to organize our styles into components, modules, & pages.

Our about styles would contain:

```sass
.landing-about {
  /* styles overwriting any components or modules */
}
.sec-history {
  /* styles specific to history */
}
.sec-timeline {
  /* styles specific to timeline */
}
.sec-team {
  /* styles specific to team */
}
```
