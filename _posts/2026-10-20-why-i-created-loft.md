---
layout: post
title: "Why I created loft"
---

When there are so many programming languages around already, why build yet another one?

## Where it comes from

During my career in software I built many systems that needed custom data structures to reach
the efficiency we were after. Those were for multi-server setups with many cores and they had to
be rock solid too: a 99.999% uptime is not easily reached.

Loft was, from the start, a way to get the lessons of that career somewhere more people can make
use of them. The data structures I hand-crafted under Java had a common theme that could be
generalised into a language as an in-memory database.

The best use I could imagine for it was games with a dynamic world model.

## The problem games share

C++ is still the most common language for published games, and in my opinion it is not very
helpful for them. A lot of constructs in it can crash a game, and being one of the most
efficient languages around still doesn't help against the actual reasons games get slow.

Those reasons are:
- **Bloat**: features or details that players cannot experience.
- **Memory fragmentation**: the processor and the GPU are waiting on data instead of doing
  something useful. A machine can show 100% activity while most of that time is spent waiting
  for memory. The only cure here is to keep data used together close together, in the order it
  is needed.
- **A second language inside the engine**: even developers fluent in C++, Rust or OpenGL need
  their attention on the game, not on the language.

I cannot really help with the first one. The other two can be helped, though that road is not
short or simple.

## What loft does about it

**Iteration speed.** Change the code while the game runs, instead of compiling, restarting and
playing back to where you were. Loft can already swap an edited function into a running program,
and a compile error leaves the old version running. Changing the shape of the data is the next
step I still have to add.

**Save games and mods.** The data in memory and on disk is one representation: a store saved to
disk is the same bytes the program held. When the code changes, added and removed fields are
carried over, and a save that no longer fits is refused rather than misread. Data can be read
straight from a web server or handed to another process without translation overhead.

**One source, every target.** The same program runs compiled to native code, in WebAssembly, and
as a single HTML page playable in the browser — [Brick
Buster](https://loft-lang.org/loft/brick-buster.html) is one file of loft. Windows, Linux and
macOS are fully supported.

**Running inside an engine.** C# or Lua inside an engine can stop functioning for many reasons,
and the engine then has to step in, keep the rendering running and restart the embedded runtime,
losing what it held. In loft, a fault in a calculation gives an empty value and the game carries
on. The game's data lives in stores, not inside a script's runtime. We take the state so
seriously that the whole program can be switched for a more optimised build while the game keeps
running.

## Who it is for

Small teams and indies, who cannot afford to work around C++'s problems.

## Speed as the condition for readable code

Speed matters, but not because every algorithm in a game needs the same speed. Without speed
comparable to Rust or C++ there will always be a reason to reach for those instead, and to give
up code that is readable for as many people as possible. Rust is already more readable than C++
in many cases, but even it has many constructions that baffle a curious reader without years of
experience. That is not a slight against Rust; it is a complex language. Loft tries to prevent
that as much as possible.

The same goes for the libraries: a slow routine is work for the compiler, never a hand-written
Rust shortcut, so nobody has to read Rust to read a library. For example, a matrix
multiplication in the 3D library started forty times slower than its Rust twin but ended up
faster, without any change to the library. The compiler learned to keep a temporary result off
the heap altogether, and every program with the same shape got the same gain.

## Useful in the end, not today

I am convinced loft will be useful in the end. I am not claiming it is useful today.

Getting there is a hard but reachable goal. Once it is reached, a whole class of problems that
can halt a project is solved. Loft and its libraries take on the hard work so developers don't
have to.

To be useful, loft needs speed and stability. Compiled loft is already a quick language: about
twice the time of the same routine in Rust, down from nearly three times at the start of
October. "Slower than Python" is true only of the interpreter, and even there the gap is now
small on most tests. The interpreter is not how the games run, nor how most code runs during
development. It is there for turnaround: an instant start, editing while the game runs, the
debugger.

Stability has two sides. The meaning of a program is close to locked in: written down as formal
rules, nearly all of them with a test by now. But the code the compiler generates is still very
much under construction, to make it faster. So I will not call loft stable until most of the
planned optimisations are in.

Implementation changes are very hard to stabilise. A routine that worked fine yesterday can
suddenly stop working because the optimiser chose another implementation for it, with new bugs.

The end goal here is that every working program will keep on working. That is a promise for the
future, and it can only be judged after the fact.

*Loft is open source: [github.com/loft-lang/loft](https://github.com/loft-lang/loft).*
