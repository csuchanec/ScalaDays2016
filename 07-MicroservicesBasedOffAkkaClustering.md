# Microservices based off Akka Clustering

* Where do you define API gateway
  * At the akka service
    * Downside is you have to take care of registery and other things
    * Also encurages http communication between services
  * at an API gateway

* Akka Cluster
  * Out of box clustring
  * Loose coupling through typed binary protocol
  * high resiliance

* Distributed endpoints 
  * defined in the microsverice
  * Served by API gateway
  * Play app creates route for those endpoints and routes to the right endpoint
  * Why?
    * Cross cutting logic is kept in api gateway
    * redeploy cross cutting logic without redeploying microservices
    * microservices remain independent
  * Implementation
    * Mimic some of what Play does to begin with
    * Control defines the way the controller works not the actual cotnrol
    * Write happy path, sad path taken care of the cross cutting logic

* Reactive work pipeline
  * Kanaloa (open source project)
  * smart controlled pressure on backend
  * optimal concurrency size exploring - figure out what the optimal number of connections to allow (don't just pick arbitary numbers)
    * Does this thrash ever? could this flip around depending upon what you are trying to do right?

* Metrics Monitor
  * Because of a clear pipeline you can see how thigns are flowing through

* Nodes Monitor - adapted from muuki88


* Make this developer friendly through SBT utils
  * blue-green deployment


* github.com/iheartradio/
  * kanaloa
  * asobu - distributed ednpoints
  * play-swagger - distributed swagger docs


* used 
  * cats
  * shapeless
  * kittens (combine the above two)

* Functional Building Block
  * Used to be is A => B
  * More functional - type K[A,B] = Kleisli[XorT[Future, Reason, ?], A, B]
    * XorT is a Either of success or reason for failure
    * Kleisli is a function wrapping this

  * This gives you functional composition
