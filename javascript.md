# The 40Digits JavaScript Guide

## Introduction
This guide provides a brief overview of tools and methodologies used in JavaScript development at 40Digits.  Use it as a starting point to understand the build cycle and to find out more information about our tools.


## Writing JavaScript
Our projects are written in ES2015, the current JavaScript standard.  We strive for organization and readability through our code, providing a powerful and extensible development environment to help us create the ultimate product.

### Code Style
We follow the [Airbnb JavaScript guide](https://github.com/airbnb/javascript). This guide brings many benefits:
* It is fully up-to-date with ES2015 standards
* Wide community support and adoption
* Readily available tools (linters, formatters, etc.)
* An alternative guide for JSX and React

#### Linting
We use [`eslint`](http://eslint.org/) to help ensure that code follows the guide.  It's pluggable, meaning it can be used on its own or through a variety of text editors and build scripts.  See [the integrations documentation](http://eslint.org/docs/user-guide/integrations.html) for a full list of ways to integrate `eslint`.  Use these packages to ensure `eslint` is working in your editor.
* **Sublime**: [SublimeLinter-eslint](https://github.com/roadhump/SublimeLinter-eslint) and [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter3)
* **Atom**: [linter-eslint](https://atom.io/packages/linter-eslint) and [linter](https://github.com/atom-community/linter)
* **Vim**: [eslint.vim](https://github.com/scrooloose/syntastic/blob/master/syntax_checkers/javascript/eslint.vim)
* **PHPStorm**: Refer to the [official docs for enabling `eslint`](https://www.jetbrains.com/phpstorm/help/eslint.html)

The `.eslintrc` file at the base of the project will be used to set the settings that eslint will follow.


### Organization
JavaScript files are compiled into a deliverable, so developers can organize them modularly based on purpose. The following directories inside `src/js` organize where files should be located:
* `components` - reusable UI pieces, e.g. `Accordion.js` could be an accordion.
* `config` - configuration files.  Use `bundles.js` to set up which files Eta compiles for your project.
* `lib` - third party libraries intended to be compiled in with the rest of the script.
* `modules` - a reusable section of logic.  Not intended to be used for views or reusable UI components.
* `templates` - EJS templates for unique views or modular sections.
* `views` - a file related to a single view, e.g. `ProjectList.js` might set up a list of projects.  This usually couples with templates from `templates`.


## Building JavaScript

### Eta
We use our own [`gulp-eta`](https://github.com/40Digits/gulp-eta) to provide a preset list of gulp tasks to run.  Each of these components below are used with gulp to turn the JavaScript we write into the JavaScript that runs in the browser.

#### Gulp
We use *Gulp* to run tasks that automate actions on code.  Tasks can be used to compile the JS, minify the code, and much more.  All of our JavaScript compilation is currently orchestrate by Gulp.

#### Browserify
*Browserify* is used to bundle multiple JavaScript files into one, and intelligently link them together in your application.  Allows for simple, modular code and a small deliverable to the end user.

#### Browserify-shim
*Browserify-shim* converts CommonJS-incompatible files into ones usable by Browserify.  This lets you bundle and use unaltered vendor files without including them directly on the page.

#### Browserify-ejs
*Browserify-ejs* lets us use [EJS templates](http://www.embeddedjs.com/) easily inside JavaScript.  These are often used to represent views or partials.

#### Babel
*Babel* is a tool that transforms newer JavaScript into older JavaScript.  In our case, it's converting mostly unsupported ES2015 into browser-compatible ES5.  See [Babel's documentation](http://babeljs.io/docs/learn-es2015/) about support for ES2015 transforms.

#### Uglify
We use *Uglify* to minify code for production.  This gives us the smallest deliverable file, but still allows us to write cleanly and legibly.


### Compiling
### With the `browserify` task
Run `gulp browserify` to initiate a manual compile and rebundle from within the project.  This will rebuild all files and run all transforms in the `browserify` configuration options.

#### With the `watch` task running
When the `watch` task is running, `.js`, `.ejs`, and `.jsx` files are watched for file changes.  When one of these files is altered, it will be rebundled.


## Writing in ES2015
Using Babel to transpile ES2015 into ES5 for older browsers offers us the ability to write next-gen code while still maintaining support that meets our clients' needs.  We favor ES2015 methodologies over ES5 to provide a consistent code-base for our developers and help prepare us for the future of JavaScript.  The [Babel documentation](http://babeljs.io/docs/learn-es2015/) contains lots of examples to get up-to-speed on new features.

### *Avoid the following* due to poor support when transpiling:
* Native Promises.  Use something like [Q](https://github.com/kriskowal/q) to support this feature.


### Prefer the following ES2015 methods to their ES5 counterparts:
* `let` and `const`.  These block-level variables give you more control over scoping and mutability.

* Template strings.
```javascript
// ES2015 with Babel
const world = 'world';
console.log(`Hello ${world}`);

//ES5
var world = 'world';
console.log('Hello ' + world);
```

* Importing.
```javascript
// ES2015 with Babel
import Accordion from './components/Accordion';

// ES5
var Accordion = require('./components/Accordion');
```

* Exporting.  Use explicit exports to gain more control over what this module can expose, as well as reduce code pulled in when importing.
```javascript
// ES2015
export function foobar(foo, bar) {
  // ...
}
export var pi = 3;
```

* Arrows.  These might just look like syntactical sugar, but sharing the lexical `this` can help save headache and make code cleaner to read.
```javascript
// ES2015
function foo() {
  return () => {
    console.log(this);
  };
}

// ES5
function foo() {
  const that = this;
  return function () {
    console.log(that);
  };
}

// good
```

* Default and rest parameters
```javascript
// ES2015
function foobar(foo, bar='bar') {
}

// ES5
function foobar(foo, bar) {
  bar = (!!bar)? bar : 'bar';
}
```

* Classes. Organize modules and components by classes when they serve a single purpose and represent a new type of object that can be instantiated.
```javascript
// ES2015 with Babel
class Accordion {
  openItem() {
     // ...
  }

  closeItem() {
    // ...
  }
}

// ES5
function Accordion () {
}

Accordion.prototype.openItem = function () {
  // ...
}

Accordion.prototype.closeItem = function () {
  // ...
}
```

See [ES6 equivalents in ES5](https://github.com/addyosmani/es6-equivalents-in-es5) for a thorough list of examples and comparisons between the two.
