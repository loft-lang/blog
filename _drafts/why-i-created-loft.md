---
layout: post
title: "Why I created loft"
---

When there are so many programming languages around already, why build yet another one?

## Where it comes from

During my career in software I built many systems that needed custom data structures to reach
the efficiency we were after. Those were for multi-server setups with many cores and they had
to be rock solid too: a 99.999% uptime is not easily reached.

Loft was, from the start, a way to get the lessons of that career somewhere more
people can make use of them. The data structures I hand-crafted under Java had a common
theme that could be generalized into a language as an in-memory database.

The best use case for this I imagined was writing games with a dynamic world model.

## The problem games share

C++ is still the most common language for published games, and in my opinion it is not very
helpful for them. A lot of constructs in it can crash a game, and being one of the most efficient
languages around still doesn't help against the actual reasons games get slow.

Those reasons are:
- **Bloat**: features or details that players cannot experience.
- **Memory fragmentation**: the processor and the GPU are waiting on data instead of doing
  something useful. A machine can show 100% activity while most of that time is spent waiting
  for memory. The only cure here is to keep data used together close together, in the order it is needed.
- **A second language inside the engine**: even developers fluent in C++, Rust or OpenGL need
  their attention on the game, not on the language.

I cannot really help with the first one. Both others can be aided, though that road is not
short or simple.

## What loft does about it

**Iteration speed.** Change the code while the game runs and keep its state, instead of
compiling, restarting and playing back to where you were. Loft can already swap an edited
function into a running program at the next frame, and an edit that does not compile leaves the
old version running. For now that covers the bodies of functions; changing the shape of the data
is the next step, and our own games still have to switch it on.

**Save games and mods.** The data in memory and on disk is one representation: a store saved to
disk is the same bytes the program held. When the code changes, added and removed fields are
carried over, and a save that no longer fits is refused rather than misread. The same store can
be read straight from a web server or handed to another process or machine without translating
anything.

**One source, every target.** The same program runs compiled to native code, in WebAssembly, and
as a single HTML page playable in the browser —
[Brick Buster](https://loft-lang.org/loft/brick-buster.html) is one file of loft. This month
Windows joined Linux and macOS as a fully supported platform.

**What makes loft unique in its embedding.** C# or Lua inside an engine can stop functioning for
many reasons, and the engine then has to step in, keep the rendering running and restart the
embedded runtime, losing what it held. In loft a fault in a calculation gives an empty value and
the game carries on, and the game's data lives in stores, not inside a script's runtime. We take
the state so seriously that the whole program can be switched for a more optimised build while
the game keeps running. The missing piece is converting the stores when a data definition
changes: it is outlined, it needs few new routines, but a lot of testing. It is a nice example of
what we try to reach with loft.

## Who it is for

Small teams and indies, who cannot afford to work around C++'s problems.

## Speed as the condition for readable code

Speed matters, but not because every algorithm in a game needs the same speed. Without speed
comparable to Rust or C++ there will always be a reason to reach for those instead, and to give
up code that is readable for as many people as possible. Rust is already more readable than C++
in many cases, but even it has many constructions that baffle a curious reader without years of
experience. That is not a slight against Rust; it is a complex language. Loft tries to prevent
that as much as possible.

The libraries follow the same rule: a slow routine is work for the compiler, never a
hand-written Rust shortcut, so nobody has to read Rust to read a library. This month showed why.
A matrix multiplication in the 3D mesh library started October almost forty times slower than
its Rust twin and ended up faster than it, without a line of the library changing. The compiler
learned to keep that throwaway matrix out of memory altogether, and every program with the same
shape got the same gain.

## Useful in the end, not today

I am convinced loft will be useful in the end. I am not claiming it is useful today.

It is a hard but reachable goal. Once it is reached, a whole class of problems that can halt a
project is solved. We take on the hard work so its users don't have to.

Compiled loft is already a quick language: about twice the time of the same routine in Rust, down
from nearly three times at the start of this month. "Slower than Python" is true only of the
interpreter, and even there the gap is now small on most tests. The interpreter is not how the
games run, nor most code during development; it is there for turnaround: an instant start,
editing while the game runs, the debugger. Once compiled code is close to Rust, the interpreter
gets its own overhaul.

What it needs to be useful is speed and stability. Stability has two sides. The meaning of a
program is close to locked in: written down as formal rules, nearly all of them with a test by
now, and this month those tests moved into
[their own repository](https://github.com/loft-lang/loft-suite), so every change to loft is
checked against a promise that did not move with it. The implementation is still very much under
construction, and the separation is what lets it keep changing for speed without changing what a
program means.

Implementation changes are very hard to stabilise. A routine that worked fine yesterday can
suddenly stop working because the optimiser now chose another implementation for it, with new
bugs. It happened this month: a new optimisation made compiled code silently lose a list it
should have added to. It was found by testing the cases around it, and turning that one
optimisation off confirmed the culprit straight away, because every optimisation has its own
switch.

The intention is that a working program keeps working. That is a promise for the future, and it
can only be judged after the fact.

*Loft is open source: [github.com/loft-lang/loft](https://github.com/loft-lang/loft).*
