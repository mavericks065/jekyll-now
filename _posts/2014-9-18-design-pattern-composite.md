---
layout: post
title: Design Pattern Composite
---

The intent of the Design Pattern Composite is to compose objects into tree structures to represent part-whole hierarchies.
Composite lets clients treat individual objects and compositions of objects uniformly.

The figure below shows a UML class diagram for the Composite Pattern:

![an image alt text]({{ site.baseurl }}/images/composite-pattern.png "UML Composite Pattern")

### Component

Component is the abstraction for leafs and composites. It defines the interface that must be implemented by the objects in the composition. For example a file system resource defines move, copy, rename, and getSize methods for files and folders.

### Leaf

Leafs are objects that have no children. They implement services described by the Component interface. For example a file object implements move, copy, rename, as well as getSize methods which are related to the Component interface.

### Composite

A Composite stores child components in addition to implementing methods defined by the component interface. Composites implement methods defined in the Component interface by delegating to child components. In addition composites provide additional methods for adding, removing, as well as getting components.

### Client

The client manipulates objects in the hierarchy using the component interface.
A client has a reference to a tree data structure and needs to perform operations on all nodes independent of the fact that a node might be a branch or a leaf. The client simply obtains reference to the required node using the component interface, and deals with the node using this interface; it does not matter if the node is a composite or a leaf.

### Consequences

The composite pattern defines class hierarchies consisting of primitive objects and composite objects. Primitive objects can be composed into more complex objects, which in turn can be composed.
Clients treat primitive and composite objects uniformly through a component interface which makes client code simple.
Adding new components can be easy and the client code does not need to be changed since the client deals with the new components through the component interface.

### Related Patterns

**Decorator Pattern** - Decorator is often used with Composite. When decorators and composites are used together, they will usually have a common parent class. So decorators will have to support the Component interface with operations like Add, Remove, and GetChild.




