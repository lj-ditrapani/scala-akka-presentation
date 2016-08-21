Inventory Application Design using Akka Streams
===============================================


Concurrency
-----------

- Threading
- Akka Actors
- Akka Streams


Threading
---------

- Low level abstractions
- synchronization, atomic vars, thread-safe data structures
- difficult to reason about
- difficult to get right
- deadlocks, race conditions
- misleading
- Bad performance if everything is synchronized & thread safe
- Threads are expensive in memory cost
    - Default java stack size = 512 KB


Actors
------

- high-level abstractions for
    - distribution
    - concurrency and parallelism
- Asynchronous, non-blocking, performant, message-driven model
- Lightweight processes
  - Several million actors per GB of heap memory
- Easier to "get right" than threading, harder to create disasters
- Simple to grasp basic concepts and start building


Using Actors
------------

- Extend Actor, implement receive method
- Receive method branch on message type/content
- Send messages to other actors (tell !)
- Mailbox
- Become/unbecome
- Isolate state
- Guarantee sequential execution of messages


Actor issues
------------

- Boiler plate to achieve stable streaming network of actors
- Implement 2 messages for each method
- OO, not functional
- Not completely type safe
- Network is not verified
- How to bound mail boxes to
  - prevent out-of-memory
  - but also not drop events?


Streams
-------

- Reactive function programming
- Meta language for building actor networks
- Typed input & output
- Focus on what you want to do with each data element
- Streams take care of the "conveyor belts" between nodes
- Both pull & push systems; switches control dynamically
  based on mailbox depths & availability
- Automatic back pressure
- Description and execution are separate


Stream basics
-------------

http://doc.akka.io/docs/akka/2.4/scala/stream/stream-composition.html

- Source: 1 output
- Flow: 1 input, 1 output
- Sink: 1 input
- Components are composable
- Higher level Graph dsl
  - fan in (merge)
  - fan out (balance, broadcast)
  - feeback


Other Akka APIs
---------------

- Http superPool for HTTP client requests (Flow or Future interfaces)
    - Asynchronous IO using java nio select polling
    - HttpRequest & HttpResponse akka models
- Circuit breaker


Benefits of using Akka Streams in Inveroty App
----------------------------------------------

- Performance
    - asynchronous IO
    - parallel streams
    - pipeline stages
    - Processing stages scale better than threads
    - Future: scale out with Akka clusters
- Readability/maintainability
    - Very concise; minimal boilerplate
    - Desired behavior for free
- Reliability/robustness
    - back-pressure
    - typed processing stages
- Get rid of multiple thread pools/execution contexts
- Get rid of low level while loops to pull events off sqs
- Conceptual Synergy with Rx.js on frontend
