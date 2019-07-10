---
layout: post
title: How to create Apache Spark dataframes with null values?
---

Working at the moment on a data analytics project we use Apache Spark with Scala and whole lot of other framework and technologies.

Often while doing unit tests we want to represent data structures with null values in some of the columns of our dataframes. We noticed something interesting about type inference:

This runs perfectly
```
val stuff = Seq(
  (2, null, 1L),
  (1, null, 1L)
).toDF("a", "b", "c")
  .withColumn("other_col",
    when(col("a").isNull, map(Seq(col("c"), col("b")): _*))
      .when(col("a").isNotNull, map(Seq(col("a"), col("b")): _*))
      .otherwise(lit(null))
  )

stuff.count() shouldEqual 2
```

However this code:
```
val stuff = Seq(
  (null, null, 1L),
  (1, null, 1L)
).toDF("a", "b", "c")
  .withColumn("other_col",
    when(col("a").isNull, map(Seq(col("c"), col("b")): _*))
      .when(col("a").isNotNull, map(Seq(col("a"), col("b")): _*))
      .otherwise(lit(null))
  )

stuff.count() shouldEqual 2
```

throws the following:
```
scala.Any
java.lang.ClassNotFoundException: scala.Any
```


The problem is that Any is a general type and Spark does not know how to serialise it.
In first case it thinks the types are: Integer, Null, Long while in the second case it takes: Any, Null, Long.

We should explicitly provide some specific type, and in our case: Integer. null cannot be assigned to Int therefore we will declare it as java.lang.Integer.

I heard here and there that if we use Option it would solve our problem. This is not the case.

These cases don’t work:
```
val stuff = Seq(
  (null, null, 1L),
  (1, null, 1L)
).toDF("a", "b", "c")
```

```
val stuff = Seq(
  (None, None, 1L),
  (Some(1), None, 1L)
).toDF("a", "b", "c")
```

This one works because it has no scala.Any in the picture:
```
val stuff = Seq(
  (3, null, 1L),
  (1, null, 1L)
).toDF("a", "b", "c")
```

And these ones are the cleanest ways:
```
val tuples: Seq[(Integer, String, Long)] = Seq(
  (null, null, 1L),
  (1, null, 1L)
)

val stuff = tuples.toDF("a", "b", "c")
```

```
val tuples: Seq[(Option[Integer], Option[String], Long)] = Seq(
  (None, None, 1L),
  (Some(1), None, 1L)
)

val stuff = tuples.toDF("a", "b", "c")
```

```
case class MyObject(A: Integer,
                    B: Integer,
                    C: Long)

val tuples: Seq[MyObject] = Seq(
  MyObject(null, null, 1L),
  MyObject(1, null, 1L)
)

val stuff = tuples.toDF("A", "B", "C")
```

check out my github page where are the unit tests with the whole code [here](https://github.com/mavericks065/spark_lab/blob/master/src/test/scala/au/com/nig/DataframeCreationExperiment.scala)
