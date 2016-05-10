# Full Stack Scala

* Front end is important

* Things that were being looked at when selecting what to write
  * Need types. This need is implicit in a lot of places even without Scala.js this seems needed
  * Support immutable data - track changes through the stack (who knows what changed where?)
  * Functional Programming ideas
  * Maturity (scala.js is 0.6.9 - but fairly mature)
  * Isomorphism
  * Community


  * Remote Data Challenges
  ** Minimize roundtrips
  ** Minimize data

  ** You can wind up making a lot of calls with REST calls to get the data piece by piece
  ** Sizing problem, what data do you get back 
  ** Falcor - think server data as big JSON and you can select the parts (access as if it is locally) -> future like API, emphasizes caching
  ** GraphQL - Grab what data you want but only as much data as you want 
  ** Rolled their own sort of way of doing this


* Leaning on community
** github.com/payalabs/scalajs-react-bridge - wrote this, some macros to deal with the boilerplate


* MDL - UI library  - material design lite

