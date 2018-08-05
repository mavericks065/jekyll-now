---
layout: post
title: Design Pattern Adapter
---

In our professional projects, there are some patterns we see more often than others. The Design Pattern Adapter is one of them.

## What is the Adapter Pattern?

It converts a class' interface into another interface that our target class ( let's call the Client) is waiting.  Actually, it allows running classes that could not otherwise because of incompatible interfaces.

### Example

We have a database access class which provides the access to database tables and returns the data. This data should be displayed in a tree widget. The table expects the data is to be provided via a certain interface. Instead of adding this interface to the database access class (which would couple the GUI coding very tight to the database access class), we develop an adapter which converts the interfaces of the database access class to the interfaces of the tree widget.

## Schema

By implementing an interface we can replace the adapter and/or the underlying model easily which another adapter/model. Then the application is loosely coupled.

The adapter allows re-using existing coding without changing it. The adapter will make the conversion between the interfaces.

In comparison to a decorator, the adapter pattern only converts interfaces, while the decorator pattern adds new functionality to an existing interface. Therefore the decorator does not change the existing interface.

The figure below shows a UML class diagram for the Adapter Pattern:

![an image alt text]({{ site.baseurl }}/images/adapter-pattern.png "Adapter Pattern")


