# cppfront

A personal experimental C++ Syntax 2 -> Syntax 1 transpiler

Copyright (c) Herb Sutter

See [License](LICENSE)

[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](code_of_conduct.md)

# What is this project?

This a personal project for my own use and experimentation, to learn some things, proof out some concepts, and share some ideas. As parts may work out, I'll continue to bring those results to ISO C++ as proposals: I did most of this design work in 2015-16, and since then every evolution proposal paper I've brought to ISO C++, and every conference talk I've given, has come from this work and just been presented as a standalone proposal under today's syntax, to help validate and refine that part of the design.

I'm sharing this work because I hope to start a conversation about what could be possible _**within C++**_’s own evolution to rejuvenate C++. It's currently still hilariously incomplete (e.g., as of this writing, there's no support for classes!). Don't contemplate any real use yet. :)

This is one of many experiments going on across the industry looking at ways to accomplish a major C++ evolution. What makes this experiment different from the others? Two main things...

## 1) This is about C++, not about something else

<image align="right" width="150" src="https://user-images.githubusercontent.com/1801526/188887745-23e0c3a0-3ea7-4589-993c-f54fe662b107.png"> I love ISO C++. It's the best tool in the world today for me to write the programs I want and need.
    
**I want to keep writing code in C++... just "nicer":**
    
- with less ceremony to remember;

- with fewer safety gotchas; and

- with the same level of tool support other languages enjoy.

Know what I mean? I want "C++, the powerful and expressive parts" without "C++, the cumbersome and dangerous parts." That C++ is a fun language. I want that.
    
We've already been improving C++'s safety and ergonomics with every ISO C++ release, but they have been "10%" improvements. We haven't been able to do a **"10x"** improvement primarily because we have to keep 100% syntax backward compatibility.

What if we could have our compatibility cake, and eat it too — by having:

- 100% seamless **link compatibility always** (no marshaling, no thunks, no wrappers, no generated 'compatibility modules' to import/export C++ code from/to a different world); and
    
- 100% seamless **backward source compatibility always available**, including 100% SFINAE and macro compatibility, **but only pay for it when we use it**... that is, apply C++'s familiar "zero-overhead principle" also to backward source compatibilty?

I want to encourage us to look for ways to push the boundaries to bring C++ itself forward and double down on C++ — not to switch to something else.
    
I want us to aim for major C++ evolution directed toward things that will make us better C++ programmers — not programmers of something else.

    
## 2) This is about a specific goal
    
<image align="right" width="320" src="https://user-images.githubusercontent.com/1801526/188898468-17e5ce70-d417-48d6-b204-ad9e4caa30ed.png"> My specific goal is to explore the question: Can we make C++ **10x safer, simpler, and more toolable** if we had a "syntax #2" alternative syntax for C++, within which we are completely free to improve **semantics** free of any backward source compatibility restrictions?
    
An alternative syntax would be a cleanly demarcated "bubble of new code" that would let us do things that we can never do in today's syntax without breaking the world, such as to:

- fix defaults (e.g., make `[[nodiscard]]` the default);
- double down on modern C++ (e.g., make C++20 modules and C++23 `import std;` the default);
- remove unsafe parts that are already superseded (e.g., no unsafe `union` or pointer arithmetic);
- have type and memory safety by default (e.g., make the [C++ Core Guidelines safety profiles](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#S-profile) the default and required);
- eliminate 90% of the guidance we have to teach about today's complex language (e.g., by eliminating special cases, and refactoring the language into a smaller number of regular composable features); and
- make it easy to write a parser (e.g., having a context-free grammar and order-independent semantics).
   
This repo is an experiment to try to develop a proof of concept that evolution along these lines may be possible. For example, this repo's `parse.h` is a standalone context-free parser that is growing month by month as I implement more of the "syntax #2" experiment.

> **Important disclaimer: Please do not make the mistake of focusing on syntax, or thinking 'Herb wants to make syntax pretty.' That is _so_ not the point.** The syntax is not the important thing — yes, we should make it clean too, and yes, it's the most visible thing. **The important thing is the semantics** — the syntax is just the gateway into a new open space where can (finally) fix the semantics. If this project were just about 'making the syntax prettier' it would be a total waste of time. I'm not interested in wasting my time on 'just lipstick,' I want to solve semantic problems so I can write C++ code more safely and conveniently myself on my own future projects.

# How do I build cppfront?

<image align="right" width="120" src="https://user-images.githubusercontent.com/1801526/188906112-ef377a79-b6a9-4a30-b318-10b51d8ea934.png">
Cppfront builds with any major C++20 compiler.

MSVC build instructions:

    cl cppfront.cpp -std:c++20 -EHsc

GCC build instructions:

    g++-10 cppfront.cpp -std=c++20 
    
Clang build instructions:

    clang++-12 cppfront.cpp -std=c++20

That's it. There are no outside dependencies (no YACC/Bison/...), no build scripts (no CMake/Bazel/...). I started cppfront with just a blank editor and the C++ standard library, and have stuck to that so far. The parser is custom hand-written code, so is everything else, and all the code in this repo is my own (including a small function that is also in the Microsoft GSL implementation because I contributed it there too).

# How do I build my `.cpp2` file?

Just run

    cppfront your.cpp2

then run it through any major C++20 compiler after putting `/cppfront/include` in the path so it can find `cpp2util.h`.

MSVC would be:

    cl your.cpp -std:c++20 -EHsc

GCC would be:

    g++-10 your.cpp -std=c++20 
    
Clang would be:

    clang++-12 you.cpp -std=c++20

That's it. 


# Where's the documentation?

For now I'm not posting a lot of written documentation because that would imply this project is intended for others to use — if it someday becomes ready for that, I'll post more docs.

Here's where to find out more about my 'syntax #2' experiment:

- **My CppCon 2022 talk** [link coming soon] — this is the primary documentation right now.
- The [cppfront regression tests](https://github.com/hsutter/cppfront/tree/main/regression-tests/test-results) which show dozens of `.cpp2` files and the `.cpp` file each one is translated to. Each filename briefly describes the language features the test demonstrates (e.g., contracts, parameter passing, bounds safety, `is` queries and `as` casts, generalized value capture including in "lambdas" and string interpolation).

I'll add a few overview examples here soon...
