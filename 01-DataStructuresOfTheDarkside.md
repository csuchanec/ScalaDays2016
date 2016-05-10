
#Data Structures Of The Darkside 

## Zippers
* Data scturcture with focus and direction
* regular datastructure witha cursor
* `case class StreamZipper[+A](lefts: Stream[A], focus:A, rights:Stream[A])`
  * Left side should be reverse stream
* Map is the simple case and transitively just makes sense, but flatmap is costly and something that generally shouldn't be done because it is expensive
* Fold -> Catamorphism (math term) - cat go down
* Good fold detection - (hueristic) if pass all possible constructors to the fold method you should get the original object you started with
* Anamorphisms (unfolds) - ana go up
* Unfold - paths of workspaces example (is there something to use in how we think about creating our graph?)
* Stream vs List because the StreamZipper[StreamZipper[A]] which provides a zipper with a cursor pointing to all the cursors. List would evaluate this, but Streams don't
* Comonad - in context of a Zipper
  * `extract` - focus item
  * `coflatMap` - `positions map f`
*`mapWith[B]` - General way to think about it is List[A] -> List[(A,B)] - idea to carry the context forward with the map
* monad based on a flatMap, comonad starts with a context and element and allows you to annotate it


## DList
* Difference List
* Useful in context of a writer Monad
* Constant complexity for append and concatenation
* Function of List -> List (compose the functions -- append in it) (naive approach)
* Stack Overflow can be a problem here
* solve this with a Tranpoline - trade stack space for heap space
* Really is function of List[A]->Trampoline[List[A]]



