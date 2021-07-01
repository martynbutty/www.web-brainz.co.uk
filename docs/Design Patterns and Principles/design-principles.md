---
title: Design Principles
---
These are some of the more important design principles and strategies to consider during your OOP software design and development activities.

Objects are things with well defined responsibilities
-----------------------------------------------------

At a conceptual level an object is a set of responsibilities (at a specification level it is a set of methods, at an implementation level an object is code and data). The responsibilities define the behaviour of the object. This focuses on what objects are supposed to do and its public interface, rather than the actual implementation.

Objects are responsible for themselves
--------------------------------------

The more that objects become responsible for their own behaviours, the less the controlling programs have to be responsible for them. Careful thought must be given to the separation of responsibilities between objects.

Encapsulation means any kind of hiding
---------------------------------------

*   Data hiding (private data or object composition)
*   Implementation hiding (private methods or Strategy/Bridge pattern)
*   Class hiding (behind an abstract class)
*   Design hiding (Façade pattern)
*   Instantiation hiding (with factories)

Encapsulate what varies
-----------------------

Encapsulated behaviour means that changes to an object’s internal behaviour becomes transparent to other objects. Encapsulation therefore helps to prevent unwanted side-effects because when something is encapsulated, it becomes loosely coupled to the user. The encapsulating layers become the interfaces to design to. Many design patterns utilise this principle and it is an important way of thinking about software design.

Abstraction is the representation of an entity in non-concrete terms
--------------------------------------------------------------------

The process of abstraction within computer science allows you to deal with ideas and entities without being encumbered by unnecessary details. Abstraction is generally accomplished either through abstract classes and interfaces, or with conceptual layers of functionality which expose only the necessary elements of a lower level set of components. The goal of abstraction is generally to allow one or both sides of a relationship to vary independently from the other. For example, if a presentation layer accesses a database through a domain layer serving as the layer of abstraction, the database and method of access can be modified without affecting the presentation layer.

Abstract out variations in behaviour and data with commonality and variability analysis (CVA)
---------------------------------------------------------------------------------------------

Commonality analysis seeks structure that is unlikely to change over time, while variability analysis captures structure that is likely to change within the common set. The commonality analysis is a conceptual perspective where the common concepts will be represented by abstract classes; the variations within the common concept will be implemented by concrete classes. The interface for the abstract class must cater for all the variations among the concrete sub-classes. In general using CVA helps us discover patterns in the problem domain.

Program to an interface not an implementation
---------------------------------------------

Because the interface (or abstract class) represents an abstraction that is unlikely to change; it also hides the subclasses from the client, and helps maintain the “once and only once” principle.

Favour composition (or aggregation) over inheritance
----------------------------------------------------

When a class composes (or aggregates) an object instead of extending an inheritance hierarchy, it improves the cohesion of the class and decouples the implementation of the aggregated object. Inheritance hierarchies also suffer from the [fragile base class problem](fragile).

Think of inheritance as a way of conceptualising variation
----------------------------------------------------------

not for making special cases of existing objects. Instead of considering what might force a change to a design, _consider what you want to be able to change without redesign_, and then to **encapsulate what varies**. Using inheritance for special cases can lead to:

*   Tight coupling because features are indirectly related to each other in the inheritance hierarchy
*   Weak cohesion because methods that performed core functions are scattered among classes
*   High redundancy with similarity of code in different classes
*   Potential class explosion when a new type of specialisation or super class is introduced

Keep variations in a class decoupled from other variations in the class
-----------------------------------------------------------------------

In the [Bridge pattern](bridge) there are two variations in the problem domain. There is a variation of the basic type, this leads to an abstract class and various concrete subclasses. Then there is a variation in method implementations, this results in a separate abstract class with a variety of concrete implementations. The first inheritance hierarchy aggregates the second, and hence the two are decoupled.

Strive for loose coupling
-------------------------

Loose coupling is the state of possessing an association or awareness from one component or system to another by means of abstraction (interface or abstract class). Loose coupling provides the ability for one component to be associated with another while allowing independent variation. For example, if component A interacts with component B through an abstraction of component B, the implementation of component B can be changed without affecting component A. This contrasts with tight coupling – the state of possessing a direct association or awareness between one component or system and another which affects the ability for the associating component or system to vary independently. Decoupling is the process of disconnecting an association or awareness of two components or systems.

Strive for strong cohesion
--------------------------

Cohesion is a measure of how strongly related and focused the various responsibilities of a software module are. Cohesion is usually expressed as "high (strong) cohesion" or "low (weak) cohesion" when being discussed. Modules with high cohesion tend to be preferable because high cohesion is associated with several desirable traits of software including:

*   Robustness
*   Reliability
*   Reusability
*   Understandability

Whereas low cohesion is associated with undesirable traits such as being difficult to maintain, difficult to test, difficult to reuse, and even difficult to understand.

Separate the code that uses an object from code that creates the object
-----------------------------------------------------------------------

This is done by the use of factories, so that the code that uses an object does not need to know how to create that object.

Apply the once and only once rule
---------------------------------

If there is a rule on how to do things, then only implement that rule once. Therefore write a method for the rule that can be called where required. Duplication is bad because if it needs to be changed it will have to be changed in several places, not just one. Hence different parts of the code would be coupled to each other where the duplication exists. Also known as ‘Don’t Repeat Yourself’ (DRY).

Open Closed Principle (OCP)
---------------------------

Software should be designed so that you can extend its capabilities without changing it. I.e. when a new requirement arises, this should be able to be implemented by extending (e.g. adding new classes) the software rather than modifying existing methods or classes.

Dependency Inversion Principle (DIP)
------------------------------------

The dependency inversion principle states that high level modules should not depend on low level modules, instead both should depend on abstractions.

The Liskov Substitution Principle (LSP)
---------------------------------------

A class deriving from a base class should support all the behaviour of the base class, hence both base class and derived classes can be used interchangeably. An object that uses a reference passed to it should not care if that reference is to the base class or the derived class. This implies that subtypes should not add new public methods.

LSP helps us to have well designed inheritance. If your subclass cannot be substituted for the base class which it inherits from, without causing problems (for example methods with the same name but different signatures) the your design does not satisfy LSP. In this case, consider alternative approaches such as using delegation or composition (i.e. the old subclass will hold an instance of the base class).

Ensure that your code is readable
---------------------------------

By “programming by intention” and by using intention-revealing names. Give methods and attributes “intention-revealing names” hence calls to methods are named in a way that clearly describes their intended use.

Consider the testability of your code before coding it
------------------------------------------------------

Testable code is code that can be tested in isolation without having to worry about how it is coupled to other modules or entities. Testable code is:

*   More cohesive because the code is only about one thing
*   More loosely coupled because there are minimal interactions to worry about

Further Reading
---------------

For a good list of design principles see:[http://mmiika.wordpress.com/oo-design-principles/](http://mmiika.wordpress.com/oo-design-principles/)

Note the five foundational principles that provide the acronym SOLID.
