# Designing Data Intensive Applications - Notes

- [Designing Data Intensive Applications - Notes](#designing-data-intensive-applications---notes)
  - [Designing Data Intensive Applications - Chapters 1 through 3](#designing-data-intensive-applications---chapters-1-through-3)
  - [Chapter 1 - Reliabilitiy Scalability Maintability](#chapter-1---reliabilitiy-scalability-maintability)
  - [CHAPTER 2 - DATA MODELS AND QUERY LANGUAGES](#chapter-2---data-models-and-query-languages)
  - [Chapter 3 - Storing and Retrieving Data (Reads and Writes)](#chapter-3---storing-and-retrieving-data-reads-and-writes)
    - [Transaction Processing vs. Analytics](#transaction-processing-vs-analytics)
  - [Chapter 4 Encoding and Evolution](#chapter-4-encoding-and-evolution)
      - [Formats for Encoding Data](#formats-for-encoding-data)
      - [Language Specific Formats](#language-specific-formats)
    - [JSON, XML, and Binary Variants](#json-xml-and-binary-variants)
      - [Binary Encoding](#binary-encoding)
      - [Thrift and Protocol Buffers](#thrift-and-protocol-buffers)
      - [Avro](#avro)
    - [Dataflow -\> HTTPS / RPC / …](#dataflow---https--rpc--)
      - [Dataflow Through Databases](#dataflow-through-databases)
      - [Dataflow Through Services (REST / RPC)](#dataflow-through-services-rest--rpc)
      - [Web Services](#web-services)
      - [Remote Procedure Calls](#remote-procedure-calls)
      - [Message Queues](#message-queues)
      - [Distributed Actor Frameworks](#distributed-actor-frameworks)
  - [Chapter 5 Replication](#chapter-5-replication)
    - [Replication](#replication)
      - [Leaders and Followers](#leaders-and-followers)
      - [Synchronous vs. Asynchronous](#synchronous-vs-asynchronous)
      - [Adding New Followers](#adding-new-followers)
      - [Node Outages](#node-outages)
      - [Implementing Replication Logs](#implementing-replication-logs)
      - [Problem with Replication Lag](#problem-with-replication-lag)
      - [Reading own Writes](#reading-own-writes)
      - [Monotonic Reads](#monotonic-reads)
      - [Consistent Prefix Reads](#consistent-prefix-reads)
      - [Multi-Leader Replication](#multi-leader-replication)
      - [Handling Write Conflicts - Data Racing](#handling-write-conflicts---data-racing)
      - [Multi-Leader Replication Topologies](#multi-leader-replication-topologies)
      - [Leaderless Replication](#leaderless-replication)
      - [Quorums and Consistency](#quorums-and-consistency)
  - [Chapter 6 - Sharding](#chapter-6---sharding)
    - [Sharding / Partitioning](#sharding--partitioning)
      - [Key Range Partition](#key-range-partition)
      - [Partition by Hash](#partition-by-hash)
      - [Skewed Workloads and Relieving Hot Spots](#skewed-workloads-and-relieving-hot-spots)
      - [Secondary Indexes](#secondary-indexes)
      - [Rebalancing Partitions](#rebalancing-partitions)
  - [Designing Data Intensive Applications - Chapter 7 Transactions](#designing-data-intensive-applications---chapter-7-transactions)
    - [Slippery Concept of a Transaction](#slippery-concept-of-a-transaction)
      - [Atomicity](#atomicity)
    - [Consistency](#consistency)
    - [Isolation](#isolation)
      - [Durability](#durability)
    - [Single-Object and Multi-Object Operations](#single-object-and-multi-object-operations)
    - [Handling Errors and Aborts](#handling-errors-and-aborts)
    - [Weak Isolation Levels](#weak-isolation-levels)
    - [Read Committed](#read-committed)
        - [Implementing Read Committed](#implementing-read-committed)
      - [Snapshot Isolation and Repeatable Read](#snapshot-isolation-and-repeatable-read)
      - [Implementation](#implementation)
      - [Visibility rules for observing a consistent snapshot](#visibility-rules-for-observing-a-consistent-snapshot)
      - [Indexes and snapshot Isolation](#indexes-and-snapshot-isolation)
    - [Repeatable Read and Naming Confusion](#repeatable-read-and-naming-confusion)
      - [Preventing Lost Updates](#preventing-lost-updates)
      - [Atomic write operations](#atomic-write-operations)
      - [Explicit Locking](#explicit-locking)
    - [automatically detecting lost updates](#automatically-detecting-lost-updates)
      - [Compare and Set](#compare-and-set)
    - [Conflict Resolution and Replication](#conflict-resolution-and-replication)
    - [Write Skew and Phantoms](#write-skew-and-phantoms)
    - [Characterizing a write skew](#characterizing-a-write-skew)
    - [More examples of Write Skew](#more-examples-of-write-skew)
    - [Serializability](#serializability)
    - [Actual Serial Execution](#actual-serial-execution)
      - [Encapsulating transactions in stored procedures](#encapsulating-transactions-in-stored-procedures)
      - [Partitioning](#partitioning)
    - [Two-Phase Locking (2PL)](#two-phase-locking-2pl)
      - [Implementation](#implementation-1)
      - [Performance of Two Phase Locking](#performance-of-two-phase-locking)
      - [Predicate Locks](#predicate-locks)
      - [Index-range locks](#index-range-locks)
      - [Serializable Snapshot Isolation (SSI)](#serializable-snapshot-isolation-ssi)
      - [Pessimisitc versus optimisic concurrency ocntorl](#pessimisitc-versus-optimisic-concurrency-ocntorl)
      - [Decisions based on an outdated premise](#decisions-based-on-an-outdated-premise)
      - [Detecting stale MVCC reads](#detecting-stale-mvcc-reads)
      - [Detecting writes that affect prior reads](#detecting-writes-that-affect-prior-reads)
      - [Performance of serializable snapshot isolation](#performance-of-serializable-snapshot-isolation)
  - [Chapter 8 - Trouble With Distributed Systems](#chapter-8---trouble-with-distributed-systems)
    - [Faults and Partial Failures](#faults-and-partial-failures)
      - [Cloud Computing and Super computing](#cloud-computing-and-super-computing)
      - [Unreliable Networks](#unreliable-networks)
      - [Network Faults in Practice](#network-faults-in-practice)
      - [Detecting faults](#detecting-faults)
      - [Timeouts and Unbounded Delays](#timeouts-and-unbounded-delays)
      - [Network Congestion and queueing](#network-congestion-and-queueing)
      - [Synchronous Versus Asynchronous Networks](#synchronous-versus-asynchronous-networks)
      - [Can we not make network delays predictable](#can-we-not-make-network-delays-predictable)
    - [Unreliable Clocks](#unreliable-clocks)
      - [Monotonic Versus Time-of-Day Clocks](#monotonic-versus-time-of-day-clocks)
      - [Clock Synchronization and Accuracy](#clock-synchronization-and-accuracy)
      - [Relying on Synchronized Clocks](#relying-on-synchronized-clocks)
      - [Timestamps for ordering events](#timestamps-for-ordering-events)
      - [Clock Readings have confidence interval](#clock-readings-have-confidence-interval)
      - [Synchronized clocks for global snapshots](#synchronized-clocks-for-global-snapshots)
      - [Process Pauses](#process-pauses)
      - [Response time guarantees](#response-time-guarantees)
      - [Knowledge, Truth, Lies](#knowledge-truth-lies)
      - [Truth Is Defined by the Majority](#truth-is-defined-by-the-majority)
      - [Leader and the lock](#leader-and-the-lock)
      - [Fencing Tokens](#fencing-tokens)
      - [Byzantine Faults](#byzantine-faults)
  - [chapter-9-consistency-and-consensus/](#chapter-9-consistency-and-consensus)
  - [chapter-10-batch-processes/](#chapter-10-batch-processes)
  - [Chapter 11 - Stream Processing](#chapter-11---stream-processing)
    - [Transmitting Event Streams](#transmitting-event-streams)
    - [Messaging Systems](#messaging-systems)
      - [Direct Messaging from producers to consumers](#direct-messaging-from-producers-to-consumers)
    - [Message Brokers](#message-brokers)
    - [Databases and Streams](#databases-and-streams)
      - [Keeping Systems in Sync](#keeping-systems-in-sync)
      - [Change Data Capture](#change-data-capture)
      - [Implementing Change Data Capture](#implementing-change-data-capture)
      - [Initial Snapshot](#initial-snapshot)
      - [Log Compaction](#log-compaction)
      - [API Support for change streams](#api-support-for-change-streams)
    - [Event Sourcing](#event-sourcing)
      - [Deriving current state from the event log](#deriving-current-state-from-the-event-log)
      - [Commands and Events](#commands-and-events)
      - [State, Streams and Immutability](#state-streams-and-immutability)
      - [Deriving several views from same event log](#deriving-several-views-from-same-event-log)
      - [Concurrency control](#concurrency-control)
      - [Limitations of immutability](#limitations-of-immutability)
    - [Processing Streams](#processing-streams)
    - [Uses of Stream Processing](#uses-of-stream-processing)
      - [Complex event processing](#complex-event-processing)
      - [Stream analytics](#stream-analytics)
      - [Maintaining Materialized Views](#maintaining-materialized-views)
      - [Search on Streams](#search-on-streams)
      - [Message Passing and RPC](#message-passing-and-rpc)
  - [Reasoning About Time](#reasoning-about-time)
      - [Event Time vs. Processing Time](#event-time-vs-processing-time)
      - [Knowing when your ready](#knowing-when-your-ready)
      - [Whose clock to use?](#whose-clock-to-use)
    - [Types of Windows](#types-of-windows)
      - [Stream Joins](#stream-joins)
      - [Stream-Stream join (window join)](#stream-stream-join-window-join)
      - [Stream-table join(stream enrichment)](#stream-table-joinstream-enrichment)
      - [Table table join (materialized view maintenance)](#table-table-join-materialized-view-maintenance)
  - [chapter-12-future-of-data-systems/](#chapter-12-future-of-data-systems)

## Designing Data Intensive Applications - Chapters 1 through 3

[My Notes](https://raymondjones.dev/en/system-design-notes/)

Data Intensive Application Data as primary challenge Quantity of Data / Complexity of Data / Speed of Data

Lots of Buzzowords like AWS / NOSQL / etc. Choosing from these means understanding tradeoffs Book details how to navigate and select from all these options

---

## Chapter 1 - Reliabilitiy Scalability Maintability

Databases / Caches / Search Index / Stream processing / Batch Processsing SP is filtering data by key words Batch Processing is crunching large amounts of data

These can all be considered Data Systems and they can interact with each other to help a overall application

Reliability User errors or Mistakes are handled Performs as user expects Performance meets required case Prevents unauthorized access Functional / Non-Functional Requirements\*

Hardware Errors Problems with hardware can arise, in sources that want to be highly avaiable RAID / Redudancy is added. But this increases rates of hardware failure Common for AWS to be down Software Errors Cause bigger system errors than hardware errors No real solution, although testing, process isolation, and crash/restart can help Measuring / Monitoring / Analyizing system behavior in production Test at all levels -> Unit / Integration / Manual / Regression Roll back capabilities Generally very important to reduce loss of money (Or catatrophic nuclear failure) Can cut corners but need to be conscious of risks SCALABILITY What will the service look like in the future? What happens if data expands? How is it handled?

Discover what current load is, then look for ways to optimize\* Twitter example with updating timeline tweets at WRITE vs. VIEW

Once load is found, examine what happens when it increases (Measure Throughput or time)

latency vs. response time (time until request finishes vs. time until user sees change) Median is better than average for estimating time data Percentiles can also tell a story -> higher percentile (tail latency) usually serve bigger data Service Level Objectives (SLOs) and Service Level Aggrements (Contracts the define expected performance) Queueing delays and waiting for 1 slow application request can stall everything else

How to improve architecture scalability Usually have to redesign it as it scales (Load 1 design does not work for Load 10 design) Vertical scaling vs. Horizontal Scaling (shared-nothing / scaling out) Elastic systems for unpredictable traffic There is no magic key, need to evaluate types of distributed systems MAINTAINABILITY People dislike working with legacy software, but it’s important to reduce pain Operability / Simplicity / Evolvability

Operability involves making life easier for operators (People who monitor / keep software up to date) Data systems that have good visibility for this is preferred Good Documentation / default behavior / Avoid dependency on 1 machine(!!!) Simplicity OOP / consistent naming / Avoiding tangled dependencies

---

## CHAPTER 2 - DATA MODELS AND QUERY LANGUAGES

Data models are important part of applications Very difficult to master the intricacies of one data model (There’s 20+ books on relational modeling) This chapter will go over Relational / Document / some graph based models

RELATIONAL VS. DOCUMENT MODEL SQL as most popular relational DB model Developed in 1970s and was overall best among competitors, also has good general use cases NOSQL rose to reduce difficulties from SQL Scalability, simpler to code than SQL, specialized query operations, Open Source Likely that NOSQL co-exist with SQL Object-Relational Mismatch (Tables don’t map to objects, code needs to be made for this) JSON representations don’t have this problem (However, it still has other issues) IDs. vs Strings (IDs are useful because they remain consistent / avoid ambiguity, human language changes)

    Many to One vs. One to Many
    	Using Joins on JSON is hard, maybe can reference objects instead of strings

DOCUMENT MODEL In 1970s, IBM’s IMS was a hierarchical / tree model that had many similarities with JSON Eventually faded away when SQL grew Network MODEL / CODASYL -> Struggled if the path for data wasn’t known Relational DB was another solution -> Allows data without lookups / paths… Query optimizations

Code Complexity Document good at One to Many (Lack of joins means Many to Many is difficult)

Schema Flexibility No schema enforced means any document can contain anything Documents have a schema-on-read, relational has schema-on-write that’s enforced What if an application wants to change the format of data? Document needs to write new documents with new fields Relational has to use ALTER query

    Documents are great if data stored can have different fields, Schema-enforced relational DB would be hard here

Data Locality All the data is loaded at once (Faster if all data is being used) Convergence of Document / Relational XML is allowing querying / indexing…. PostgreSQL is allowing JSON support.. Others soon to follow?

QUERY LANGUAGES Imperative -> most common Declarative programming offers super fast code by telling computer what type of data to get Map Reduce Querying -> hybrid (MONGODB)

GRAPH-LIKE MODELS Document good for ONE-to-MANY or No-relationships… Relational good for many-to-many When the many-to-many is too big -> Use graphs Social Network // Web graph // Rail / road network

Property Graph Model (Neo4j, Titan, InfiniteGraph) Vertex has ID / outgoing edges / incoming edges / properties (key-val pairs) Edge has ID / head(ends) / tail vertex (where edge starts) / label for relationship / properties

No restrictions for vertex connections // Can easily find incoming + outgoing edges for a vertex // Labels for relationships can store info on graph Has good evolvability due to flexible nature

Cypher query language for graphs

Triple-Store Model

**SUMMMARY** Brief overview of the big field data models Unmentioned Models -> Genome data // Particle physics // Full - Text Search

## Chapter 3 - Storing and Retrieving Data (Reads and Writes)

Simple method is to append to end of file. And search entire file when reading (slow)

Hash Index Mapping data at offsets so you can skip more of the file k1 -> offset 1, key2 -> offset 64 (better than searching entire file)

    These files can be segmented to allow new files to be created when space runs out
    	Compaction (Throwing away duplicate keys in log)
    Details of implmentation
    	Store using byte file
    	Append special char to bytes that need to be deleted
    	Crash recovery
    		Store snapshots that can be reloaded
    		Partially written records deleted
    		Writer locks file
    Benefits -> Appending is fast, crash recovery is simple
    	removing old segments removes need of fragmentation
    Limitations -> hash-table must fit in memory
    	Range queries are difficult / slowish

SSTables and LSM-Trees Sorted String Table (SSTables) Instead of appending to end, keep in sorted order (Allows faster searching) How to maintain sorted order? B - Trees work. In-Memory works too using a tree structure like Red-Black / AVL 1. Insert in sorted order 2. Check if memtree is bigger than some capacity…Make new one if it is 3. on Read, search memtable, then check disk-segment, and older segments 4. Occasionally run merge / compaction in background to delete files/overwrite values Handling Crashing Memtable is lost if it crashes…Prevent loss by append every memtable write to a stack

    LSM - Trees
    	Process above is used in LevelDB and RocksDB
    	Indexing structure called Log-Structured Merge-Tree
    	Seem to be exact same as SSTables
    	Optimizing -> Misses are expensive
    		Fix this by using Bloom Filter(Approximates set contents)
    	Strategies for compacting/merging
    		Size-Tiered / Leveled Compaction. HBase(level)/Cassandra(does both)
    		Newer / smaller SStables are merged into older/larger tables (Size-tiered)
    		Key range is split into smaller SSTables and older data moved into levels
    	LSM keep a cascade of SSTables that are merged in background.
    	Simple and Effective

B-Tree One of most common index References point to other References in a range of numbers Uses fixed blocks / Pages (4KB usually)

    	During update -> Search ranges for the key
    	During insert -> Search ranges until at the end, and add it (If size too big, split list in half)
    		Then update parent
    Can watch a youtube video to learn more

LSM-Tree vs. B-Tree LSM has less writes. B-Trees need to write at least twice (Once for WAL log in case of crash, Once on tree) Some storage engines write same page twice to prevent power outage partial write LSM rewrite during compaction / merging phase (Write amplification) Write heavy application will notice the difference LSM is compressed better, yielding smaller files on disk

    ---
    BAD of LSM
    ---
    Compaction can be expensive
    Disk bandwidth expands bigger database gets
    Compaction could possibly not keep up with the write requests

    B-Trees provide consistently good performance. Each key exists in one place wheras LSM might have multiple copies
    Transaction isolation can be done by locking ranges

OTHER STRUCTURES Primary key -> Uniquly identifies a row in SQL/relational Secondary index -> Important for joining data Heap file -> stores rows for indexing… Avoids duplicating data when multiple secondary indexes present Index referes to location Multiple Columns What if you want a key to have multiple values? Concatenated index -> rule is set to append X columsn when key/index is found Multiple-dimensional like below can’t be done in a B-Tree / LSM

    	SELECT * FROM restaurants WHERE latitude > 51.4946 AND latitude < 51.5079
    		AND longitude > -0.1162 AND longitude < -0.1004;

Ful-text-search / fuzzy indexes

In Memory Databases Don’t need to write to a hard disk, everything in memory Can use data models that are complicated to use with a hard disk

    Anti-caching approach, a type of virtual memory can be used by evictng LRU cache and putting in disk

---

### Transaction Processing vs. Analytics

Online Transaction Processing (OLTP) Standard CRUD applications, writing data into database and reading it. Blogs / Old Websites / Banking / etc. Online Analytic Processing(OLAP) -> What was revenue for Jan -> June… / Queries to improve business Reading large amounts of data and taking a small part of it Now, we are moving away from using SQL for both… Data Warehousing for OLTP

Data Warehousing Give the analytics people their own read-only database Improves security / isolates processing for the big OLTP data OLTP needs to be highly available and low latency ETL (Extract, Transform, Load) -> Moving OLTP data to OLAP Small businesses usually don’t know about OLAP, the small data works with pure relational Data warehouses can be optimized for analytics patterns indexing algorithms don’t help OLAP queries Data Warehouse is typically a relational database for the queries STAR SCHEMA -> WHERE/WHEN/HOW, one central table that branches off into these dimension tables\*\* Data warehouses have very wide tables and fact tables have over hundreds of columns Dimension tables can also be wide OLTP databases are usually row-oriented

## Chapter 4 Encoding and Evolution

Applications always need to change over time

- Features are added / New User requirements come in / Business changes Need to change the data, like adding a new field or modify how object is presented

Applications very often **need** to change data over time.

- Server-side applications can perform a rolling upgrade
  - Deploy to a few nodes at a time and check whether everything is working, then deploy to all
- Client-side -> Some users will never upgrade their software so you need backwards compatibility

Old and New data may co-exist in the system at the same time. Need to maintain backward compatibility and forward compatibility

- Newer code can read data written by older code
- Older code can read data written by newer code

Backward compatibility is typically easier (You know your code and can make sure it works for it) Forward compatibility is difficult because the old code must ignore the data changes that happened in new code

This chapter will look at several formats for encoding data, including JSON, XML, Protocol Buffer, Thrift, and Avro. Then Kleppman will go over how it’s sent over HTTP / RPC / Message Queues

#### Formats for Encoding Data

Programs usually work with data in two representations

- In memory
- Writing data to a file or send it over network
  - Have to encode it in a way the in-memory doesn’t do

Translation is called encoding / serialization

- I feel like this comes up a ton in software engineering
- This is a common problem, so we have a massive amount of libraries and encoding formats to choose from

#### Language Specific Formats

Languages have support for encoding in-memory into byte sequences

- Python has pickle, Java has Serializable
- Very convenient because objects can easily be saved and restored
- Problems
  - Tied to one exact language -> Must commit to using that language forever
  - Has Security flaws -> Requires decoding the bytes and instatiating code (An attack can sneak executable code into the bytes)
  - Versioning doesn’t exist really for these libraries
  - Some libraries have terrible CPU performance

### JSON, XML, and Binary Variants

- Going into formats that can be read by any programming language
- Widely used, accepted, and disliked
- XML
  - Criticized for being too verbose and unnecessarily complciated
- JSON
  - Web browser support
  - SImple
- CSV
  - Less powerful

JSON,XML, and CSV are textual formats and are somewhat human-readable

- Problems
  - Ambiguity around encoding numbers (Can’t differentiate between a string number and int number)
  - JSON can’t distinguish between ints and floating point
  - Problem with dealing with large numbers, like 2^53
    - Lose accuracy
    - Twitter has a problem like this where their Tweet API will send two different responses to cover it
  - JSON / XML support Unicode but not binary string. Most people get around this by encoding binary data as text using Base64
    - Works but increases data size by 33%
  - CSV doesn’t have a schema, application must define meaning of row and columns
    - It’s a vague format (What to do with values that contain a comma or newline?)
    - Not all parsers implement escaping rules
- Overall
  - Good enough for many purposes
  - People agree on the formats. The best part is that you don’t need to get organizations to agree

#### Binary Encoding

For data that’s only internally used, you can use the most compact and fastest encoding format

There exist binary encoding for JSON

- MessagePack, BSON, BJSON, BISON, and Smile are some examples

Have to decide if saving like 20% of space is worth having less human readable format

#### Thrift and Protocol Buffers

Binary encoding libraries that are based on same idea

Define an object schema and then it’ll convert to binary based on it

    struct Person {
      1: required string       userName,
      2: optional i64          favoriteNumber,
      3: optional list<string> interests
    }

Has forward and backwards compatibility

- TODO:Kleppman gives examples of how this works, but I won’t take notes on it now

#### Avro

Also uses a schema to specify structure of data being encoded Uses a writers schema and reader’s schema

- Don’t need to be the same I’m also going to skip this section on how it’s implemented

### Dataflow -> HTTPS / RPC / …

This Chapter will go over common ways of moving this encoded data to where it needs to go

Databases / Service Calls (RPC) / Async Message Parsing (Message Queue)

#### Dataflow Through Databases

Process that writes to a database is doing encoding Process that reads from DB does decoding

Need to be careful of losing fields

- Data written by new version that has fields
- Read and decoded into an object with those fields
  - But it reads and loses the old field that it had
- Updates to DB from that app will have a missing field now

He mentions something about multiple writes / schema changes

- Can use NULL entires for future rows if fields don’t exist anymore Assure forward and backward compatibility

Can do Datadumping at various stages to maintain snapshots of your database

- Data dump will take the latest schema

#### Dataflow Through Services (REST / RPC)

Clients make request sto servers

- Have some API key / method call (GET/ POST)
- Server will make a response and send data back

Web Browsers and Native applications have to agree with what the server is sending

Servers can also make requests to other servers

- Service Oriented Architecture (SOA) or Microservice Architecture

Goal is to make applications easier to change and maintain by having teams own each service

- Don’t need to coordinate with other teams to make their changes
- More isolation

#### Web Services

- HTTP Calls
- REST vs. SOAP
  - REST uses HTTP
  - SOAP uses XML
    - Uses WSDL (Not human readable)
    - SOAP relies on heavy tool support, code generation, and programming language support
    - Fallen out of favor for small companies / non-enterprise companies

#### Remote Procedure Calls

- Also generally not used
- Have problems
  - JavaBeans only works with Java
  - CORBA is insanely complex
  - DCOM is only for Microsoft
- Other problems
  - Based on idea of local function calls
  - Only allows full success or full failure, nothing else
    - Must predict network problems
  - Doesn’t allow for timeouts
    - No way of knowing if something timed out
  - Doesn’t tell you if your response was lost and actualy had succeeded
  - Network requests take time to pass, local functions are always the same time
  - RPC must translate differences in programming languages in client and service
- Is not going away
  - gRPC supports streams
  - Has a lot of new things coming out to realize that network calls and local function calls are different
  - RPC has built in support for Avro encoding binary stuff
  - Support service discovery

#### Message Queues

- Similar to RPC in that it’s sent with low latency
- Use a message broker
- Retry’s / Can guarantee message is always sent / …
- Read Alex Xu for more info

#### Distributed Actor Frameworks

- Actor Model is programming model for concurrency
- Each actor is a client that has its own local state

## Chapter 5 Replication

### Replication

Replication is useful when:

- One system goes down, others still work (no Single Point of Failure - SPF).
- Data doesn’t change over time, making it easy to replicate.

Distributed databases must handle the challenge of data changing over time using strategies like single-leader, multi-leader, and leaderless, each with its pros and cons.

Replication also has its pros and cons, including considerations like Synchronous vs. Asynchronous Replication, handling failed replicas, and the challenge of developers not understanding _eventual consistency_ and checking reads/writes.

#### Leaders and Followers

- Each node that stores a copy is called a replica.
- Every write to a database is first sent to the leader, who then forwards it to the followers.
- This setup is also known as active/passive or master/slave.

#### Synchronous vs. Asynchronous

- In synchronous replication, a user writes to the database, the leader is notified, updates, acknowledges the user, and tells followers to update.
- Pros: Followers are guaranteed to have the same data eventually.
- Cons: Writes won’t work if a follower crashes, and the leader must block all further writes until the follower replica can work.
- Usually, one node is synchronous, and others are asynchronous to avoid system co-dependence. Alternatively, all nodes can be asynchronous, but this may lead to data loss and lowered durability.

#### Adding New Followers

- It’s challenging to add new followers mid-way because clients are constantly changing the database.
- Locking the database would shut down the application, causing a loss of high availability.
- Instead, you can make a snapshot of the leader and then make all the changes to data that the leader does in the timeframe.

#### Node Outages

- The goal is to keep the impact of a node outage as small as possible so the system can keep running.
- For follower failure, followers keep a log of the leader’s changes, and when the node restarts, it reads the log.
- For leader failure, you need to detect that the leader has failed, assign a new leader, and redirect followers/info to the new leader. However, this can introduce issues like data loss with asynchronous leaders and the possibility of creating two new leaders (split brain).
- Deciding what timeout is needed for a leader to be declared dead can be challenging, and it might be better to handle these situations manually.

#### Implementing Replication Logs

- Replication logs can be implemented by sending SQL Insert/Update/Delete directly to the followers.
- There are challenges with certain SQL statements (e.g., NOW() or Rand()), auto-incrementing columns, and dependencies on current DB data.
- Write-ahead Log (WAL) Shipping, Logical Logs, and Trigger-Based Replication are alternative methods with their own advantages and disadvantages.

#### Problem with Replication Lag

- In read-heavy applications, followers can provide faster reads, but what happens if a follower isn’t up to date when a read happens?
- Eventual consistency can usually be achieved by waiting.

#### Reading own Writes

- Applications that allow users to see what they’ve written right after writing have various strategies, including reading from the leader for small edits and tracking replication lag for many edits.
- Dealing with multiple devices and data centers adds complexity.

#### Monotonic Reads

- Monotonic reads are essential to ensure consistency when users make read requests to different followers.

#### Consistent Prefix Reads

- Consistent prefix reads are important to guarantee that writes occur in the right order when being read.

#### Multi-Leader Replication

- Multi-leader replication is a good alternative when connection loss to a leader is a concern, although it adds complexity.
- It’s useful for multiple data centers, reducing latency, and providing redundancy for data center outages.
- However, it introduces issues like data racing and write conflicts between data centers, especially with triggers, auto-increment keys, and integrity constraints.

#### Handling Write Conflicts - Data Racing

- Handling write conflicts (data racing) depends on the replication setup, involving locks and waiting in a single setup or asynchronous writes with conflict resolution in a multi-set up.

#### Multi-Leader Replication Topologies

- Deciding how leaders should send information to other leaders is a key consideration.

#### Leaderless Replication

- Some database systems, like Dynamo, Cassandra, Riak, and Voldemort, use leaderless replication.
- Handling a follower being down involves completing writes on other followers and reading from all followers to compare version numbers.
- Failed nodes catch up by updating their version during reads and through background scans.

#### Quorums and Consistency

TODO

- \[Details on quorums and consistency are not provided in this summary.\]

## Chapter 6 - Sharding

Chapter 5 discussed replication -> Having multiple copies of data on different nodes

### Sharding / Partitioning

Sharding or partitioning allows breaking up data into partitions, where each partition is essentially a small database. This approach is used to distribute a large dataset across many processors, leading to faster lookups for big data.

Usually combined with replication, although the strategy is the same as in Chapter 5, so replication won’t be covered.

---

#### Key Range Partition

- Like an Encyclopedia, group the data.
- Inside each partition/page, the keys can be sorted to improve searching speed.
- Downside is that data is not evenly distributed, leading to hot spots.

#### Partition by Hash

- Hash function evenly distributes the data.
- Also called consistent hashing, although the vocabulary is awkward in some places.
- Range queries aren’t supported, and there is no sorted order to search.

---

#### Skewed Workloads and Relieving Hot Spots

Hash doesn’t fix everything; sometimes there are hot keys (like a celebrity on Instagram). Keys can be split into parts to ease the load, such as adding two random numbers to the celebrity ID to yield more partitions. This splits the writes but means reads need to check all 100 different fields.

---

#### Secondary Indexes

Another index is needed, like occurrence of User 123 or the number of cars with the color red. Relational databases are good at this, but partitioning these indexes is difficult.

---

#### Rebalancing Partitions

Evenly distributing the load of all partitions as data changes over time is essential as systems crash, the dataset increases, RAM increases, queries increase, and CPU increases. Hash mod is not ideal because it requires data to be moved around after it changes (e.g., Mod 10 -> Mod 15).

- Fixed # of Partitions: Start with 100 and don’t change it. New nodes will steal more partitions from all other nodes until balanced. This is used in Riak, Voldemort, ElasticSearch.
- Dynamic Partitioning: No need to waste space; allow it to adjust itself.

## Designing Data Intensive Applications - Chapter 7 Transactions

I’m guessing this is a chapter on concurrency and other things

Many things can go wrong in data systems

- Software or hardware may fail at any time
- Application may crash at any time (Including during a series of operations)
- Writing to Database at the same time
- Race conditions between clients can cause surprising bugs

A Reliable System needs to deal with these faults

For decades, transactions have beent he mechanism of choice for simplifying these issues.

A transaction is a way for an application to group several reads and writes together into a logical unit.

- Transaction succeeds (Commit) or fails (Abort and rollback)
- They’re not a law of nature, just a programming paradigm to simplify the programming model for applications accessing a database.
- Programs can ignore certain potential error scenarios and concurrency issues

This chapter will examine examples of things that can go wrong, and see algorithms that databases use to guard against the issues.

- Will also go deep into area of currency control

### Slippery Concept of a Transaction

Almost all relational databases today, and some nonrelational databases support transactions. General idea has remained the same since 1975 (IBM System R, the first SQL DB)

Transactions have advantages and limitations

- Benefits
  - ACID I know ACID so I won’t bother writing it here, but here’s some fun facts
- ACID is pretty loosely defined. Specifically Isolated
- It’s a mostly just a marketing term
- Systems that aren’t ACID are called BASE (Basically available, soft state, eventually consistent)
  - Even more vague than ACID
  - Anything that isn’t ACID

#### Atomicity

- One thread will execute an operation
  - Other threads won’t see half actions
  - System can only be in full or none state
- It’s not about concurrency, Isolation handles when several processes try to access the same data at the same time
- It’s focused on what happens when data is being processed and not yet done

### Consistency

- Kleppman says word is terribly overloaded
  - Consistent hashing / eventual consistency / replica consistency
  - CAP theorem uses _consistency_ to mean _linearizability_
- Means that there’s certain statements about data that must always be true
  - Accounting system -> Credits and debits must always balance to zero
- If a transactions starts with a valid database according to those invariants, and any writes preserve the validity, then the constraints are always satisfied
- Need to have constraints in place (Or prevent application code) from adding in weird data that violates the invariants rules
- This is not only the job of the database

### Isolation

- Most databases are accessed by several clients
- Need to make sure there aren’t any race conditions with modified data
- Isolation means that concurrently executing transactions are isolated from each other

#### Durability

- Data can be stored without fear of losing it
- Usually means that data has been written to nonvalatile storage like a hard drive or SSD
  - Usually also involves a write-ahead log or similar, which allows for recovery in the event that data structure on disk are corrupted
- Perfect durability does not exist (See Reliability Chapter)
  - Data can be corrupted
  - Power outages can happen
  - Disk can gradually wear away
  - One study found that 30% and 80% of SSD develop at least one bad block during first four years of operation

### Single-Object and Multi-Object Operations

He gave examples of how atomicity / isolation work on individual objects / (rows?)

- I’m gonna go ahead and skip this

Many distributed datastores have abandoned multi-object transactions

- There are some cases where it’s useful
  - Rows that have a foreign key, you can check that the references remain valid(idk this too much)
  - Document Data Model has multiple fields that need to be updated are treated as single object
    - Document databases don’t use joins though. They use Denormalizations
      - Need to update several documents in one go
  - Secondary indexes in databases
    - These are different database objects from a transaction point of view

### Handling Errors and Aborts

A key feature of a transaction is that it can be aborted ACID is based on this

Not all system follow this idea

- Leaderless Replication work on a “best effort” basis
- Database will do as much as it can, and if it gets an error, it won’t undo anything
- Application’s responsibility to recover from errors

Kleppmann says errors will happen, but many software developers prefer to only think about the happy path rather than intricacies of error handling

Aborting isn’t perfect

- If transaction succeeds, but the network response fails, client will retry again (Idemptoency will prevent this)
- If error is due to overload, retrying won’t do anything and will make the problem worse
- Only retry after transient errors (deadlock, isolation violation, network error, failover)
  - Retry after a permanent error is bad (Like a constraint violation)

### Weak Isolation Levels

Concurrency bugs are hard to find by testing (They only appear when timing is unlucky)

- Very difficult to reproduce

Serializable Isolation (Transaction Isolation) have performance costs

To prevent performance costs, systems will use weaker isolation levels.

- Concurrency bugs have led to big loses in money
- People usually just say “Do Serializable” But many population relational databases get by with weak isolation

Don’t blindly rely on tools, we need to develop a good understanding of the kinds of concurrency problems that exist, and how to prevent them. Then, we can build reliable applications using tools at disposal

this section will look at several weak isolation levels that are used in practice and discuss in detail what kinds of race conditions and cannot occur, os that you can decide what levle is appropriate to your aplication.

Then, Kleppmann will discuss serializability in detail

### Read Committed

Most basic level of transaction isolation

- Only see data committed (no _dirty reads_)
- When writing, only overwrite data that has been committed (no _dirty writes_)

I feel like this is pretty straight forward right?

- Dirty read is seeing data that has not yet been committed by a transaction

Why prevent these?

- User sees an unread email, but the counter isn’t updated
  - Seeing partially updated state is confusing for users

**No Dirty Writes**

- Two transactions try to update the database at same time
- Don’t want to overwrite a non-committed value
- If transactions updates multiple objects, this can be bad
  - We lose data from that transaction
  - Alice and Bob try to buy same car and let’s say it requires to DB writes
    - Sale can be awarded to bob, but the invoice can be sent to Alice

##### Implementing Read Committed

Very popular Isolation Level

- It’s a setting in PostgreSQL, SQL Server 2012, MemSQL, and many others

Databases solve this by using row-level locks. When a transaction wants to modify an object, they must acquire a lock first and hold it until transaction is complete.

Preventing dirty reads

- Can use this same lock idea. But one long-write can prevent any reads from reading
- Most databases prefer to just have two versions of data, one pre-commit, and one post-commit
- They show read objects the old value

#### Snapshot Isolation and Repeatable Read

What concurrency bugs is this level missing?

- Alice could view database in inconsistent state
  - Alice can see her balance before transferring money to someone
    - Someone sending her money at the same time can have a different balance
    - For a moment, Alice will see money taken out of the other persons account, but the money in her account hasn’t changed at all

This is called a _non-repeatable read_ or _read skew_

- Kleppman says Skew is unfortunately an overloaded word

Ofc this isn’t a lasting problem, just for brief second. But other cases would make this horrible

- This example is destructive for backups
- Or analytics queries and integrity checks

Snapshot Isolation is the most common solution to this problem.

- Each transaction reads from consistent snapshot of DB

#### Implementation

Typically use write locks to prevent dirty writes and don’t use any locks onr eads

- Reads never block writes and writers never block readers

Database keeps several different committed versions of an object

- Called -> Multi-version concurrency control (MVCC)

Two versions would be okay in the read committed isolation, but this one needs more

Tpyical approach is that read commited uses a separate snapshot for each query, while snapshot isolation uses the same snapshot for entire transaction

In PostgreSQL, transactions are given IDs and snapshots are made for those IDs

- An update is internally translated into a deleted and a create
- Rows that are marked as “delete”, rows that are freshly updated
- Garbage collection will delete the deleted marked rows after some time
- Have multiple copies stored as rows in the DB

#### Visibility rules for observing a consistent snapshot

When transcation reads form DB, transactions IDs are used to decide which objects it can see and which are invisible.

By carefully defining visibility rules, the database can present a consistent snapshot of the database to the application.

Works like

- At start of each transaction, the database makes alist of all the other transactions in progress (It ignores those IDs)
- Any writes made by aborted transactions are ignored
- Any writes made by transactions with a later ID are ignored
- All other writes are visible to the application’s queries.

#### Indexes and snapshot Isolation

How do indexes work in multi-version databse? One option is to have index point to all version of an object.

In practice, many implementation details determine what happens.

- B Trees and using append-only / copy-on-write

### Repeatable Read and Naming Confusion

Snapshot isolation is a useful isolation level, especially for read-only transactions. Many databases call it by different names though.

- Oracle calls it serializable
- PostgreSQL and MySQL call it _repeatable read_

SQL doesn’t have true snapshot isolation, it’s just really similar.

- There’s a big difference in the guarantees it provides

#### Preventing Lost Updates

Have mostly ignored the presence of having two transactions writing concurrently

Lost update can occur in a read-modify-write cycle (reads data, then commits a modified read)

If two transactions do this concurrently, data is lost

- Incrementing a count
- Two users editing a wiki page

#### Atomic write operations

Databases provide atomic update operations

Usually implemented by making an exclusive lock on the object that blocks reads until update is finished

- Called _cursor stability_

#### Explicit Locking

If database built-in atomic operations aren’t good enough, then application code can check for anything also trying to read-modify-update

This can happen in game development, where multiple players move characters simultaneously. It’s not based on the database.

Need to add locks in the code, but it’s very tricky to do

### automatically detecting lost updates

Alternative is to allow these to occur and have a transaction manager detect a lost update, then abort the transaction and force it to retry.

Advantage is that databases can perform this check efficiently in conjunction with snapshot isolation.

- This is what those popular databases from earlier use with their own snapshots.

It’s a great feature

#### Compare and Set

Databases without transactions sometimes have atomic compare-and-set operation. Purpose of this is to avoid lost updates by allowing an update to happen only if the value has not changed since you last read it.

Check to see if old value is different from when the _read-modify-write_ cycle occured

### Conflict Resolution and Replication

Replicated databases are much more difficult

Copies of data on multiple nodes and data can potentially be modified concurrently on different nodes

multi-leader and leaderless replication allow multiple writes to happen concurrently

- techniques based on locks or compare and set won’t work

Common approach is to just allow concurrent writes to have conflicts, then use application code or a data structure to resolve and merge these versions after the fact

Atomic operations can work well too

### Write Skew and Phantoms

We’re not at the end of potential race conditions yet

Imagine doctors in a hospital where there must be at least one on call doctor

- If two doctors check out at the same time, a condition can occur

Snapshot isolation will return true for both of the doctors

### Characterizing a write skew

This is called write skew

It’s neither a dirty write or a lost update, but definitely a race condition

- Can be generalization of the lost update problem. Write skew can occur if two transactions read the same objects, and then update some of those objects

Atomic single object operations don’t help (multiple objects are involved)

The automoatic detection of lost updates doesn’t help Some databases allow contraints, but most don’t have support for multi-object constraints

If serializable isolation level doesn’t work, then second best option is to explicitly lock the rows

### More examples of Write Skew

Meeting Room Booking System

Multiplayer Game Claiming Username Preventing double spending

Phantoms

- All of these examples have a similar pattern
- SELECT query checks for requirement by searching rows
- Depending on result of first query, checks how to continue
- Makes a insert / update / delete to database and commits transaction
- This idea, where the write in one transaction affects a search query, is called _phantom_

Using a lock to prevent this is called “Materializing Conflicts” and removing the phantom.

- introduces lock basd problems now
- Hard to fix completely

### Serializability

We’ve covered some race conditions for read commited and snapshot isolation levels. We covered tricky problems with write skew and phantoms.

- Isolation levels are hard to understand and inconsistently implemented in databases
- Application code is hard to tell if it’s safe to run partiicular isolation levels
- There are no good tools to help detect race conditions
  - There’s no tools or research techniques that have found their way to practical use It’s been like this since the 1970s

Serializable Isolation is regarded as the strongest isolation level

- Performance is slower

The rest of this chapter will explore

- Literally executing transactions in a serial order (Actual Serial Execution)
- Two-Phase Locking
- Optimistic concurrency control techniques

### Actual Serial Execution

Simplest way is to just remove concurrency entirely is to just only run one transaction at a time, in serial order, on a single thread

This was a new invention that came about from improvements in RAM

- RAM was cheap enough to keep a database in memory for transactions\*
- designers realized that OLTP transactions are usually short and very small

#### Encapsulating transactions in stored procedures

Databases can’t just sit around waiting for users to make up their minds if they want to book an airline ticket

Transactions are broken up, databaes don’t allow multi-statement transactions

Application must submit the entire transaction code to the database ahead of a time as a _stored procedure_

Pros

- Code running in DB is diffiuclt to manager compared to application server
  - No version contorl, hard to test, hard to have metrics
- Database is much more performance sensitive

Stored procedures and in-memory data allow executing all transactions on a single thread

#### Partitioning

Makes concurrency control simpler, but limits transaction throughput of the database to the speed of a single CPU core on a single machine.

Tough for high-write throughput, the single-threaded transaction processor can become a bottleneck.

To scale with multiple CPU cores, can potentially partition data (supported in VoltDB)

- Doesn’t work for transactions that need to access multiple partitions
- VoltDB reports a throughout of about 1,000 cross-partition writes per second, which is order of magnitude slower than its single parition throughput and cannot be fixed

### Two-Phase Locking (2PL)

For around 30 years, this was the only algorithm for serializability in databases

- 2PL is NOT 2PC (two phase commit). They are different

Several transactions are allowed to concurrently read the same object as long as nobody is writing to it.

When someone wants to write to object, exclusive access is required

- If transaction A has read an object and B wants to write, B must wait for A to finish w/ commit or abort before it can continue
- If transactions A has written object, and B wants to read, B must wait until A commits or aborts
  - Not allowed to read old versions of objects

Readers and Writers get blocked

This algorithm protects against race conditions

#### Implementation

MySQL(InnoDB) and SQL Server have this available in their serializable isolation level

Blocking of readers and writers is implemented by a lock on each object

- Shared mode and an exclusive mode

Reads must require a lock in shared mode Writes must acquire a lock in exclusive mode Transactions may upgrade from shared to exclusive when they read and then write Once lock is acquired, hold lock until finished with transaction

Called two-phase because first phase is when locks are acquired, second phase is when transaction executes

#### Performance of Two Phase Locking

Performance is very slow compared to weak isolation

- This is why everybody hasn’t been using it since 1970s

Very easy to have a queue of transactions that need to be run

#### Predicate Locks

Can add locks to search queries to like shared / exclusive to prevent write skew

predicate lock applies even to objects that do not yet exist int he database, bu tmigh tin future.

Two phase locks include predicate locks that prevent all forms of write skew and other race conditions

#### Index-range locks

Predicate locks do not perform well

Most 2PL DBs implement index-range locking

Don’t need to lock exact queries, Its safe to simplify a predicate by making the query range wide and locking it wide

#### Serializable Snapshot Isolation (SSI)

Two phase locking doesn’t perform well Serial Execution doesn’t scale well Weak isolation have good performance but have race conditions

Serializable snapshot isolation seems to be promising

- Gives full serializability, bu tonly have a small performance penalty compared to snapshot

First used in 2008 and is the PhD thesis of Michael Cahill

Today (???) SSI is used in both single-node databases (PostgreSQL) and distributed databases(FoundationDB)

#### Pessimisitc versus optimisic concurrency ocntorl

2PL is called pessimistic

Serializable snapshot is an optimisitic concurrency control technique

I’m not gonna bother writing these, Check out the chapter (Or read Alex Xu’s book)

Can reduce contention weakenss of optimisitic locking using atomic operations

- If all transcations want to increment a counter allow them because order doens’t matter

#### Decisions based on an outdated premise

write skew occurs from having an incorrect premise (Data conditions are met and can write)

#### Detecting stale MVCC reads

I’m gonna skip these two pages

Something about how to detect faulty reads / bad premises when using multiple versions of objects

#### Detecting writes that affect prior reads

Also I will skip this one

#### Performance of serializable snapshot isolation

TODO skipping..

It depends on the cases

## Chapter 8 - Trouble With Distributed Systems

“This chapter is a thoroughly pessimistic and depressing overview of things that may go wrong in a distributed system. We will look into problems with networks (“Unreliable Networks”); clocks and timing issues (“Unreliable Clocks”); and we’ll discuss to what degree they are avoidable. The consequences of all these issues are disorienting, so we’ll explore how to think about the state of a distributed system and how to reason about things that have happened (“Knowledge, Truth, and Lies”).”

### Faults and Partial Failures

Distributed systems are unique in that they can have _partial failures_. Some parts of system work great, others are down

These failures are typically _nondeterministic_, they happen at random times

This is what makes distributed systems difficult

#### Cloud Computing and Super computing

There are several philosophies on how to build large-scale computing systems:

- High performance computing (HPC). Supercomputers with thousands of CPUs are typically used in the scientific community.
- Cloud computing
  - Not well defined, but often associated with multi-tenant datacenters with elastic on demand resource allocation
- Traditional enterprise lies somewhere in between

Each of these have their own problems with handling faults.

- Super computer is like a single-node computer. Everything is just reset on a fault

This book focuses on internet services -> They need to always be online with low latency

#### Unreliable Networks

The Distributed systems in this book are _shared-nothing systems_, a bunch of systems connected by a network. The network is the only way those machines can communicate (They don’t share disks)

Networks are not reliable

- Requests can get lost (someone unplugs a cable)
- Request waits in queue and must be delivered later
- Remote node can fail (Crash or powered down)
- Remote stops responded (Very long garbage collection day)
- Remote node can process response, but response has been delayed

The sender can’t even tell whether the packet was delievered. Sender can send a response that gets lost

Usual way of handling this is through timeouts, but you still don’t know if the receiver got it.

#### Network Faults in Practice

One study found a medium sized datacenter found about 12 network faults per month Human error is a major source of outages (misconfigured switches) so redundancy doesn’t help

Public services like EC2 are notorious for having frequent transient network glitches Sharks can bite undersea cables and damage them

It’s important that the software can handle these because they can always occur

#### Detecting faults

Many systems need to automatically detect faulty nodes for clean up

- Load balancer needs to stop sending requests to a dead node
- For single leader follower, dead leader needs to be rotated out

But network uncertainty means it’s hard to tell if a node is dead

- If node crashed but OS is running, a script can notify the other nodes of a crash
- Management interface of network switches can be queried to detect link failures at hardware level
- Router can say ICMP Destination Unreachable
- Kleppman also mentions that you can retry a few times and eventually call it dead
- Xu always just did heart beats

#### Timeouts and Unbounded Delays

There’s no strong number on when to set timeout. They have pros and cons

- Long timeout means users will have to wait longer or see error message
- Short timeout means we can incorrectly declare a node as dead when it only had a temporary slowdown
  - This is especially bad if the node was in the middle of some kind of work
  - Or other nodes are busy with a lot of work already. It’ll bottleneck by shifting responsibility Asynchronous Networks have _unbounded delays_, there’s no upper limit on how long it takes

#### Network Congestion and queueing

Variability of packet delays comes down to traffic and queuing , similar to driving on a highway in your car

Data packets must wait if several nodes are sending to the same destination

If the receiving node has a full CPU, it’ll also queue the task

Virtual Machines can sporadically pause too TCP performs flow control in which a node will limit it’s own packets being sent to avoid overloading the network link

Systems can have variable timeout setting instead of a constant

- They can measure their response times and automatically adjust timeouts based on the data

#### Synchronous Versus Asynchronous Networks

Why can’t we just solve this at the hardware level and make network reliable so that software doesn’t need to worry about it?

Imagine if it could be like phone calls on a fixed telephone network (no VoIP, non-cellular)

Phones use circuits that set a fixed amount of data to be sent. This is synchronous

#### Can we not make network delays predictable

Not gonna write this but TLDR -> Not really

### Unreliable Clocks

On distributed systems, each node can have their own clock time

Time can be important

- When has request timed out
- What is 99th percentile response time fo this service
- How long did the user spend on the site
- Ticketmaster problem
- etc.

Time is hard because communication is not instant Delays due to network. Each machine on the network has it’s on clock, usually a quartz crystal oscillator.

#### Monotonic Versus Time-of-Day Clocks

Computers have two types of clocks NTP -> Network Time Protocol

Time of Day

- Sync to NTP and based on Gregorian calendar

Monotonic Clocks

- Good for measuring duration
- Difference between two checks of the running timer can give info
- Don’t work among multiple CPUs with their own processes
- Usually fine to use for measuring timeouts in distributed systems

#### Clock Synchronization and Accuracy

Clock drift is a thing in quartz clocks.

- Google assumes about a 200ppm for its servers or like 6ms of drift (assuming 30 second resynchronization)
  - About 17 seconds for a clock resynchronized every day
- Leap Seconds are a thing and can crash entire systems
- node can be firewalled off from NTP by accident
- Network delay can mess things up

MiFID II draft European Regulation for high frequency trading requires insane levels of sync’d clocks (100 ms) to help detect market manipulation and flash crash

- They achieve this using GPS receivers, Precision Time Protocol, and careful deployment and monitoring
- Requires a lot of effort and expertise, plenty of ways to go wrong

#### Relying on Synchronized Clocks

Problem is that time is insanely complicated

Another problem is that incorrect clocks easily go unnoticed. Most things work fine if a clock is slightly off, but it’ll continue to drift and then cause a problem

If you have software that requires synchronized clocks, it’s crucial to monitior clock offsets between all machines.

If it’s too far drifted, need to declare machine as dead and remove it.

#### Timestamps for ordering events

Let’s say we have the ticket master problem and several people buy tickets. Who gets to go first in the distributed system?

Time of day is terrible here

Last Write Wins is a widely used conflict resolution strategy

- Problems still occur
- Database writes can disappear
- LWW can’t distinguish between writes that occur in quick succession sequentially
- Two nodes can generate the same timestamp, additional tie breaker value is required

Is it possible to make NTP synch accurate enough to prevent incorrect orderings? Probably not

For correct ordering, you need a more accurate clock source.

- Logical Clocks, are based on incrementing counters, rather than osciallating quartz crystal
  - Safer for ordering events
- Don’t measure time of day, just order of events

#### Clock Readings have confidence interval

A clock reading has a ton of digits up to the nanoseconds, but it can be way off

It’s more like a range of possible times. It can be 95% accurate that it’s within 10.3 and 10.5 seconds

#### Synchronized clocks for global snapshots

Snapshot isolation is done by incrementing transaction ID, but what do we do in a distributed environment

- Pretty sure Xu just gives each cluster their own hash / ID (Used in Twitter Snowflake ID I think)
- And then they have their own increments

It’s possible to use timestamps from the clocks as transaction IDs

- Need to handle uncertainty though

Spanner uses clock’s confidence interval based on TrueTime API

- Spanner with wait the length of the confidence interval to perform the write Google deploys a GPS receiver or atomic clock in each datacenter, allowing clocks to be synchronized

This is an area of active research but haven’t been implemented outside of Google

#### Process Pauses

Let’s consider another dangerous example of clocks in distributed systems

In leader follower, how does a Leader know that it’s still a leader? That it hasn’t been declared dead by the others

One option is for leader to get lease from other nodes. Only one node can hold the lease

- Must periodically renew it’s lease
- Can renew lease every 10 seconds (But this relies on the clock)

If the node unexpectedly pauses for 10 seconds, then it loses it’s lease

- This happens often with garabge collection in many programming languages
- Not to mention virtual environments
- User closes laptop and suspends
- OS does context switch to another thread

Node must assume that execution can be paused for a significant length of time at any point even in the middle of a function call

#### Response time guarantees

You don’t want to have a pause occur during a car crash to drop out the air bags

There are ways to guarantee real-time for hardware. It’s a lot more work though

You can also limit the impact of Garbage Collection

#### Knowledge, Truth, Lies

What do we even know about Distributed Systems then?

We can just make assumptions about a system and state the behavior that will happen

#### Truth Is Defined by the Majority

A node cannot trust it’s own judgement Rely on _quorum_, voting to make decisions

#### Leader and the lock

TODO skipping…

#### Fencing Tokens

TODO skipping…

#### Byzantine Faults

TODO skipping…

## chapter-9-consistency-and-consensus/

https://raymondjones.dev/en/system-design-notes/chapter-9-consistency-and-consensus/

## chapter-10-batch-processes/

https://raymondjones.dev/en/system-design-notes/chapter-10-batch-processes/

## Chapter 11 - Stream Processing

What do we do when input isn’t bounded (Has finite size)

This chapter will look at _event streams_ as a data management mechanism: the unbounded, incrementally processed counterpart to the batch data we saw in the last chapter.

We will look at how streams are represented, stored, and transmitted over a network. In “Databases and Streams” we will investigate relationship between streams and databases. Finally, in “Processing Streams” Kleppmann will explore approaches and tools for processing those streams continually, and ways that they can be used to build applications

### Transmitting Event Streams

In batch processing, inputs and outputs are files. What about for streaming?

When input is a file (sequence of bytes), first step is usually to parse it into a sequence of records. In a stream processing context, the record is known as an event.

- Essentially same thing, a small, self-contained, immutable object containing some details
- Event usually contains a timestamp indicting when it happened according to a time of day clock

i.e user clicks a button or ad or views a page

Event may be encoded as a text string, or JSON, or perhaps in some binary form

How do we send the messages as soon as they arrive?

DB Triggers are a thing in relational databases, but they’re limited on that they can do

### Messaging Systems

Simple way is Unix or TCP connection

Publish / Subscribe model

- What to do if producers overload the consumers
  - Remove messages, buffer messages in queue, or apply backpressure (block producer from sending)

#### Direct Messaging from producers to consumers

UDP multi-cast Brokerless messaging libraries like ZeroMQ StasD use unrelibable UDP messaging for collecting metrics from all machines on the network If consumer is exposed on network, can use HTTP or RTC request

- This is the idea behind webhooks

### Message Brokers

Essentially a DB designed for sending messages

Skipping because I’ve read most of this in Alex Xu’s book

What to do when memory is almost full?

Consumer offsets What to do when consumers are overloaded?

### Databases and Streams

We’ve drawn comparisons between message brokers and databases, even though traditionally, they’re considered different categories of tools.

We saw that log-based message brokers have been successful in taking ideas from databases and applying them to messaging.

We can go in reverse, take ideas from messaging streams and apply them to databases

We can store events like users clicking a button or sensor readings, but we can also store events like a write to a DB

A replication log is a stream of database write requests, produced by the leader. The followers apply that stream of writes to their own copy of the database.

_state machine replication_ principle in “Total Order Broadcast”, which states, if every event is a write to databases and every replica processes same events in same order, replicas will all end up in final state (assuming processing an event is deterministic)

#### Keeping Systems in Sync

Applications must combine different systems. No single systems wins at everything.

We can use data warehouses and then query them

If full periodic database dump is too slow. Sometimes, dual writes can be done

- Application writes to each system when data changes

Dual writes can suffer from race conditions though if two systems want to write into each other at the same time

- Some writes may fail while other succeeds too

#### Change Data Capture

Problem with DB replication logs is that their only internal exposed. Client can’t query it directly.

More recently, DB’s are allowing this. Called, _Change Data Capture_ (CDC)

#### Implementing Change Data Capture

Log consumers can be called _derived data systems_

CDC makes one database a leader and turns others into followers. Database triggers can be used to implement change data capture

- Tend to be more fragile and have performance overheads
- Parsing replication log can be more robust approach

LinkedIn’s Databus, Facebook’s Wormhole, and Yahoo’s Sherpa use this idea at large scale.

#### Initial Snapshot

Having a log of all changes ever made allows reconstruction of the DB

Keeping all changes forever would require too much disk space though. And replaying woudl take too long. Log needs to be truncated

Need to start with a consistent snapshot instead of storing everything Snapshot of DB must correspond to a known position / offset in change log, some CDC tools allow this snapshop facilitiy

#### Log Compaction

Storage engine goes through records with the same key, and throws away duplicates and keeps the end result on that key. This runs in background several times

If a key is deleted, it marks it and removes all instances of it

Supported in Apache Kafka

#### API Support for change streams

DB’s are supporting Change Streams as first-class interface now

ReThinkDB allows queries to subscribe to notifications when results of query change Firebase and CouchDB provide data synchronization based on change feed

VoltDB allows transactions to continuously export data from DB in form of stream

### Event Sourcing

Developed in Domain-Driven-Design (DDD) community. Will talk it briefly because it incorporates useful and relevant ideas for streaming systems

Event sourcing involves storing all changes to the application state as a log (like CDC)

Difference is:

- Data is used as mutable way in CDC
- In event sourcing, application logic is built on basis of immutable events

Powerful technique in data modeling

- Easier to evolve applications over time
- Helps with debugging
- Guards against application bugs

#### Deriving current state from the event log

Event Log must be converted into some version of the application state to be helpful to users

- Shopping cart user might want to see what they added in the past

Replaying logs is option like in CDC

Log Compaction needs to be handled differently

- Events are modeled at higher level, os event expresses intent of user action, not mechanics of the state update
- Later events typically do not override prior events, so you need full history of events to reconstruct final state. Log Compaction is not possible in the same way

#### Commands and Events

In event sourcing, there’s a difference between _events_ and _commands_

Commands are like requests that can be rejected Events are within the constraints and are accepted

#### State, Streams and Immutability

Immutability benefits

Good for financial bookkeeping

Deploying buggy code can never overwrite old data

#### Deriving several views from same event log

Druid for data analytics can ingest directly from Kafka Kafka Connect sinks can export data from Kafka to several different databases

#### Concurrency control

Biggest downside to event sourcing and CDC is consumers of event log are asynchronous, so user may make a write to the log, and then read form a log-derived view

#### Limitations of immutability

Version control systems like Git, Mercurial, and Fossil also rely on immutable data to preserve version history of files

Truly deleting data is hard, since copies can live in many places. SSDs, storage engineers, and filesystems often just write to a new location rather than overwriting. Backups are often deliberately immutably to prevent accidentally deletion or corruption

### Processing Streams

What can you do with streams once you have it?

Three options broadly

- Take data in events and write to data store / DB /cache/ search index
- Push events to users in some way (email, push notification)
- Produce one or many output streams

Rest of this chapter will discuss option 3, making other streams

Code that processes streams is known as an _operator_ or _job_, very similar to Unix and MapReduce

Big different is just that a stream never ends

### Uses of Stream Processing

Stream Processing has long been used for monitoring purposes

- Fraud Detection systems need usage pattern
- Trading systems examine price change
- Manufacturing systems track status of machines
- Military and Intelligence systems track activities of potential aggressor

#### Complex event processing

CEP

Use a high-level declarative query language like SQL, or graphical user interface, to describe the patterns of events that should be detected.

Queries are stored long term, and events continuously flow past them in search of a query that matches even pattern

Esper / IBM InfoSphere Streams / Apama TIBCO StreamBase, anD SQLstream.

#### Stream analytics

Analytics on streams. Similar to CEP, but analytics don’t care about specific event sequences and more on aggregations and statical metrics overall large number of events

Used sometimes in probabilistic algorithms like Bloom filters or set membership

Many Stream processing frameworks are designed with analytics in mind

- Apache Storm, Spark Streaming, Flink, Kafka Streams
- Azure Stream Analytics, Google Cloud Dataflow

#### Maintaining Materialized Views

Having windows of different views of the DB / log of events

#### Search on Streams

Sometimes want to search for individual events based on complex criteria like ful-text search queries

ElasticSearch is good for this

- Percolator feature

Queries are stored and documents run past the queries

#### Message Passing and RPC

skipping this

## Reasoning About Time

Stream processors often need to deal with time

- Analytics that frequent time windows like (Over last 5 minutes)

#### Event Time vs. Processing Time

Processing may be delayed

- Queueing
- Network Faults
- Performance issues
- Restart of stream consumer
- Reprocessing of past events while recovering from a fault

Message delays can mess up message order

Confusing event time and processing time lead to bad data

#### Knowing when your ready

Never sure when you have all the data for a window

Time out and declare a window ready after you haven’t seen events for awhile

- What if a straggler is there?
- Ignore it OR publish a correction

#### Whose clock to use?

When user clicks? When system receives?

Log three timestamps

- Time when it occured
- Time when sent to server
- Time when it was received by server acoording to server clock

Can offset the processing time difference

### Types of Windows

Tumbling Window -> Fixed length, every event only in one window

Hopping Window -> Fixed length, windows can overlap in order to give some smoothing

Sliding Window -> All events that occur within some interval

Sessions window -> No fixed duration, all events for a given user

#### Stream Joins

New events can appear anytime, Joins are harder

#### Stream-Stream join (window join)

skipping

#### Stream-table join(stream enrichment)

skipping

#### Table table join (materialized view maintenance)

## chapter-12-future-of-data-systems/

https://raymondjones.dev/en/system-design-notes/chapter-12-future-of-data-systems/
