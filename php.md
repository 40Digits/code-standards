# 40Digits PHP Code Standards

### TL;DR
Use [`PSR-1`](http://www.php-fig.org/psr/psr-1/) and [`PSR-2`](http://www.php-fig.org/psr/psr-2/)


## Introduction
The purpose of these standards is to share a set of guides and expectations about how we at 40Digits format our PHP code.


## PHP Version
Unfortunately we have a double standard for our PHP projects:
* Due to the limitations of our production server, we write our Wordpress projects using 5.3. Fear not, we're working on getting that server up to date.
* For all other PHP projects, (when possible) prefer PHP 5.6.
* Sometimes we don't know where the site will be hosted. **Make sure to verify the production server version is compatible with the project version** Do this as soon as possible.


## Code Style
We follow the [PHP Standard Recommendation](http://www.php-fig.org/psr/). This guide brings many benefits:
* Wide community support and adoption
* Readily available tools (linters, formatters, etc.)
* Most popular frameworks follow these recommendations

There's a lot of fluff that comes along with all of the PSRs, we recommend making yourself most familiar with [`PSR-1`](http://www.php-fig.org/psr/psr-1/) and [`PSR-2`](http://www.php-fig.org/psr/psr-2/).


### Additions
This is a list of items that we have chosen to follow in addition to the PSRs
* Use camelCase for methods, functions, properties and variables.
* Don't use short echo tags. `<?= $variable; ?>` should be `<?php echo $variable; ?>`


### Pay attention to these things
This is a list of items we wanted to emphasize that are a part of the PSRs
* Use 4 spaces in all files with the php extension. Even though our JS and CSS files are written using 2 spaces, we've chosen to follow the community adopted standard.
* Make sure to put spaces before and after operators. Meaning don't do `$variable=$variable+1;` make it look like `$variable = $variable + 1;`. Also, pay attention to similar styles in the PSR.


### Suggestions
Here is a list of items that aren't necessarily part of the style guide, but we suggest you follow them anyways
* [Type Declarations (Hinting)](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration): you should use this when you can. (You can't use Type Hinting in 5.3).

### Commenting
We think writing self documenting code is good practice. We also know that we're all terrible at doing that. So we use PHPDOC Syntax to try and help.
* When writing a class or function use [PHPDOC Syntax](http://phpdoc.org/docs/latest/getting-started/your-first-set-of-documentation.html).
* Most modern editors will parse that syntax when searching or making new functions.

Here's an example:

```
 <?php
 /**
  * A summary informing the user what the associated element does.
  *
  * A *description*, that can span multiple lines, to go _in-depth_ into the details of this element
  * and to provide some background information or textual references.
  *
  * @param string $myArgument With a *description* of this argument, these may also
  *    span multiple lines.
  *
  * @return void
  */
  function myFunction($myArgument)
  {
  }
```
There are tools that exist to make our life easier when writing this syntax.
* [Sublime DocBlock](https://github.com/spadgos/sublime-jsdocs)


### Linting
We recognize that linting is essential to helping developers new to a style guide learn the ins and outs. We're working on adding suggestions here.

* [PHPStorm Style Setup for PSR-1 & 2](http://www.matthewsetter.com/enforcing-psr1-and-psr2-with-phpstorm/)


### How to contribute
If you have suggestions, questions, or concerns open an issue (or pull request if you have a suggestion).
* Understand that these affect the team as a whole.
* For suggestions, be sure to include reasons why this would be a good idea to change.
