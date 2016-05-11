# Implicts Inspected and Explained

* http://blog.timmybankers.nl

## Implicits
* What are they?
  * Way to get a value without explicitly referencing it
  * OO has `is a` & `has a`, implicits add `is viewable as a`
  * Loose coupling, tight cohesion

* @implicitNotFound gives nice error message if the implict cannot be found

* Enable
  * DSLs
  * Type evidence
  * Reduce verbosity
  * Type classes
  * DI at compile time
  * Extending libraries

* Beware
  * Resolution rules can be difficult
  * Automatic conversions
  * DO NOT overuse - apply principle of lease power

* Types
  * implicit parameter 
    * `implicit` in front of a parameter
    * `implicity` can find things from the scope
    * Compiled code does not have implicts anymore, compiles down to byte code with getters that get the value
    * If there are two posisble implicits will result in compile time failure
  * Implicit conversions
    * `implicit def` into scope 
    * Look in scope for a method that goes from A -> B to make the function work
    * JavaConverters are preferable to JavaConversions (both are implicits but Converters are doing so with an explicit call but is safer and clearer as to what is happening)
  * Implicit View
    * implicit conversation to project from one type to another
    * Scala allowed View Bounds but now depricated
      * def foo[T <% ImplictViewOfT](x: T) = x.bar
      * New ay of writing this foo(t:T)(implicit )
  * Implicit Classes
    * `implicit class`
    * Make a wrapper class to extend an existing class
    * Used when you don't have control over an existing class but want to add methods to it

## Scoping and Resolving
* Lookup precdence
  1. By name only, without any prefic
  2. In "implicit scope":
    * companion/package object of
      * the source tye
      * its parameters, supertype, and supertraits
* This was a bad explination of this and not terriby useful
* Different scoping that can be used
  * Companion object 
  * Explicit import - import Foo.explicit
  * Wildcard - import Foo._
  * local
  * Parent 


## Typeclasses
* Ad-hoc polymorphism
* Extension of libraries you do not have control over
* Create a type class (trait with what we want available) ex `trait JsonWriter[T] { def toJsonSring(value:T): String}`
* create implicit val of the type of the type class that implements the type class - ex `implicit val StringJsonWriter extends JsonWriter[String] ...`
* Implicit classes can help remove boiler plate here
* Can be generalized more by writing apply methods











* Used an intersting tool to be able to create slides in the repl that can run the code as part of the 


