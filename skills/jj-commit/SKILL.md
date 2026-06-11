---
name: jj-commit
description: Commit your work so far using jj VCS
---

Commit your work so far using `jj commit`, following the guidelines below.

## Commit message structure

- Subject line
- Blank line
- Body (optional)

### Subject line

A concise, imperative, one line description of what was changed

When someone is viewing the commit history, they want to be able to quickly and easily judge from the first line of each commit:

- what area of the codebase was changed
- what the nature of the change was

This lets them quickly and accurately filter down to the set of commits that
they're interested in. For example when debugging an auth issue they will be
looking for recent commits that touched the auth flow and login page etc. Ensure
your commit subject line meets these two criteria.

### Optional body

For simple changes where just the subject line is enough you can omit the body
entirely. For example if the commit is "Fix typo on homepage" someone browsing
the history can just quickly view the diff to see the change, additional context
is unncessary.

For larger or more complex changes the body provides additional context on the
"what" and "why" of the change, not the "how". In most cases you can leave out
the details about "how" a change has been made entirely. Code is generally
self-explanatory (and if the code is so complex that it needs to be explained in
prose, that’s what source comments are for). Just focus on making clear the
reasons why you made the change in the first place — the way things worked
before the change (and what was wrong with that), the way they work now, and why
you decided to solve it the way you did.

Be succinct, the viewer can always read the full diff. The point of the commit
message is to save time compared to gathering a deep understanding of and trying
to reverse engineer the reasoning behind a change. A super long message defeats
this.

## Example of a good commit message

As the commit message to a very large diff, this message provides a clear and
succinct overview of what was changed, and the reason why.

```sh
jj commit -m "Simplify serialize.h's exception handling

Remove the 'state' and 'exceptmask' from serialize.h's stream
implementations, as well as related methods.

As exceptmask always included 'failbit', and setstate was always
called with bits = failbit, all it did was immediately raise an
exception. Get rid of those variables, and replace the setstate
with direct exception throwing (which also removes some dead
code).

As a result, good() is never reached after a failure (there are
only 2 calls, one of which is in tests), and can just be replaced
by !eof().

fail(), clear(n) and exceptions() are just never called. Delete
them.
"
```
