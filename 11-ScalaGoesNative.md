# Scala Goes Native

## The golden cage
* JVM language 
  * Fast, but with lots of "buts"
  * Safe (Maybe to so)
    * Sacrafice expresivitity
  * "Don't talk to strangers" - make talking to native code hard

## Daydreaming - what does he want
* Immediate - no warm-up
* Value Types - not always allocate (stack usage would be nice)
* Better Memory Management - Maybe you know better than the GC. JVM has high cost to "forget" things
* Able to call native code 

## Choices
* LLVM based
* can optimize tail calls
* Same languagte with some low-level primaitives
* Not just a backend - native compiler that both scalac and dotty could go to it
* GC'ed - used Boehm GC
* Hardware support - Developed on 64-bit Intel, but interst in ARM as well as 32-bit
* Library support - c's stdlib bindings are built in, subset of java.*
* Opensourced - https://github.com/scala-native/scala-native
* Not quite ready yet - http://twitter.com/scala_native
