---
layout: post
title: "A team of eager juniors who google a lot"
---

Building a project with AI agents is not that different from running a project with a
whole bunch of eager but inexperienced programmers who love to google.

They are eager: they never sleep and will happily take on anything you point them at.
They are inexperienced: they take no time to find where a problem really comes from, so
they fix exactly the problem in front of them and miss the fix that was actually needed.
And they google a lot: they know a great deal about programming in theory and nothing
about my language unless already documented.

None of this is new. Every team lead has managed such people. What is new here is having
them available for the price of a subscription. This post is about what that has meant for
loft, the programming language I am building to ease the creation of games.

## Loft is not a new language

Loft had been in development for eight years before any AI was involved. The agents did not
invent it; they inherited it and built it out.

What changed is not only the development speed: the language has also become much more
complete, because it is now quick to compare loft against other languages like Julia, OCaml or
Python. What those languages can express is turned into tests, and each failing test forces a
decision: is this a missing feature, a language bug, or something we do not want to implement
at all?

## What I actually do

I write very little of the code myself now. My work is steering: guiding the agents around
problems and devising ways of working that enhance what they are good at while covering
for what they tend to overlook.

Their strengths are easy to list: they are fast, they do not tire, they know a lot, and they
follow a written method faithfully once they have read it. Their blind spots are just as
clear: they remember nothing between sessions, they rush to a fix, they trust their own
explanation, and they apply what is true in general where it is not true here.

So most of my effort goes into how the project works rather than into its code. I find the
blind spots through frustration: when the AI makes the same mistake several times, that is one.
Each is then investigated and turned into a document, skill or tool that makes it less of a
risk.

## AI agents remember nothing

An agent starts every session without memory. Everything that needs to be remembered has to be
in the project itself: the bugs, the features, the rules, the design decisions, each tagged so
it can be found and tested again. The documentation is not a nice extra; it is the team's
memory.

That memory goes stale, just like a person's. Almost anything written in a document might be
true on the day it is written, and is certainly wrong a month later. So documents should hold
as few facts that can go stale as possible, and be easy to check.

None of this is unique to AI. A team of people needs the same discipline. Individual people
just hide the problem by vaguely remembering things. Agents cannot, so the gaps show up
immediately. It is the same as when experienced team members leave and new ones replace them
— except that with agents, it happens every session.

## The exact problem is fixed, but its cause is not

This is where inexperience shows most. An agent finds a bug, finds a change that makes the
failing case pass, and stops. The exact problem is fixed, but the place it came from is not,
and the same mistake keeps living elsewhere. Over time you get many slightly different copies
of the same logic, each patched for its own bug, with no design holding them together.

Optimisation shows it even more clearly. The profiler points at a slow line, and the tempting
fix is a special shortcut for exactly that line. It works, and it helps nothing else. Looking
for the source usually finds something different, and fixes every program that has the same
shape. That is why loft treats a slow library routine as work for the compiler, never as a
place for a hand-written shortcut.

Two things help. The first is making it cheaper to look than not to: before fixing anything
non-trivial, each agent has to map out the cases around the bug. Only when both the working and
the failing cases are mapped can it be sure it has found the real boundary. For a person that
would be slow, but an AI does it quickly, and it is still small next to the time the fix and
its tests take.

The second is a set of formal rules: precise statements of how the language must behave. The
rules come first, and code that disagrees with them is what gets fixed. When a bug comes in,
the rules usually already say what the right answer is, so there is much less guessing. But
the rules only help if they are checked again and again. They are also the way to find
duplicated code and the errors in it: when two pieces of code implement the same rule
independently, one can be right and the other wrong, and the rule shows where to merge them.

## Tests introduce new problems too

Agents write a lot of tests. That is good in itself, but the tests become a system of their
own that needs managing: how long they take, how much memory they use, how much disk space they
fill when several agents run them beside each other on the same machine.

And a test that cannot fail is worse than no test, because it makes you feel safe. So each new
test is checked against the old, broken version of the code, to prove it would have caught the
bug it was written for. Eager programmers write a lot of tests; some process has to check that
the tests are actually testing something.

## The upside of using AI

With all those challenges, why do it? Because the result is worth it.

- Work happens while I sleep. Several agents work through the night on different parts of
  the language.
- Bugs are found by checking rules, not by waiting for users. Most bugs now show up when
  the rules are validated or loft is compared with other languages, before anyone runs into
  them in a real program.
- The turnaround of bugs is fast. A bug is often fixed within the hour, with a new test that
  proves it.
- The cost is relatively low. I pay about 200 euro a month. Before it, getting the base
  language into a good shape meant taking half a year of sabbatical.

## Starting yourself?

Let the AI fix a couple of bugs. See where it fails, takes the wrong turn, invents things on
its own that do not fit your plan. Those problems are not inherent to AI; they show the gaps in
your setup: designs that are hard to find, old bugs nobody can learn from, a project that is
too much of a mess. And yes, left alone, an AI will make that mess for you.

This is not really advice about AI. It is advice about leading a team. The AI just makes it
impossible to skip.

*Loft is open source: [github.com/loft-lang/loft](https://github.com/loft-lang/loft). The rules,
the working methods and the record behind everything in this post are in the repository.*
