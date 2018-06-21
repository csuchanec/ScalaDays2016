# Closing Panel

* Dotty - evolution and time frame
  * Scala 2.12 - how to encode traits and functions were done first in Dotty (taken into Scala 2.12), incubation of features, this pattern will be repeated -> hopefully this converges to a smooth transition
  * for the 2.x line try to get rid of the paper cut type problems to focus on the core of the transition
  * Have some sort of "gofixit" like refactoring tool to help with the transition
  * Avoid the python 3 problem where nobody upgrades

* Scala community member on Scala board
  * Listen to community, collect input, and then present it

* Standard vs Non-Standard let the community do their thing
  * ex: Dates have to use Java Dates
  * Dangerous to gloss over the differences in platforms
  * Would like Scala core library completely portable
  * How portable is it now (in context Scala.js)
    * More than you'd think
    * Lots of JDK is ported to scala.js
    * Things like parallel collections or weak hash maps don't make sense in JS context
    * No runtime reflection in Scala.js because standard library would be 10 MB if you don't do optimizations to use only what you need - just not practical, but maybe a linker plug-in

* Strawman designs for collections
  * Want more
  * Not all the ones that different/going the same direction
  * On going 
  * Most of what being done to collections would be internal and most users will not notice

* 2.13 will be a library release 

* What is the path and pace of deprecating things in the standard library
  * SIP/SLIP should anwer this
  * Not stagnate
  * Introduce deprecation during a cycle? Could reduce the lead time
  





