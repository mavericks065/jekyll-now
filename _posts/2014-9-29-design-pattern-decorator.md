---
layout: post
title: Design Pattern Decorator
---
The intent of the Design Pattern Decorator is to add responsibilities statically or dynamically to an object.

### Implementation

The figure below shows a UML class diagram for the Decorator Pattern:

![an image alt text]({{ site.baseurl }}/images/Decorator-Pattern.png "Decorator Pattern")

### Component

Interface for objects that can have responsibilities added to them dynamically.

### ConcreteComponent

Defines an object to which additional responsibilities can be added.

### Decorator

Maintains a reference to a Component object and defines an interface that conforms to Component's interface.

### Concrete Decorators

Concrete Decorators extend the functionality of the component by adding state or adding behaviour.

### Description

The decorator pattern applies when there is a need to dynamically add as well as remove responsibilities to a class, and when subclassing would be impossible due to a large number of subclasses that could result.