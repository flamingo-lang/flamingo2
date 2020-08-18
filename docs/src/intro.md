# Introduction

**Flamingo is a DSL for describing state machines in an ultra-compact way,
emphasizing simplicity, modularity, and correctness.** 

Flamingo is built with web apps in mind and ~~compiles to efficient, portable
javascript~~ is interpreted by a WebAssembly backend \[1\]. Flamingo programs
handle _state management_ - you can think of Flamingo as DSL for writing
Redux reducers. Hook up browser events to Flamingo's runtime, bind state changes
to the DOM as views with, e.g., React, and _voilà_! you have a web app!

In terms of language theory, Flamingo is a _logic programming language_, specifically
an extension of [Datalog](https://en.wikipedia.org/wiki/Datalog) that adds an explicit
notion of action and change, negative constraints, and powerful, object-oriented module
system\[2\].


## A Little Example

Here's a small example that models menus that can open and close.
```alm
module menu
sorts
    menu :: universe
        attributes
            title : string
            text : string
actions
    menu_action :: action
        target : menu
    open_menu :: menu_action
    close_menu :: menu_action
fluents
    basic
        open : menu -> booleans
axioms
    occurs(A) causes open(Menu) if
        instance(A, open_menu),
        target(A) = Menu.

    occurs(A) causes open(Menu) if
        instance(A, open_menu),
        target(A) = Menu.
```

Obviously, Flamingo's syntax is quite different from imperative
or functional languages; however, it's ultimately much simpler - this
small example covers the majority of it. We'll cover the syntax
in depth in the coming sections. But first, let's discuss the motivation
behind the language: the tar pit of modern software development.

----------------

[1]: The Flamingo-to-JS is a work in progress. For now, Flamingo is translated
into ASP and interpreted by the [Clingo solver](https://github.com/domoritz/clingo-wasm).

[2]: Flamingo is a mostly-faithful Javascript implementation of the
[Modular Action Language ALM](https://arxiv.org/abs/1505.05022), a specification language
with a rich history beginning with John McCarthy's
[situation calculus](https://en.wikipedia.org/wiki/Situation_calculus).




Let's break that down:
- 🤖 _action language_ - Flamingo is a DSL for describing the _relationships
between action and change_ in an ultra-compact way, an comes from a long
line of AI research beginning with
[Shakey the robot](https://en.wikipedia.org/wiki/Shakey_the_robot).
- 💻 _for implementing user interfaces_ - Flamingo's is for web apps, and functions 
as a drop-in replacement for state-management solutions like Redux.
- _simplicity_ - In Flamingo, you describe relationships _directly_. There are no
loops, callbacks, or other algorithms.
- _modularity_ 
- ✔️ Correctness - Flamingo's compiler automatically analyzes programs for
consistency. Write declarative constraints, get thousands of tests for free.


## Motivation

_Marcello_: So how is the project coming?

_Emily_: Well, it started out great! The requirements we got from our clients seemed
very clear, and I was able to implement most of them in the first week or two. But
then things started to go down hill... QA found 
