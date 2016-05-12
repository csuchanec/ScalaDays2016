# Metaprogramming 2.0

## What is scala.meta
* Make metaprogramming easy for everyone
* http://scalameta.org/
* officially endorced
* In Beta trying to get to 1.0 (feature complete)
* Supports SBT files

## What can scala.meta do?
* 1.0 
  * Parsing
  * Quasiquotes
  * Tokenization
  * Prettyprinting
* 2.0
  * AST persistence
  * Name resolution
  * Typechecking
  * Implicit inference


## Demo 
* ammonite - repl
* `"foo + bar".parse[Term]` - parse term
* term.structure - print out what the structure is (string rep)
* Pretty printting
  * uses tokens under the hood to maintain the parsed code  
  * term.get.tokens
* parse files including SBT files
* q prefix to a string (quasiquotes) will do the transformation to the term
  * `val q"$x + $y" = q"$foo + $bar" ` will set `x` and `y'


## Summary
* Parsing different dialects
* Type safe 

## Macros
* Bad
  * Hard to write
  * Don't work well with tools
  * Entanged with scalac
* Good
  * enable unique use cases
  * frequently used by libraries
  * most of the complexity is incidental

* New future of macros
  * SIP - Macro published - Inline Definitions and Meta Expresions
  * Two concepts  - `inline` for inlining & `meta` for metaprogramming
  * metaprogramming - compiling code at execution time
  * inline - inline expansion
  * Seperate these things out

# Future

* Codacy
  * code analysis - some of which is built on scala.meta
* scalafmt
  * code formatter - using scala meta
* dotty linker - rewrite rules


