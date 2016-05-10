#Pri nciples Of Elegance


1. Public API's minimal
  * Why
    * easier to learn, maintain, understand
    * easier to compose
    * Avoid poluting public API's with types and terms not intended for end-users
    * Users will import with wildcard
    * fewer more general methods (use parameters)
  * How
    * protected/private
    * use typeclasses instead of overloading
    * nest types to hide them

2. Choose Your Names Wisely
  * Why
    * Things need names
    * names communicate something
    * preconceptions are good and bad
  * Naming consideration
    * does it implement a familar concept
    * short names are good for pervasive types/methods
       * huffman encoding idea - more usage 
    * If in doubt favor using long names
    * Especially important forr implicits to avoid accidental shadowing
    * See Haoy Li's Concicesness and Names

3. Embrace the Type System
  * Why
    * Empowers us with constraints
    * types give us sconfidence to reason about the code
    * refactor/maintenaince becomes easier
  * How
    * avoid primative types and Strings 
      * make the type system speak to what you are doing. If that int a length i
    * avoid pure structural types (Option, Either, tuples)
    * Have a low boar for introducing a new type
    * DOn't desing a type so it can represent an illegal/impossible state
    * value classes can provide typesaftey without performance costs
    * macros can enforce additional constraints


4. Design for User experience
  * How
    * Many principles of UX design apply
    * users are all programmers
    * users have different abilities and expectations
    * take advantage of familiar expectations
    * educate where neccessary
    * Keep boilerplate requirements minimal
    * each line should be significant and meaningful
    * casual readers should be able to undersatnd what the code does (names chosen, structure of DSL, etc drive this)
  * Usablity Heuristics
    * Draw parallels with the real world
    * consitency and standards
    * error prevention
    * recognition, not recal
    * fleaxabulity and efficency of use
    * aestethic and  minimalist design
  * Use-site-first design
    * optimize for the use site
    * write some sample code you'd like to compile
    * write code you'd want not to compile
    * then try to write the definitions to make samples compile
    * only compromise when all possibilities in language are exhausted (this could comflict with the principle of least power)


5. Accomidate Learning
  * Why
    *  You should not need to be a library author to use a library
    *  implicits, macros, or type theory should not be a barrier to use
    *  it's acceptale to learn recipes when starting out
  * Scala for Abstraction
    *  Scala is good at hiding details at the use site
    * abstracting for users of our code the dirty details of the code


6. Be Modular
  * What is modularity
    * How easily components can be seperated and combined
    * use typeclasses
  * typeclasses
    * seperate datatypes from their operations
    * extension ethods make the syntax natural
    * implemented in scal with implicits
    * provide more general polymorphism for types
    *  allow retrofitting functionality to types
  * chainging implicits
  ** 

7. Scope and organize your code


8.


## Hurdles and cavates
* Implicits
  * Hard to tell where implicits come from
  * Hard to know where to satisfy the implicit
  * `@implicitNotFound` error meesages can help
  * Better tooling and documentation can 
* Naming conflicts
  * rely on active ecossystem to fix common name classes
* Complex types
  * precise static typing can result in complicated types
  * these get exposed in error messages
* Fix your type errors with this one wierd trick
  1. Work out what types you want to handle
  2. Write a low-priority implicit conversation from a generic source to a generic expected type
  3. implement the implict conversion with a macro
  4. deconstruct the parameter and return types passed to the macro
  5. print a nice error message
  6. make the macro fail everytime (so your code doesn't compile)









