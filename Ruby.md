# Ruby Styleguide

Please add to this guide if you find any particular patterns or styles that we've adopted internally. Submit a pull request to ask for feedback.

## Formatting

* Use UTF-8.
* Use soft-tabs, 2 space width.
* Strip whitespace from all empty lines.
* Use Unix-style line endings.
* Always include a blank new line at the end of every file.
* Use spaces around operators (except `!`), after commas, colons and semicolons.
* No spaces after `(`, `[`, `{` and before `}`, `]` and `)`.
* No spaces after !.

```ruby
  !array.include? element
```

* Don't indent the `when`s, but indent the `when` blocks.
e.g.

``` ruby
  case something
  when 1
    # do something here
  when 2
    # do something here
  else
    # do something else here
  end
```

* Indent code after `private` or `protected` statements, but outdent those statements to be inline with the class definition.
All `end`'s should be consistently outdented if you do this correctly.
* Ensure a new line after `private` or `protected` keywords.
* Use an empty line before the return value of a method (unless it only has one line).
* Use an empty line between method definitions.
* Document your code consistently where needed using [Yardoc](http://yardoc.org/).
* Always write a README in the root of the project in Markdown.
* Use empty lines to break up a long method into logical paragraphs, but try to keep methods short and logical.
* Try keep lines fewer than ~80 characters.
* Place public API methods at the top of your classes.


## Syntax

* **Seattle Style**
  * Only use parentheses when absolutely required.
  * Use `def` with **no** parentheses around arguments.
* Never use `for`, unless you exactly know why.
* Use `then` sparingly. One word conditionals AND code blocks are pretty much the only excuse.
* Use `&&`/`||` for boolean expressions, `and`/`or` for control flow. (Rule of thumb: If you have to use outer parentheses, you are using the wrong operators.)
* Use `!` instead of `not`
* Avoid multiline ?:, use if.
* Prefer {...} over do...end.  Multiline {...} is fine: having different statement endings (} for blocks, end for if/while/...) makes it easier to see what ends where. But use do...end for "control flow" and "method definitions" (e.g. in Rakefiles and certain DSLs.) Avoid do...end when chaining.
* Surround the contents within braces {} with a space when used as blocks, and have no spaces when used as a hash.
* Avoid return where not required.
* Avoid line continuation `\` where not required.
* Do not use the return value of `=`

``` ruby
  value = array.grep(/foo/)
  if value ... # Good

  if value = array.grep(/foo/) ... # Bad
```

* Use ||= freely.
* Expect the default value of arguments to be nil and assign default on first line:

``` ruby
  def run(options = nil)
    options ||= {}
    ...
```

* Use non-OO regexps (they won't make the code better).  Freely use
  =~, $0-9, $~, $` and $' when needed.
* Don't use `!` in conditions, use `unless` instead
* But, prefer `if` over `unless`, using different query methods where appropriate:

```ruby
  # This is bad
  if !pages.empty?
    # ...
  end
```

```ruby
  # This is better
  unless pages.empty?
    # ...
  end
```

```ruby
  # This is best
  if pages.any?
    # ...
  end
```

* When definining multiline hashes and arrays, use trailing commas. This
  prevents errors when adding items, and results in better line diffs.

```ruby
  people = [
    huey,
    dewey,
    louie,
  ]

  wealth = {
    donald: "poor",
    scrooge: "rich",
  }
```


## Naming

* Only the names of potentially *dangerous* methods should end with an exclamation mark. Bang methods should only exist if a non-bang method exists.
* Use `snake_case` for methods.
* Use `CamelCase` for classes and modules. (Keep acronyms like HTTP, RFC, XML uppercase.)
* Use `SCREAMING_SNAKE_CASE` for other constants.
* Be descriptive with block variables and use `_` to identify unused variables.
* Prefer `map` over `collect`, `find` over `detect`, `find_all` over `select`, `size` over `length`.


## Comments

* Inline comments are to be avoided as the code should be self documenting.
* If a comment is required use a comment block above the method definition that
  describes **what** the method does not **how** it is implemented.
* All comment blocks should be formatted using yardoc style metadata, this
  allows you to specify parameters, return values, notes etc.
* Leave no TODOs or NOTEs. Prefer raising a GitHub issue (usually technical
  debt).

``` ruby
# Calculates the complexity of a method.
#
# @note The call to `foo_bar` is required because of a rails quirk that will be
#   fixed in 4.1.
# @see {https://github.com/rails/rails/issue/41}
# @param [string]
# @return [Integer] the complexity of a method
def a_complex_method method_name
  foo_bar
end
```


## Testing

* Use MiniTest (and not MiniTest::Spec).
* Red-Green-Refactor is srs bsns. Write a failing tests first, then make it pass. Improve your test, improve your code. Stop when shit is awesome.
* One assertions per test case.
* Write the minimum amount of code to make your tests pass. If you feel the need to write more code, you're probably not testing it properly.
* Write unit tests which do not require huge amounts of fixtures in order to run, if they do then you're doing it wrong.
* Only test your public API methods, private methods should be tested as a result of testing public methods.
* If you find that your need to test your private methods consider grouping and moving them into their own class - you'll thank me later.


## Example Class

Taking from everything above we've put together a sample class that
hopefully represents our style.

``` ruby
class Person
  attr_accessor :name

  def initialize name
    self.name = name
  end

  def consume drink
    drinks << drink
  end

  def drinks
    @drinks ||= []
  end

  def energised?
    drinks.find { |drink| drink.energises_you? }.any?
  end
end

class RedBull
  attr_accessor :count, :size

  def initialize attributes = nil
    attributes ||= {}
    self.count = attributes.fetch :count, 1
    self.size  = attributes.fetch :size, 350
  end

  def energises_you?
    true
  end
end

red_bull = RedBull.new
person = Person.new 'Tim Cooper'
person.consume red_bull
person.energised? # => true
```
