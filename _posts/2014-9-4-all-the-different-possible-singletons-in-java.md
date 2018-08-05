---
layout: post
title: All the different possible Design Patterns Singleton in Java
---

## What is the Design Pattern Singleton?

First of all, it is a creation pattern.  The singleton makes sure that only one instance will be instantiated while the application is running. We often use it for classes that do not have states and always do the same processes.

For being sure that there is just one instance of the class, we have to modify the visibility of the constructor: private or at least protected. And to access to the instance we must think about create a static method (a class' method) that will return it.



Different types of Java Singleton

* Classic :

![an image alt text]({{ site.baseurl }}/images/Classic-Singleton.png "Classic Singleton")

* Static :

![an image alt text]({{ site.baseurl }}/images/Static-Singleton.png "Static Singleton")

It has no timing issue since the class loading is thread-safe. The only problem it has is that the static instance is initialized at class loading which makes the loading expensive. Indeed, it does not implement lazy initialization. With the holder method (with inner class) I think it is the best method to create Singleton.

* Synchronized :

![an image alt text]({{ site.baseurl }}/images/Synchro-singleton.png "Synchronized Singleton")

It works well in a multithreaded environment. But the synchronization will cost a lot of time. If there is a lot of data we will have some performance issues.

* Double Check Lock :

![an image alt text]({{ site.baseurl }}/images/Double-Check-Singleton.png "Double Check Singleton")

This code looks good, however, it has the same issue that the previous singleton. Two threads can enter simultaneously in the if block when an instance is equal to null. Then a thread enters into the synchronized block while the other is blocked. When the first thread exits the synchronized block, the waiting thread can then enter this block and initialize the second instance of our Singleton. The problem is that when the second thread enters the synchronized block, it does not check if the instance is always null. We need a second check for instance.

The failure of the DCL singleton is due to the model of the JVM memory. The memory model allows what is known as "out-of-order writes". The order of the instantiation will depend on the Just-In-Time compiler.

* ThreadLocal :

![an image alt text]({{ site.baseurl }}/images/Threadlocal-singleton.png "Threadlocal Singleton")

A ThreadLocal variable is a different copy for each thread that is using it. Like that every thread can use his own version of the variable with his value without manipulating other variables and values. As the variable is not shared between the threads there is no writing problem.

But it seems ThreadLocal is not efficient and is based on synchronization.

* Volatile :

![an image alt text]({{ site.baseurl }}/images/volatile-singleton.png "Volatile Singleton")

Volatile will help the developer to be sure that we won't use the cache.

But if there are other attributes they must be volatile too.  This way of doing the java singleton allows the reorganization of reads/writes of volatile variables compared to the read / write non-volatile variables. This means that, unless all resources are volatile, (if there is a second thread but it should have been another thread if not we use a classic singleton) thread 2 may perceive the effects of the constructor after the new instance is referenced Singleton created. The solution is to declare all variables as volatile, resulting in the lack of use of records and performance degradation.

* Holder :

![an image alt text]({{ site.baseurl }}/images/inner-class-Singleton.png "Holder Singleton")

This way of doing the singleton is an adaptation of the static method.

In doing this you can be sure it will be "Thread-safe"  because there will be a late loading of the inner class just when the application will call the Singleton Class for the first time (on the first call of the getInstance). Then it works on every JVM.

* Serialization :

![an image alt text]({{ site.baseurl }}/images/serialization-singleton.png "Serialization Singleton")

We can instantiate objects in Java by deserializing. If our singleton implements java.io.Serializable we must prevent its deserialization for not creating many instances. That is why we use the method "readResolve".

* Enum :
It is a simple implementation, but one of the two big disadvantages is that it is available just since Java 1.5. The second disadvantage: it is not really flexible.