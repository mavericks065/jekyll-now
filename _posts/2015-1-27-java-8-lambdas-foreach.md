---
layout: post
title: Java 8, Lambdas - the ForEach
---
Today I will write a little article about the Lambdas in Java 8 and more precisely the forEach loop. You will tell me that nobody has written something on it ... RIGHT!! Or maybe not ...

Anyway, in java 5 you were doing a loop like that : (with the for and not with the while of course !! )
```java
List<Object> loop = new ArrayList<Object>();
for (int i = 0; i < loop.size(); i++) {
    // action !
}
```

in java 7:
```java
List<Object> list = new ArrayList<>();
for (Object object : list) {
     // action !
}
```

or with the while loop:
```java
List<Object> list = new ArrayList<>();
        Iterator<Object> objects = list.iterator();
        while(objects.hasNext()) {
            // action
        }
```

And in java 8 : the forEach
```java
List<Object> list = new ArrayList<>();
list.forEach( s -> s.toString() /* action */);
```

So as you see before Java 8, your for-each loops where based on external iterations. Before the Lambdas in java 8 there was just one way to have internal iterations and it was to create your collection by implementing an interface and Iterable.

The 2 most important issues of external iterations are :

Java’s for-each loop/iterator is sequential, and must process the elements in the order specified by the collection.
It limits the opportunity to provide better performance by exploiting reordering of the data, parallelism, or anything else.
Sometimes the guarantees of the for each loop (sequential, in-order) are necessary. They can also be an issue for the performance.

External iteration mixes the computation / operation and the order / "how".

Internal iteration is where instead of controlling the iteration, the client delegates that to the library and passes in snippets of code to execute at various points in the computation. Or you can also implement your collection with Iterable...

In the case of Java 8 forEach the control of the operation is handed to the library code, allowing the libraries not only to abstract over common control flow operations, but also enabling them to potentially use laziness, parallelism, and out-of-order execution to improve performance. (Whether an implementation of forEach actually does any of these things is for the implementation to determine; but with internal iteration, they are at least possible, whereas, with external iteration, they are not.)

It also lets the client dictate the operation but lets the library control the "how". This offers several potential benefits: client code can be clearer because it need only focus on stating the problem, not the details of how to go about solving it, and we can move complex optimization code into libraries where it can benefit all users.

If you want to watch the implementation it is on [grepcode](http://grepcode.com/file/repository.grepcode.com/java/root/jdk/openjdk/8-b132/java/lang/Iterable.java#Iterable.forEach%28java.util.function.Consumer%29). The advantages of grepcode : you can navigate into the classes but in case you are not interested here is the code :

There are 3 interesting things here :

* the use of the pattern reactor on the call of the method accept() of Consumer,
* it throws a null pointer exception if your list is null,
* the default method. Yes Iterable is an interface and since Java 8 you can write code in the body of a method if this method is a default method.

If you want to have a look about the performance of simple forEach loops you can look here.

See ya and have fun with your lambdas :-)