# Quake Common Lisp

Quake Common Lisp is a project to remove [QuakeC](https://en.wikipedia.org/wiki/QuakeC) from Quake 1 and replace it with [ECL](https://ecl.common-lisp.dev/). My hope is that this project will some day become an advanced tool for making serious games. But I'd be okay with it just achieving the Core Goals listed below.

## Overal Plan

At the moment, I plan to use [Quakespasm](https://quakespasm.sourceforge.net/Quakespasm.html) as the foundation for this project, since it appears to be a clean implementation of Quake 1, it has some bug fixes, and it's source code is in the Debian repos. If you have a better suggestion, which doesn't have extraneous features that could get in the way of this project (e.g. more QuakeC features), then let me know.

### Principles
- Avoid writing any new code in C. Ideally, all new code for this project would be written in Common Lisp and:
  - would run in ECL, or
  - would be compiled to C (via ECL) and which would in turn be compiled as a part of the game engine.
- Other than adding ECL to Quake, avoid removing/modifying functionality of the Quake engine itself, unless that would be necessary to improve the ability of developers to make games/mods (e.g. adding hypertext support to the dropdown terminal).

## Goals

### Non-goals
- This project is NOT intended to recreate the original Quake 1 experience. Personally, I am not interested in re-writing QuakeC code in Common Lisp. However, I do plan to use assets from Quake 1 shareware.

### Core Goals
- Can run games/mods written in Common Lisp
- The dropdown terminal presents an ordinary Common Lisp REPL
- The game state/code can be modified at runtime via the dropdown terminal
- A sample level for testing all the monsters, items/weapons, and level features
- Use [cl-isolated](https://github.com/kanru/cl-isolated) to provide some basic protections for the user (e.g. prevent the REPL and games/mods from being able to read/write random files).

### Long-term Goals
- A proper Lisp IDE inside the dropdown terminal, so that the programmer can write/organize code without exiting Quake.
  - A code editor which supports Emacs, Vi, and CUA keybinds
- Hypertext/[CLIM](https://www.cliki.net/CLIM)-like features in the dropdown terminal, such as:
  - hyperlinks (e.g. for documentation)
  - interactive elements (buttons, sliders, etc)
  - vector drawings, images, and possibly 3D elements
  - a CLIM/[Genera](https://en.wikipedia.org/wiki/Open_Genera)-like Command Processor for the dropdown terminal
- A hypertext documentation system, similar in spirit to Genera's [Concordia](http://www.bitsavers.org/pdf/symbolics/software/genera_8/User_s_Guide_to_Symbolics_Concordia_Book_Design.pdf), though obviously not oriented to making books. Developers would use this system to read the [Hyperspec](http://www.lispworks.com/documentation/HyperSpec/Front/index.htm), documentation for Quake Comon Lisp, and any available documentation for the currently-loaded game/mod -- all from the comfort of the dropdown terminal.
- A texture editor, which works inside the game engine
- A 3D model editor, which works inside the game engine (I don't yet have any ideas on how to implement this.)
- A map editor, which works inside the game engine (BSP compilers are fast on modern machines, so this might be feasible.)
- Security sandboxing via a portable environments project that I'm working on separately
  - The dropdown terminal would let you run code outside the sandbox, but it would still have some simple protections (e.g. cl-isolated).
  - The code that controls the state of the game would be sandboxed.
- Two advanced AIs for the game monsters (or NPCs):
  - An AI which allows each type of monster to learn across game sessions (e.g. the Shamblers would learn separately from the Grunts, but individual Grunts and Shamblers would behave indepentently).
  - An AI that controls all the monsters in the game session, such that it coordinates the monsters to fight the player. This woudl be similar to a DM/GM in pen-and-paper RPGs.
- A single-player campaign to show off the features of Quake Common Lisp
- Multiplayer (no ideas on this yet)
- Game state files and level files are identical (i.e. they are Lisp files that contain a snapshot of the game state). This enables, for instance, having a level begin with a monster attacking the player.
- The ability to run the game state backwards, in order to more easily test code (not sure how to implement this, but it would probably involve [Screamer](https://nikodemus.github.io/screamer/))
- Port this idea to other open-source game engines (e.g. Quake 2, Quake 3)
- Replace ECL with a faster Common Lisp implementation (e.g. re-write parts of Quake so that it is compiled into a library that can be loaded by SBCL via FFI.)
