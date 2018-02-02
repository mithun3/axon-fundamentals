# Axon Fundamentals


## Table of Contents
**[Axon Framework Background](#axon-framework-background)**<br>
**[Architectural Overview](#architectural-verview)**<br>
**[Messaging Concepts](#messaging-concepts)**<br>

## Axon Framework Background

### Brief History

* The demands on software projects increase rapidly as time progresses.
* That means that not only projects and code bases become more complex.
* Although there are many applications and frameworks around that deal with scalability issues, such as GigaSpaces and Terracotta, they share one fundamental flaw.
* These stacks try to solve the scalability issues while letting developers develop applications using the layered architecture they are used to.
* The Command Query Responsibility Segregation (CQRS) pattern addresses these issues by drastically changing the way applications are architected.

### What is Axon?

* Axon Framework helps build scalable, extensible and maintainable applications by supporting developers apply the Command Query Responsibility Segregation (CQRS) architectural pattern.
* It does so by providing implementations of the most important building blocks, such as :
  -aggregates 
  -repositories 
  -and event buses (the dispatching mechanism for events).
* Furthermore, Axon provides annotation support, which allows you to build aggregates and event listeners without tying your code to Axon specific logic. 
* Understanding of CQRS is very important (It is out of scope of this document)
* Axon does help when it comes to guaranteeing delivering events to the right event listeners and processing them concurrently and in the correct order. 

### When to use Axon?

* The application is likely to be extended with new functionality during a long period of time.
* The application has a high read-to-write ratio. 

## Architectural Overview

* The diagram below shows an example of an extended layout of a CQRS-based event driven architecture. 
* The UI component, displayed on the left, interacts with the rest of the application in two ways: it sends commands to the application (shown in the top section), and it queries the application for information (shown in the bottom section).
![screenshot of Axom Architecture](https://github.com/mithun3/axon-fundamentals/blob/master/detailed-architecture-overview.png)
* Commands are typically represented by simple and straightforward objects that contain all data necessary for a command handler to execute it.
* A command expresses its intent by its name.
* In Java terms, that means the class name is used to figure out what needs to be done, and the fields of the command provide the information required to do it.

* The Command Bus receives commands and routes them to the Command Handlers.
* Each command handler responds to a specific type of command and executes logic based on the contents of the command.
* The command handler retrieves domain objects *(Aggregates)* from a repository and executes methods on them to change their state.
* These aggregates typically contain the actual business logic and are therefore responsible for guarding their own invariants. 
* The state changes of aggregates result in the generation of Domain Events.
* Both the Domain Events and the Aggregates form the domain model.

* Repositories are responsible for providing access to aggregates.
* Typically, these repositories are optimized for lookup of an aggregate by its unique identifier only.
* The repository is also responsible for persisting the changes made to aggregates in its backing storage.

* Axon provides support for both the direct way of persisting aggregates (using object-relational-mapping, for example) and for event sourcing.

* The event bus dispatches events to all interested event listeners.
* This can either be done synchronously or asynchronously.
* Asynchronous event dispatching allows the command execution to return and hand over control to the user, while the events are being dispatched and processed in the background.
* Synchronous event processing, on the other hand, is simpler and is a sensible default.

* Event listeners receive events and handle them. 
* Some handlers will update data sources used for querying while others send messages to external systems.
* Command handlers are completely unaware of the components that are interested in the changes they make. 

### Main Modules

* The Core module contains, as the name suggests, the Core components of Axon (it must always be available on the classpath).
* The Test module contains test fixtures that you can use to test Axon based components, such as your Command Handlers, Aggregates and Sagas. 
* The Distributed CommandBus modules contain implementations that can be used to distribute commands over multiple nodes. 
* The AMQP module provides components that allow you to build up an EventBus using an AMQP-based message broker as distribution mechanism (This allows for guaranteed-delivery, even when the Event Handler node is temporarily unavailable).
* The Spring module allows Axon components to be configured in the Spring Application context.

## Messaging Concepts

### Message

* One of the core concepts in Axon is messaging.
* All communication between components is done using message objects.
* All Messages contain a payload, meta data and unique identifier. 
* The payload of the message is the functional description of what the message means.
* The combination of the class name of this object and the data it carries, describe the application's meaning of the message.

### Commands

* Commands describe an intent to change the application's state. 
* They are implemented as (preferably read-only) POJOs that are wrapped using one of the `CommandMessage` implementations.
* Commands always have exactly one destination.
* Command messages sent over the Command Bus allow for a result to be returned.

### Events

* Events are objects that describe something that has occurred in the application.  
* A typical source of Events is the Aggregate.
* When something important has occurred within the Aggregate, it will raise an Event.
* In Axon Framework, Events can be any object. You are highly encouraged to make sure all Events are serializable.

* When Events are dispatched, Axon wraps them in an `EventMessage`.
* When an Event is raised by an `Aggregate`, it is wrapped in a `DomainEventMessage` (which extends `EventMessage`).
* All other Events are wrapped in an EventMessage.
* Aside from common `Message` attributes like a unique Identifier an `EventMessage` also contains a timestamp. 
* The `DomainEventMessage` additionally contains the type and identifier of the aggregate that raised the Event.
* It also contains the sequence number of the event in the aggregate's event stream, which allows the order of events to be reproduced.


### Queries
* Queries describe a request for information or state. 
* A query can have multiple handlers.
* When dispatching queries, the client indicates whether he wants a result from one or from all available query handlers.

### Unit of Work

* The processing of a message is seen as a single unit.
* The purpose of the Unit of Work is to coordinate actions performed during the processing of a message (Command, Event or Query).

* You are unlikely to need direct access to the Unit of Work.
* It is mainly used by the building blocks that Axon provides.

```
Note that the Unit of Work is merely a buffer of changes, not a replacement for Transactions. Although all staged changes are only committed when the Unit of Work is committed, its commit is not atomic. That means that when a commit fails, some changes might have been persisted, while others are not. Best practices dictate that a Command should never contain more than one action. If you stick to that practice, a Unit of Work will contain a single action, making it safe to use as-is. If you have more actions in your Unit of Work, then you could consider attaching a transaction to the Unit of Work's commit. Use unitOfWork.onCommit(..) to register actions that need to be taken when the Unit of Work is being committed. 
```

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 

* 
* 
* 
* 
