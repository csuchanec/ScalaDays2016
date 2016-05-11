# Precise Types Bring Performance

* Sources of slowdown
    * Libraries
    * User code

## Libraries
* Scala libraries hide away a lot of complexity but also don't do things in the simplest way
* Scala has a lot of functionality not built into the java hotspot
* The compiler needs to lower what it is doing and doing it in a conservative way
* Comiler lowers generics
* Could clone the funtions but there are
  * 10 types you'd need to do that with
  * so you have 10^n clones inorder for this to work.
  * even worse if it has a function that takes type parameters 10^(n+m)
* `@specialized` as a way of hinting what you care to optimize 
* `@miboxed` 
* both of these things break modularity - because they make assumptions about what end users will be using it (guess if what they need)

* Auto specialziation in the dotty linker - looks at what type argument types are needed both in user code and libraries used by it so that you don't have the exponetnial or library authors guessing


* Type specialization removes boxing
* Term specialization removes virtual dispatch


* Auto Specialziation Limitations
   * Slows down compilation (1.5x slower)
   * Requires dependencies to have tasty
   * does not help if library does tricks
   * if it uses null as a special value
   * has typed API but untyped internals

* Don't try to be smarter than the compiler, hotspot, etc - so the optimizations can be found


## Users code
* Rewrite Rules as a way of improving this



* `x.size == 0` slow versus `x.isEmpty` - compiler should be smart enough to understand this
* User may have written inefficent code for good reason
* Need for library specific optimizations 
* Linker can do this in a generic way, but to get to really good the context of the library needs to re undrestood
* Library defined rewrite rules to do the transformation
* Check if the function is pure to combine rules
* Rewrite rules can be used to write custom warnings and error messages
* Rewrite can do logging to prevent doing
* Not a replacement for macros - but does simpiler things


  | Rewrite Rules | Macros & Inline
 Defined | Anwhere in the program and libraries | Inside implementation
 Applied | Based on analysis | Syntax only
 Influence Typing | No | Yes
 Works with Java methods | Yes | No
 Works across Libraries | Yes | No
 Best For | Simple Declaritive rules | Full-blown metaprogramming


 * Could use macros inside the rewrite rule


* Implemented In - https://github.com/dotty-linker/dotty
* Looking for people to try and see if it meets the normal usage patterns

