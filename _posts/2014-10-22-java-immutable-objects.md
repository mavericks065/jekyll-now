---
layout: post
title: Java Immutable Objects
---
Sometimes when I develop with my friends they ask me: where did you get this habit to use final on all these objects? Why do you always want to use immutable objects?

So let's start by the beginning :)

### What does "final" mean?

Before a variable, it means that the variable won't be able to be modified once it is initiated. And it must be initiated.

Before a method, we are saying this method won't be redefined if a class inherits this method. it will lead to an optimization when we call this method.

Before a class it means, it won't have subclasses of this final class.

Example of this kind of classes: String, Integer ...

Citation of Joshua Bloch :

**"Classes should be immutable unless there's a very good reason to make them mutable... If a class cannot be made immutable, limit its mutability as much as possible."**

### So what are immutable objects?

Immutable objects are simply objects whose state (the object's data) cannot change after construction like Integer or String. They are particularly useful applications because they cannot be corrupted by thread interference or observed in an inconsistent state.

These objects simplify our programs since they :

* are automatically thread-safe and have no synchronization issues
* don't need an implementation of clone
* are simple to construct, use and test
* are reliable
* don't need a copy constructor
* make good Map keys and Set elements

### How do we define immutable objects?

* Don't provide "setter" methods — methods that modify fields or objects referred to by fields.
* Make all fields final (and private)
* Don't allow subclasses to override methods. The simplest way to do this is to declare the class as final. A more sophisticated approach is to make the constructor private and construct instances in factory methods.
* If the instance fields include references to mutable objects, don't allow those objects to be changed:
* Don't provide methods that modify the mutable objects.
* Don't share references to the mutable objects. Never store references to external, mutable objects passed to the constructor; if necessary, create copies, and store references to the copies. Similarly, create copies of your internal mutable objects when necessary to avoid returning the originals in your methods.

Hope it will help other developers :)

