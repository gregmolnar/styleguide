# Javascript Styleguide

Please add to this guide if you find any particular patterns or styles that we've adopted internally. Submit a pull request to ask for feedback.

## Formatting

* Use UTF-8.
* Use soft-tabs, 2 space width.
* Strip whitespace from all empty lines.
* Use Unix-style line endings.
* Use spaces around operators, after commas, colons and semicolons.
* No spaces after `(`, `[`, `{` and before `}`, `]` and `)`.
* All statements **must** end with a semicolon.
* All statements inside of a scope that spans multiple lines should be intended. Scopes on a single line should surround their content with a single space. e.g.

```javascript
// multi line
function() {
  doSomething();
}

// single line
function() { doSomething(); }
```
* All conditionals and loops should have a space between the keyword and the expression.
* `if else`, `else`, `catch` and `finally` should follow directly after the end of the preceeding condition.

```javascript
if (something) {
  doSomething();
} else {
  doSomethingElse();
}

try {
  doSomething();
} catch(e) {
  handleError(e);
}
```

* Use an empty line before the return value of a method (unless it only has one line).
* Use an empty line between method definitions.
* Use empty lines to break up a long method into logical paragraphs, but try to keep methods short and logical.
* Try keep lines fewer than ~80 characters, but it's not enforced.

## Syntax

* All scopes must begin on the same line as its declaration, separated by a space.
* Declare multiple variables using a single `var` separated with commas. All variable declarations with assignment should be placed on a separate line and have double indentation to line up with the first variable. e.g.

```javascript
var foo = "bar",
    abc = 123,
    x, y;
```

* Always declare your variables, even when used within `for` loops. i.e.

```javascript
for (var i = 0; i < length; ++i) ...
```

## Naming

* Use `headlessCamelCase` for variables, methods and functions.
* Use `CamelCase` for objects.
* Use `SCREAMING_CAMEL_CASE` for constants.
* The length of an identifier determines its scope. Use one-letter variables for short block/method parameters, according to this scheme:
  * a,b,c: any object
  * d: directory names
  * e: rescued exceptions
  * f: files and file names
  * i,j: indexes
  * k: the key part of a hash entry
  * m: methods
  * o: any object
  * r: return values of short methods
  * s: strings
  * v: any value
  * v: the value part of a hash entry
  * x,y,z: numbers.
* Use _ or names prefixed with _ for unused variables.

And in general, the first letter of the class name if all objects are of that type.

## Comments

* Comments longer than a word are capitalised and use punctuation.
* Avoid superfluous comments, your code should be self documenting.
* TODOs are fine, but any TODOs over three-months old will be deleted.
* Profanity is A-OK. If your comment doesn't help me learn, it damn well should make me laugh.
