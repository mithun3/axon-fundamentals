# axon-fundamentals


## Table of Contents
**[Axon Framework Background](#axon-framework-background)**<br>
**[Architectural Overview](#architectural-verview)**<br>

##Axon Framework Background
###Brief History
* The demands on software projects increase rapidly as time progresses.
* That means that not only projects and code bases become more complex.
* Although there are many applications and frameworks around that deal with scalability issues, such as GigaSpaces and Terracotta, they share one fundamental flaw.
* These stacks try to solve the scalability issues while letting developers develop applications using the layered architecture they are used to.
* The Command Query Responsibility Segregation (CQRS) pattern addresses these issues by drastically changing the way applications are architected.

###What is Axon?
* Axon Framework helps build scalable, extensible and maintainable applications by supporting developers apply the Command Query Responsibility Segregation (CQRS) architectural pattern.
* It does so by providing implementations of the most important building blocks, such as :
  -aggregates 
  -repositories 
  -and event buses (the dispatching mechanism for events).
* Furthermore, Axon provides annotation support, which allows you to build aggregates and event listeners without tying your code to Axon specific logic. 
* Understanding of CQRS is very important (It is out of scope of this document)
* Axon does help when it comes to guaranteeing delivering events to the right event listeners and processing them concurrently and in the correct order. 

###When to use Axon?
* The application is likely to be extended with new functionality during a long period of time.
* The application has a high read-to-write ratio. 

##Architectural Overview
* 
![screenshot of Axom Architecture](https://github.com/mithun3/axon-fundamentals/blob/master/detailed-architecture-overview.png)
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
