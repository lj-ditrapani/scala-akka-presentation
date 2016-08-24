Inventory Application Design using Akka Streams
===============================================


Concurrency
-----------

- Threading
- Akka Actors
- Akka Streams
- Akka Http


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
    - distributed
    - concurrent and parallel
- Erlang
- Akka 2009, replaced scala std lib actors
- Erlang on JVM
- Erlang with a typed language
- Message passing
  - Asynchronous
  - non-blocking
- Lightweight processes
  - Several million actors per GB of heap memory
- Easier to "get right" than threading, harder to create disasters
- Simple to grasp basic concepts and start building


Using Actors
------------

- Extend Actor
- Implement receive method
- Branch on message type/content
- Send messages to other actors
- Mailbox
- Isolate state
- Guarantee sequential execution of messages
- Java API & Scala API


Actor issues
------------

- Boiler plate to achieve stable streaming network of actors
- OO, not functional
- Not completely type safe
- Network is not verified
- Unbounded mail boxes
  - prevent out-of-memory?
  - but also not drop events?


Streams
-------

- Reactive functional programming
- Meta language for building actor networks
- Components
  - Source: 1 output
  - Flow: 1 input, 1 output
  - Sink: 1 input
- Typed input & output
- Focus on what you want to do with each data element
- Streams take care of the "conveyor belts" between nodes
- Both pull & push systems; switches control dynamically
  based on mailbox depths & availability
- Automatic back pressure
- Description and execution are separate


Stream basics
-------------

- Components are composable
- Higher level Graph dsl
  - fan in (merge)
  - fan out (balance, broadcast)
  - feeback


Akka Http
---------


Other Akka APIs
---------------

- Http superPool for HTTP client requests (Flow or Future interfaces)
    - Asynchronous IO using java nio select polling
    - HttpRequest & HttpResponse akka models
- Circuit breaker


Benefits of using Akka Streams in Inventory App
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
