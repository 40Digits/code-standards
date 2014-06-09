# PHP

**Contents**

- [No Shorthand Tags](#no-shorthand-tags)
- [Remove Trailing Spaces](#remove-trailing-spaces)
- [Single and Double Quotes](#single-and-double-quotes)
- [Indentation](#indentation)
- [Brace Style](#brace-style)
- [Regular Expressions](#regular-expressions)
- [Space Usage](#space-usage)
- [Formatting SQL Statements](#formatting-sql-statements)
- [Database Queries](#database-queries)
- [Naming Conventions](#naming-conventions)
- [Self-Explanatory Flag Values for Function Arguments](#self-explanatory-flag-values-for-function-arguments)
- [Ternary Operator](#ternary-operator)
- [Yoda Conditions](#yoda-conditions)
- [Clever Code](#clever-code)


## No Shorthand Tags

**Important:** Never use shorthand PHP start tags. Always use full PHP tags.

**Correct:**

```php
<?php ... ?>

<?php echo $var; ?>
```

**Incorrect:**

```php
<? ... ?>

<?=$var ?>
```

## Remove Trailing Spaces

**Important:** If you do not omit the closing PHP tag at the end of a file (which is preferred), make sure you remove trailing whitespace.

Also remove trailing spaces at the end of each line of code.


## Single and Double Quotes

Use single and double quotes when appropriate. If you’re not evaluating anything in the string, use single quotes. You should almost never have to escape quotes in a string, because you can just alternate your quoting style, like so:

```php
echo '<a href="/static/link" title="Yeah yeah!">Link name</a>';
echo "<a href='$link' title='$linktitle'>$linkname</a>";
```

An exception to this is JavaScript, which sometimes requires double or single quotes. Text that goes into attributes should be run through `esc_attr()` so that single or double quotes do not end the attribute value and invalidate the HTML and cause a security issue. See [Data Validation](http://codex.wordpress.org/Data_Validation) in the WordPress Codex for further details.


## Indentation

Your indentation should always reflect logical structure. Use real tabs and not spaces, as this allows the most flexibility across clients.

Exception: if you have a block of code that would be more readable if things are aligned, use spaces:

```php
[tab] $foo   = 'somevalue';
[tab] $foo2  = 'somevalue2';
[tab] $foo34 = 'somevalue3';
[tab] $foo5  = 'somevalue4';
```

For associative arrays, values should start on a new line. Note the comma after the last array item: this is recommended because it makes it easier to change the order of the array, and makes for cleaner diffs too.

```php
$my_array = array(
[tab] 'foo'   => 'somevalue',
[tab] 'foo2'  => 'somevalue2',
[tab] 'foo3'  => 'somevalue3',
[tab] 'foo34' => 'somevalue3',
);
```

**Rule of thumb:** Tabs should be used at the beginning of the line and spaces should be used mid-line.


## Brace Style

Braces should be used for multiline blocks in the style shown here:

```php
if ( condition ) {
    action1();
    action2();
} elseif ( condition2 && condition3 ) {
    action3();
    action4();
} else {
    defaultaction();
}
```

Furthermore, if you have a really long block, consider whether it can be broken into two or more shorter blocks or functions. If you consider such a long block unavoidable, please put a short comment at the end so people can tell at glance what that ending brace ends – typically this is appropriate for a logic block, longer than about 35 rows, but any code that’s not intuitively obvious can be commented.

Single line blocks can omit braces for brevity:

```php
if ( condition )
    action1();
elseif ( condition2 )
    action2();
else
    action3();
```

If any related set of blocks is more than one line long then all of the related blocks should be enclosed in braces:

```php
if ( condition ) {
    action1();
} elseif ( condition2 ) {
    action2a();
    action2b();
}
```

Loops should always contain braces as this enhances readability, and allows for fewer line edits for debugging or additional functionality later.

```php
foreach ( $items as $item ) {
    process_item( $item );
}
```

## Regular Expressions

Perl compatible regular expressions (PCRE, `preg_` functions) should be used in preference to their POSIX counterparts. Never use the `/e` switch, use `preg_replace_callback` instead.


## Space Usage

Always put spaces after commas, and on both sides of logical, comparison, string and assignment operators.

```php
x == 23
foo && bar
! foo
array( 1, 2, 3 )
$baz . '-5'
$term .= 'X'
```

Put spaces on both sides of the opening and closing parenthesis of if, elseif, foreach, for, and switch blocks.

```php
foreach ( $foo as $bar ) { ...
```

When defining a function, do it like so:

```php
function my_function( $param1 = 'foo', $param2 = 'bar' ) { ...
```

When calling a function, do it like so:

```php
my_function( $param1, func_param( $param2 ) );
```

When performing logical comparisons, do it like so:

```php
if ( ! $foo ) { ...
```

When type casting, do it like so:

```php
foreach ( (array) $foo as $bar ) { ...

$foo = (boolean) $bar;
```

When referring to array items, only include a space around the index if it is a variable, for example:

```php
$x = $foo['bar']; // correct

$x = $foo[ 'bar' ]; // incorrect

$x = $foo[0]; // correct

$x = $foo[ 0 ]; // incorrect

$x = $foo[ $bar ]; // correct

$x = $foo[$bar]; // incorrect
```


## Formatting SQL Statements

When formatting SQL statements you may break it into several lines and indent if it is sufficiently complex to warrant it. Most statements work well as one line though. Always capitalize the SQL parts of the statement like `UPDATE` or `WHERE`.

Functions that update the database should expect their parameters to lack SQL slash escaping when passed. Escaping should be done as close to the time of the query as possible, preferably by using `$wpdb->prepare()`.

`$wpdb->prepare()` is a method that handles escaping, quoting, and int-casting for SQL queries. It uses a subset of the sprintf() style of formatting.

**Example:**

```php
$var = "dangerous'"; // raw data that may or may not need to be escaped
$id = some_foo_number(); // data we expect to be an integer, but we're not certain

$wpdb->query( $wpdb->prepare( "UPDATE $wpdb->posts SET post_title = %s WHERE ID = %d", $var, $id ) );
```

`%s` is used for string placeholders and `%d` is used for integer placeholders. Note that they are not quoted! `$wpdb->prepare()` will take care of escaping and quoting for us. The benefit of this is that we don’t have to remember to manually use `$wpdb->escape()`, and also that it is easy to see at a glance whether something has been escaped or not, because it happens right when the query happens.

See [Data Validation](http://codex.wordpress.org/Data_Validation) in the WordPress Codex for more information.


## Database Queries
Avoid touching the database directly. If there is a defined function that can get the data you need, use it. Database abstraction (using functions instead of queries) helps keep your code forward-compatible and, in cases where results are cached in memory, it can be many times faster.

If you must touch the database, get in touch with some developers by posting a message to the [wp-hackers mailing list](http://codex.wordpress.org/Mailing_Lists#Hackers). They may want to consider creating a function for the next WordPress version to cover the functionality you wanted.


## Naming Conventions

Use lowercase letters in variable, action, and function names (never `camelCase`). Separate words via underscores. Don’t abbreviate variable names un-necessarily; let the code be unambiguous and self-documenting.

``php
function some_name( $some_variable ) { [...] }
```

Class names should use capitalized words separated by underscores. Any acronyms should be all upper case.

``php
class Walker_Category extends Walker { [...] }
class WP_HTTP { [...] }
```

Files should be named descriptively using lowercase letters. Hyphens should separate words.

`my-plugin-name.php`

Class file names should be based on the class name with class- prepended and the underscores in the class name replaced with hyphens, for example `WP_Error` becomes:

`class-wp-error.php`

This file-naming standard is for all current and new files with classes. There is one exception for three files that contain code that got ported into BackPress: class.wp-dependencies.php, class.wp-scripts.php, class.wp-styles.php. Those files are prepended with class., a dot after the word class instead of a hyphen.

Files containing template tags in wp-includes should have -template appended to the end of the name so that they are obvious.

`general-template.php`


## Self-Explanatory Flag Values for Function Arguments

Prefer string values to just true and false when calling functions.

**Incorrect:**

```php
function eat( $what, $slowly = true ) {
...
}

eat( 'mushrooms' );
eat( 'mushrooms', true ); // what does true mean?
eat( 'dogfood', false ); // what does false mean? The opposite of true?
```

Since PHP doesn’t support named arguments, the values of the flags are meaningless, and each time we come across a function call like the examples above, we have to search for the function definition. The code can be made more readable by using descriptive string values, instead of booleans.

**Correct:**

```php
function eat( $what, $speed = 'slowly' ) {
...
}

eat( 'mushrooms' );
eat( 'mushrooms', 'slowly' );
eat( 'dogfood', 'quickly' );
```


## Ternary Operator

Ternary operators are fine, but always have them test if the statement is `true`, not `false`. Otherwise, it just gets confusing. (An exception would be using `! empty()`, as testing for `false` here is generally more intuitive.)

For example:

```php
// (if statement is true) ? (do this) : (else, do this);

$musictype = ( 'jazz' == $music ) ? 'cool' : 'blah';

// (if field is not empty ) ? (do this) : (else, do this);
```


## Yoda Conditions

```php
if ( true == $the_force ) {
    $victorious = you_will( $be );
}
```

When doing logical comparisons, always put the variable on the right side, constants or literals on the left.

In the above example, if you omit an equals sign (admit it, it happens even to the most seasoned of us), you’ll get a parse error, because you can’t assign to a constant like `true`. If the statement were the other way around ( `$the_force = true` ), the assignment would be perfectly valid, returning `1`, causing the if statement to evaluate to `true`, and you could be chasing that bug for a while.

A little bizarre, it is, to read. Get used to it, you will.


## Clever Code

In general, readability is more important than cleverness or brevity.

```php
isset( $var ) || $var = some_function();
```

Although the above line is clever, it takes a while to grok if you’re not familiar with it. So, just write it like this:

```php
if ( ! isset( $var ) )
    $var = some_function();
```