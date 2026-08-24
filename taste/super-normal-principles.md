# Super Normal

Principles for code, architecture, bugfixes, and prose. After Fukasawa
and Morrison. Not a style. Not a checklist of aesthetics.

The work should be the ordinary example of its kind, complete enough to
live with, and easy to ignore. "Nothing special" is often success.
Work that announces itself — a new layer, a clever sentence, a
framework where a loop would do — usually costs more than it gives.

## Principles

**Do not add what the job does not need.**
A type, section, flag, wrapper, diagram, or paragraph that exists to
look thorough is waste. If removing it loses no behavior, no meaning,
and no safeguard, remove it.

**Start from how this kind of thing is already done.**
In this codebase, this language, this document type, this team's names.
Match that form. Change it only where the current job is wrong or
incomplete. A new kind of module, API, or document is a last resort.

**Take the small step that fits, not the leap that impresses.**
One behavior, one boundary, one claim. Prefer the local helper over the
new layer, the existing heading over the new template, the fix at the
shared owner over a guard at one call site. Large redesigns and large
rhetorical structures fail more often than they land.

**Keep the unglamorous parts that use requires.**
Error handling, "fails when", exact identifiers, a test at a real seam,
the condition a shorter sentence would hide, rollback, ownership.
Deleting those to look clean is not simplicity. It is a later bug or a
later misread.

**Fit the surroundings.**
The change should read as if it already belonged in the file, the
system, or the document. If it needs a tour to explain its shape, it is
probably fighting the grain.

**Judge after use, not at first glance.**
First-glance elegance and first-glance cleverness both decay. The test
is the next call, the next incident, the next edit, the next reread.
Completeness lasts: happy path plus the boring paths.

**Do the job. Do not perform the job.**
No architecture as identity, no methodology costume, no prose that
sounds like an author. If a specialist in this craft would call it
ordinary and correct, stop. Do not label the work Super Normal.

## Where this shows up

**Code.** Ordinary language features and local patterns. No extra
abstraction until a second real consumer or a real boundary exists.
Correct, readable, safe to change.

**Architecture.** Domain and existing boundaries first. One
end-to-end slice. Name owners, contracts, failure, and rollback. Do not
draw a target shape the current pain does not need.

**Bugfix.** A pass/fail loop you can run, then a falsifiable cause, then
a fix at the owner of the mistake. Leave a regression at a real seam.
Remove the instrumentation. Do not guess from reading code.

**Prose.** The native form of this document. Plain language, exact
terms, structure that helps a reader act or understand. No filler, no
fake precision, no nuance deleted to look short.

## Checks

- Would removing this lose a real behavior, a real meaning, or a real
  safeguard?
- Did I start from how this kind of thing is already done here?
- Is this the smallest change that solves the current problem?
- Did I keep the unglamorous parts use needs?
- Can the next person call, read, operate, or change this without
  fighting it?
- Would a specialist call this ordinary and correct, or a statement?

If it passes, stop.

## Not this

Not "as short as possible." Not a ban on types, comments, tests, or
character that earn their keep. Not a reason to skip a repro, a check,
or a precise word. Not minimalism as a look.
