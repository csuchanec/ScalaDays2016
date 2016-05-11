# Key Note - Spark 2.0

* What is Spark? - genreal processing engine for clusters (basically Map Reduce with different primatves for data sharing)

## Original Spark Vison
* Unify engine for big data processing
* Concise language-integrated API

* Motivation
  * Unification 
    * MapReduce - general batch processing
    * Specialized systems for new workloads - lots of other techs built
    * Hard to manage, tune, deploy
    * Hard to compose in pipeline
  * Concise API
    * Much data analysis is exploratyr or interactive
    * Spark solution -  Resilient distributed datasets (RDDs)

## How did the vision hold up
* Generally well
* Users appreciate unification
* functional API cause some challenges
* Multiple components for differnt datatypes built under the same API
* Most users use more than one component
* Wide range of uses
* Functional API
  * Hides away many semantics of computation
    * Functions blocks of Java bytecode
    * Data stored in arbitary Java objects
  * Users can mix api in sub-optimal ways
  * groupByKey is causes the most tickets (as an example)
    * Grouping materializes the item and this is not being optimized/cannot be optimized
  * Java objects are often many times larger than underlying fields
    * Lots of space wasted with overhead that adds up when working at the scale of Spark

# Structured APIs - Dataframes and Datasets
* Implemented on top of the RDDs
* Why Structure
  * Limit what can be expressed
  * In practice accomidate the majority of computations
  * Limiting the space can be exprssed endables optimizations

* Language integrated API's for structured data - build on Spark SQL
* DataFrames - dynamically typed
* Datasets - statically typed
* Execution Steps
  * Structure -> Logical plan -(Optimizer - combine the catalog info)-> physical plan - (code generator) -> RDDs (go to the Data Source API)
* DataFrame API
  * Hold rows with a known schema and offer relational operations on them through a DSL
  * Has an expression AST to express things like filters
  * Has standard operations like count, groupby, avg etc
  * Can always go back to a Scala API if you don't want to/can't use the DSL to express what you want
  * Dataframe concept in R, Python is popular
    * Spark is the first to make this declarative
    * This gives a chance to do optimizations - in Pandas for example these are done eagerly
  * Integrates well with other data science libraries
    * MLlib takes DataFrames as input/output
    * Python/R can map to own types

* What do structured APIs Enable
  * Compact binary representation
    * Columnar, compresssed format for caching, rows for processing(but this probably will change)
  * Optimization across operators (join ordering, push down)
  * Runtime code generation (which enables optimization by preventing things like generics and virtcual calls)

  * Performance
    * Improvement from straight RDDs
    * Equal across all languages

* Dataset API
  * Try to get the performance of DataFrame with type safety
  * Built using case classes
  * dataframe.as[T] to map to case class
  * can then use them as "normal" scala code
  * Can go back to the less safe DataFrame operation
  * Uses implicit encoder object for each type T to map Scala objects to SQL rows
  * Dataset methods take either closures or expression in the same DSL as DataFrames
  * Future work - infer semanctics of user Closures (using Scala macros)
  * Using DSL gives slightly better performance (for now)

* Long-Term
  * RDD will remain low-level API in Spark
  * Datasets & DataFrames give richer semantics and optimizations
    * New libraries will increasingly use these as interchange format

## Optimizing Structured APIs
* Data Sources
  * Common way for datasets and Dataframes to access storage
    * Apps can migrate across different datasources (Hive, Cassandra, JSON, Avro, etc)
    * Structured semantics allows query pushdown into datasources, something not possible in the original spark

  * Different interfaces based on what underlying source provides
    * Tablescan - just read all rows - JSON
    * Pruned Scan - read specific coluns - Casandra
    * Filtered scan - read rows based on a filter - SQL


* Hardware trends
  * Want to do optimize CPU and memory usage
  * This was because back in 2010 the operations tended to be IO bounded (storage and network)
  * Now lots of data on SSDs, networks faster, but CPU's are not really any faster
  * Back in the day it used to be avoid I/O but now need to be efficent CPU to really get performance

* Project Tungsten
  * Runtime code generation
    * Generate Javacode then compile it
    * Using low level JVM things like Platform.getInt() - JVM intrinsic JIT-ed to pointer arithmatic
      * data has a well defined lifecycle so the data is easy to manage outside the heap 
  * Exploiting cache locality
  * Off-heap memory
      * Tungsten's compact encoding (Binary format)
        * Good for structured data 
        * This leads to better space effiency
  * Long-Term Vision
    * Works in JVM but to build different Tungsten backend, particularly to places where a JVM won't run well

## Next Steps in Spark 2.0
* Come out around end of May
* Major changes means possible breaking APIs
  * Really hate breaking APIs
  * Will not do so except for dependency conflicts (e.g. Guava)

* Major Features
  * Tungsten Phae 2
  * Machine learning model export
  * Structured streaming - real-time engine on SQL/Dataframes
    * Real-time procssing is increalingly important
    * most apps need to combine it with batch & interactive queries
      * track state using a stream, then run SQL queries
      * train an ML model offline, then update it
    * High-level streaming API built on DataFrames/Dataset
      * Event time, windowing, sessions, sources & sinks
      * Optimizations via tungsten
      * Also supports interactive and batch quering
      * Calling this conintious applications
    * API
      * Simplest way to do streaming analytics is not having to reason about streaming
      * Describe the final result not how to do it 
      * Streams as infinte DataFrames (use the same Single API)
        * Do the operation incrementally
    * Execution
      * Logically - dataframe operations on static data
      * Physically - spark automatically does the transformation
        * Incrementalized by Spark from Batch to continuous
      * Not all things can be done incrementally, you will be told when that is the case
## Conclusion
* High performance data processing increasingly requires low-level CPU and memory optimizations
* Spark implements these in Scal through simple, type-safe DSLs
* Future language versions may make it even easier

*Learn Apache Spark
  * databricks.com/ce








