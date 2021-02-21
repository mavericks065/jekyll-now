---
layout: post
title: How we use Kotlin to script some tasks in our team. 
---

In my team we work on a lot of technologies, some we chose, some we did not mostly due to  getting existing projects in while consultants were asked to leave our company. 
Nonetheless, we had some load testing to perform on our Open API stack. We decided that we needed to script it with one of the technologies we use. 
What do we currently have on our stack?  
- Java - Spring boot
- Kotlin - Spring boot
- TypeScript - NestJS
- ReactJS with and without Redux and all the possible things around
- VueJS - NuxtJS
- Golang

So one constraint we gave ourselves was to not stray away from our current technologies. Because context switching is already not easy with one technology but right now it is challenging.
As engineers, we have preferences, on my side I must say I was keen to see how easy Kotlin would be in this context knowing that I really like this language. 
I know very well that it could have been done in NodeJS or Golang too. And if we look around not too far: Python. Fair enough but no. 

## What was our goal?

Hit our API, a certain number of times, measure the requests times, observe how our system is reacting with [notebooks and dashboards](https://docs.datadoghq.com/notebooks/) on Datadog then progressively increase the load until we reach the SLA and above. Or until we break it all. #easy

There was no need for business logic, only have a few payloads 99% hardcoded with a criterion that would change from a request to another. 
We could add a parameter in order to test either POST / PUT / DELETE / PATCH of our Open API. Something relatively easy for now. Until we try to test the error use cases, but it was not the first goal.

What we also wanted was a log of start time and end time, so the script would not terminate when the request is published but would also wait for the response.

## How did we do it?

We saw that most of our needs are already in the JDK and we did not need any fancy, heavy, light framework nor any sort of library. #firstVictory

In Kotlin, we don't need to have classes since functions are first class citizens. We created our functions in a kotlin file as simply as that. 

As Http client we opted for the `HttpClient` from the JDK 11. These clients usually follow the same logic whatever library you use, they are created through a builder and can be used to configure per-client state, we can set the preferred protocol version: HTTP/1.1 or HTTP/2. 
This Http client is pretty convenient, the requests can be sent synchronously or asynchronously. 

Instantiation of our http client:

```kotlin
private val httpClient = HttpClient.newBuilder()
    .connectTimeout(Duration.ofSeconds(10)) // arbitrary time that must fit your needs
    .build()
```
Building of a request: 

```kotlin
private fun buildRequest(body: String): HttpRequest = HttpRequest.newBuilder()
    .POST(HttpRequest.BodyPublishers.ofString(body))
    .uri(URI.create("some/url"))
    .setHeader("Authorization", "Some Bearer ?")
    .setHeader("Content-Type", "application/json")
    .build()
```

To send the request: 
 ```kotlin
 httpClient.sendAsync(httpRequest, HttpResponse.BodyHandlers.ofString()) 
 ```

Alright but we wanted to measure the time of the http request between the start time and the response time - there are asynchronous processes in the background that would be monitored by Datadog and so for each request we would log the time of a request which makes snippet above:

```kotlin
private fun sendRequest(httpRequest: HttpRequest): CompletableFuture<Unit> {
    val startTime = LocalDateTime.now()
    return httpClient.sendAsync(httpRequest, HttpResponse.BodyHandlers.ofString())
        .thenApply { response: HttpResponse<String> ->
            val endTime = LocalDateTime.now()
            val requestProcessingTime = Duration.between(startTime, endTime)
            println("$requestProcessingTime ${response.statusCode()} ${response.body()}")
        }
}
```

As we can see in the signature of our function it returns a CompletableFuture. Which means we can trigger functions and non-asynchronous actions depending on the completion of the requests. 

These https requests are executed in a simple loop but to have the program running until the responses of the API we need to ask our program to wait for all the CompletableFutures to complete. and, to do it you need to return another completable future and wait for its completion. 
Alright, let's visualise the code that allows us to do that: 

```kotlin
// Piece of code we put in the main function
(0 until times).map { i -> // loop from integer 0 to the number of times we want it.  
        doSomething(httpCallInterval, i) // This will build a body then pass it to an http requests 
                                         // then send the request which shall return a CompletableFuture
    }.toTypedArray()
        .let { CompletableFuture.allOf(*it) } // Make a completable future of all of these Completable future \o/
        .get() // Make the program to wait for the completable future to complete before exiting. 
```

You can find an example of script in my [github](https://github.com/mavericks065/NIG-Kotlin-async-script).

## Conclusion

It has been a relatively low effort to make this script, a few hours, and for our team it is easy to maintain it. 
Just after one of us did it, a junior had a one off task to execute and even wrote his own Kotlin script after reviewing this one. 
So I would say the learning curve for people who already know a little of Kotlin or Java is non-existing. 
It is extremely easy to execute locally or from Rancher and very lightweight. Thus, I'd recommend people to give it a try. :) 
