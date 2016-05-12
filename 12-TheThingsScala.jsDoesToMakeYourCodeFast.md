# The Things Scala.js Does to make Your Code Fast


* Scala Optimizer - js has an optimizer (why wouldn't you use this?)

* For loop vs While loop over ints
  * Without optimizer - For loop is significantly slower than the while loop
  * With optimizer - both about the same, but for still slower


* For loop vs while loop over longs
  * Longs need a library to represent the operation and the values on longs in javascript
  * Even with optimizer the processesing is factors of 10 slower 
  * Don't use longs in performance critical code


* Array `.map` - JS Array map (native), Scala map, while (manual)
  * Non-optimized is bad, even the native version is slow
  * Optimized version scala version about same as manual but native one doesn't do anything
  * Optimizer is still not optimal - won't do something like fuse two maps into a single while loop


* Concrete methods in traits
  * when you have a concrete method on a trait, JS will create on version of that method for every subclass
  * Does multi-inlining - in front of a polymorphic call and the call is doing the same thing, pick one and inline it

* Closure Elimination
  * call to lambda inside map is mega-morphic and slow, so trying to inline that function and eliminate the closure

* Pattern matching vs object oriented method vs switch
  * Pattern matching - even with optimize still slow
  * More subclasses of abstract class the worse it gets
  * manual switch is still better

