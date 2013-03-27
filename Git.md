# Git Styleguide

Please add to this guide if you find any particular patterns or styles that we've adopted internally. Submit a pull request to ask for feedback.

## Commits

* Make separate commits for logically separate changes.
* Make separate commits **only** for logically separate changes.
* Be phrased in the imperative: Add feature, not *Added* feature or *Adds* feature.
* The first line of a commit message should be;
  * Capitalized.
  * Consise. Soft limit of 50 characters.
  * Able to explain the commit, if this is hard it's a good inidcator your commit is doing too many things.
  * Optionally prefix the message with `area: ` where *area* is a filename or identifier for the general area of the code being modified.
* The body of the commit message should be:
  * Verbose.
  * Use correct grammer and full punctuation.
  * Wrapped to 72 characters to allow for the standard indentation from git log, and to leave room for quoting.

Example of an ideal commit message:

```git
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, preceded by a
  single space, with blank lines in between, but conventions vary here

- Use a hanging indent
```
