# JavaScript

**Contents**

- [Use Strict](#use-strict)
- [Braces](#braces)
- [Quotations](#quotations)
- [Whitespace](#whitespace)
	- [Indentation](#indentation)
	- [Trailing Whitespace](#trailing-whitespace)
- [Naming Conventions](#naming-conventions)
	- [Constructors](#constructors)
	- [Filenames](#filenames)
- [The var Keyword](#the-var-keyword)
- [Operators](#operators)
- [Objects](#objects)
- [Arrays](#arrays)
- [Conditionals](#conditionals)
	- [if/else](#if-else)
	- [Ternary](#ternary)
	- [switch](#switch)
- [Loops](#loops)
	- [for](#for)
	- [forin](#forin)
	- [while](#while)
	- [do](#do)
- [jQuery](#jquery)


## Use Strict

Always.


## Braces

Braces should be used for multi-line blocks in the style shown here:

```javascript
var a, b;
if ( a && b ) {
    action1();
    action2();
} else if ( a ) {
    action3();
    action4();
} else {
    defaultAction();
}
```

**Rule of Thumb**

Opening brace should be on the same line as the function definition, the conditional, or the loop. Closing brace should be on the line directly following the last statement of the block.


## Quotations

Single quotes are preferred over double quotes, for the sake of simplicity; however, double quotes should be used when appropriate.

```javascript
'Just your everyday string.';

// Use double quotes when a string contains single quotes
"Note the capital 'P' in WordPress";
```


## Whitespace

Use spaces liberally throughout your code. Proper spacing drastically improves the legibility of any line of code.

### Indentation

As with any programming language, indent your code to reflect the structure of the program.

Use tabs, not spaces, as this allows the most flexibility across clients. Many wars have been fought over the use of tabs versus spaces. We use real tabs in WordPress core – please respect that.

Always put spaces on both sides of the opening and closing parenthesis of `if`, `else if`, `for`, `forin`, `do`, `while`, and `switch` blocks.

**Rule of Thumb**

Tabs should be used at the beginning of the line, and spaces should be used mid-line.

### Trailing Whitespace

Remove any whitespace from blank lines.

Whitespace can also easily accumulate at the end of a line – avoid this where possible. One way of catching whitespace buildup is to enable visible whitespace characters within your text editor.

This should be done prior to minification.


## Naming Conventions

Name functions and variables using camelCase, not underscores.

### Constructors

Name constructors with TitleCase.

```javascript
var myVariable = 5,
    MyConstructor = function() {
        this.attr = 'example';
    };
```

### Filenames

Separate words in files using hyphens. Include both an uncompressed version with the format **file-name.js**, and a compressed version using the format **file-name.min.js**.


## The *var* Keyword

Each function should begin with a single comma-delimited `var` statement that declares any local variables necessary. If a function does not declare a variable using `var`, it will be assigned to the current context (which is frequently the global scope, and worst scenario), and can unwittingly refer to and modify that data.

Assignments within the `var` statement should be listed on individual lines, while declarations can be grouped on a single line. Any additional lines should be indented with an additional tab.

```javascript
var i, j, length,
    value = 'WordPress';
```

Objects and functions that occupy more than a handful of lines should be assigned after the `var` statement.


## Operators

Surround operators with spaces in order to properly show the order of operations:

```javascript
var i;
i = ( 20 + 30 ) - 17;
```


## Objects

Create objects with curly bracket notation, and not new `Object()` notation.

When declaring objects, place a space after the colon, but not before. Similarly, in `var` statements and objects, place a space after the comma, but not before.

When declaring an object with more than one key, it is advisable to give each key its own line.

```javascript
var a = { key: 'value' },
    b, c;

b = {
    key1: 'value1',
    key2: 'value2'
};
```

Never end an object with a comma. Internet Explorer violently rejects trailing commas (much to our chagrin), and trailing commas are not valid ECMAScript.

```javascript
a = {
    key1: 'value',
    key2: 'value'  // A comma here would cause IE to implode.
};
```


## Arrays

In JavaScript, associative arrays are defined as objects. Creating arrays in JavaScript should be done using the shorthand `[]` constructor rather than the new `Array()` notation.

```javascript
var myArray = [];
```

You can initialize an array during construction:

```javascript
var myArray = [ 1, 'WordPress', 2, 'Blog' ];
```

Space should be placed between after the opening bracket and before the closing bracket. Each index should be separated by a comma and a bracket.


## Conditionals

There are three types of conditions that exist within JavaScript: if/else, the ternary operator, and the switch statement.

### if/else

`if/else` is subjected to the spacing guidelines that are outlined above.

This includes:

- Variables should be defined outside of the scope of the conditional.

- A function can be passed as the evaluation of the conditional.

Finally, braces should always be used.

```javascript
var a, b, c;
if ( myFunction() ) {
    // ...
} else if ( ( a && b ) || c ) {
    // ...
} else {
    // ...
}
```

### Ternary

The ternary operator generally follows the same rules as the documentation for the ternary operator for PHP. To paraphrase, they are acceptable to use but only if the result yields a `true` or `false` value. Otherwise, it becomes difficult to read.

So this is acceptable:

```javascript
var fixedP;
fixedP = 'WordPress' === $('#comment').val() ? true : false;
```

But this is not:

```javascript
var fixedP;
fixedP = 'wordpress' === $('#comment').val() ? "WordPress" : $('#comment').val();
```

### switch

Switch follows the same conditions as `if/else` conditions above.

```javascript
// Assuming that myFunction() returns a string of 'foo' or 'bar'
switch ( myFunction() ) {

    case 'foo':
        // ...
        break;

    case 'bar':
        // ...
        break;

    default:
        //
        break;

}
```

Note that case should be indented by a single tab as should the terminating break. There should always a default case. Like object declarations, there should be no space before the colon.


## Loops

There are a variety of loop constructors offered by JavaScript, each of which are similar to those offered by PHP. Though there’s no preferred loop to use, there are standards by which you use each of them.

### for

Both the index and the length of the array should be declared prior to the loop, and the values set as the first argument of the loop.

Benchmarks have shown that this yields the fastest, cross-browser for loop performance.

```javascript
var i, l;
for ( i = 0, l = 10; i < l; i++ ) {
    // ...
}
```

### forin

`forin` is typically used to iterate through the contents of an object, but is often used to iterate through the contents of an array, as well.

In WordPress-based JavaScript, we prefer to use a classical `for` loop to clearly iterate through the contents of an array; however, if you are iterating through an object, then this is the proper way to do so:

```javascript
var foo, bar;
for ( foo in bar ) {
    // ...
}
```

### while

`while` loops are preferred over `do` loops, and should be formatted with the variables for evaluation outside of the loop:

```javascript
var a, b;
while ( a && b ) {
    // ...
}
```

If a condition is being used to return a boolean value, then it can be passed as the argument to the loop:

```javascript
while ( condition() ) {
    // ...
}
```

### do

`do` loops are similar to `while` loops in that all variables should be defined outside of the scope of the loop, or the condition can be passed as the argument to the array.

The `while` should be stated on the same line as the closing brace of the `do` statement:

```javascript
var a, b;
do {
    // ...
} while ( a && b );
```


## jQuery

There are a number of different ways to resolve conflicts with jQuery and other plugins. Unfortunately, there’s no consistent way in which this is done, which ultimately results in one plugin breaking another plugin because the jQuery `function` isn’t properly relinquished.

To avoid this, define an anonymous `function`, and pass jQuery as the argument before doing anything else:

```javascript
(function ($) {
    // ...
}(jQuery));
```

This will negate the need to call `noConflict` or to set the `$` using another variable.