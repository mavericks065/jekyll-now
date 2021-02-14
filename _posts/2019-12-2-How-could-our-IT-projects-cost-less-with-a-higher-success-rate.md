---
layout: post
title: How could our IT projects cost less with a higher success rate?
---

As a former consultant and a software engineer I have been lucky enough to be part of projects in different ASX/CAC 40 companies in France and in Australia and too many of them had gigantic budgets while it could have been significantly less.

What I would like to discuss here is _why large IT projects are squandering money when it could cost less with a higher success rate._

*Disclaimer*: we will mostly talk about projects and/or products that large groups are trying to lead or create. I won’t mention small products from startups or big products that require tens of teams like Netflix. The focus will be more about ASX companies like banks, telCo companies, oil companies, insurances etc…

This article’s aim is to propose another approach of software and IT projects to managers of digital departments in order to succeed more often.

# Problem: IT Projects are too expensive

![an image alt text]({{ site.baseurl }}/images/it-costs.png "IT costs too much")

When we listen to business teams in most companies we pick up that IT is expensive, that it is a line of budget to either reduce or control and where we should be more accurate on how to track it.

Yes, IT costs money but it is not about cost, it is about **investment**. An investment in the interest of your company to help

* your employees to focus on their business in order to make it grow
* make the final customers happy in order to be more profitable

Of course, we could find counter arguments like for instance maintenance or migration projects. Indeed, these projects are forced costs but they can be seen as base for future other projects.

![an image alt text]({{ site.baseurl }}/images/Water_Plant.png "Watering your projects with the right thing")

## Business proposals flaws

I saw business proposals of hundreds of thousands of dollars or even sometimes million of dollars while nothing has been built or POC-ed, scopes haven’t been defined and requirements not been understood yet. 
Sometimes, some companies will even tweak some proposals for clients and propose very similar solutions. While it is often true that architectures and solutions can be alike, businesses are different and their goals are too. 
**Moreover, not all companies have the same maturity to setup the same engineering solutions.** Some solutions might work for your competitor or for some company from another industry but in the end it would not be adequate to your needs.


I have seen business proposals being sent to companies after a salesman and a solution architect have talked to a client for a few hours. And the people who will be using the product are often different from the ones the Solution architects are getting their information from. 
These Solution architects do their best to understand the companies’ problems and then they design and come up with a solution in the business proposal. This solution will then be “implemented” by teams of people who will most of the time barely change anything because of several factors. 
The main one being that the contract and the sales proposition mentioned/ruled on some specific architecture, however after starting the project software engineers often discover that there could be better solutions. 
These projects are not flexible enough to adapt or sometimes technical expertise is lacking in order to adapt the solution. Evolutionary architecture is not encouraged while IT projects are living creatures. 
On this topic, I recommend to read what the role of an architect is and can be [here](https://martinfowler.com/bliki/BuildingArchitect.html)

## Dysfunctional projects

Solution vendors or consulting companies and their clients are bound by contracts of different durations. It is specified that everything outside the initial requirements of the project or does not fit in the scope of the contract cannot be held responsible for the failure of the project.
This is often a problem due to the format of the contracts. Most of the time these projects are bound by Fixed price contracts with fixed scope. 
I will come back to these points later on in the article. 


One of the ways I have seen to remediate to these issues is to have an army of consultants: a few engineers/developers/programmers often labeled analysts or consultants, a few business analysts. 
Then, we would have managers to ensure that these people work correctly together, understand what needs to be done, remove the teams’ blockers and other managers who will explain to the client, internal or external, what happens, showcase the results as well as maintain a trusting relationship. 
Sometimes, a part of the managers workforce is from the client company itself too.


![an image alt text]({{ site.baseurl }}/images/managers-hierarchy.png "The managers hierarchy")

From a pure agile software development perspective and/or psychology point of view we can see that there are a **multitude of problems** with what I have just described. Without talking about Agile, there are a few commons problems inherent to these projects:

* All of these people cost a lot of money, and we could argue whether or not all of them deliver value. On another side, clients want contracts to ensure them that they will get what they want. 
* Big corporations determine their budget based on how much they spent the previous year.  Which means most of the time they need to spend it, not necessarily wisely, because if at the end of the financial year you haven’t spend it then you don’t get to have as much the next one. These contracts can also bind consulting companies or solution vendors and clients to keep spending money on the next financial year in order to ensure funding. This can become political.
 

## Success and failure statistics correlated to the project size

Big projects that start from scratch are the ones most likely to fail by default. Ludovic Cinquin, CEO OCTO Technology, spoke about it in his talk from USI 2018 ([here](https://www.youtube.com/watch?v=Fs0o4D2hg28)). He recommends to read: The Economics of Software from Capers jones, Olivier Bonsignour and Jitendra Subramaniam (on a sub-note I would also recommend to read/listen to Capers Jones). 
From these studies we learn that if the project’s size, in function points analysis, increases then the cost will increase exponentially. Which basically means that the cost of your project is going through the roof.

![an image alt text]({{ site.baseurl }}/images/project-stats.png "Curve of size and quality")

Picture from: https://www.qualimente.com/2017/03/02/effects-of-project-size-and-quality-on-software-project-delivery/

And the [report](https://www.projectsmart.co.uk/white-papers/chaos-report.pdf) from Standish group adds more figures to prove that the bigger the project the more likely it will fail. 
If you are short on time, the pages 2, 3, 4, 5, 16 of the Chaos Report will convey the main ideas...


## No safety net to learn

So what about the teams working on big projects? 
They try their best to deliver projects and to make the software delivery culture of their client change. If by any luck they succeed, it is rarely on time (read report from above) even though massive budgets have been allocated. The excessively high cost of large IT projects prevents any acceptance of failure: it is not an option.
I have been part of a few big projects and people would work long days, weekends, be always reachable and even though they do all of that they end up being late on delivery. Stress builds up, tensions arise, failure is not an option and some people can even question the need for quality. Juniors don't learn much.
In these conditions it is hard to set up a continuous improvement process. A nice article from John Cutler [here](https://cutle.fish/blog/the-psychological-safety-dance) 

One thing we often forget, it is necessary to fail in order to learn and apply what you have learnt down the line. The faster the better but this should be the topic of other articles.

# What could we do to make IT cheaper and also more aligned to what businesses need?

## A 360 framing: another approach

At OCTO Technology, we tried to split projects into small parts with something we call a 360 framing. Once every actor of the project is aligned we then think of how it will be implemented. 
Sometimes, it was all part of one business proposition: framing and implementation as a time and resource material or other formats. 

In some cases, we would advise to first start by proposing a proper framing, and then, depending on the outcome we would decide if we, the client as well as OCTO, wanted to go further or not.

## Alignment

By doing this kind of framing, the goal is to gather all of the people who have an interest in the project: 
* shareholders, 
* teams impacted by the product/projects, 
* third parties, 
* managers
* other stakeholders...

And we would do workshops. From these workshops, we try to understand as much as possible about our client, their needs, the context and what will have to be done. 
We then build a map of who does what, who is responsible for what, who requires what, why and what needs to be created. 
Then, we list the success/failure criteria. We are aligning all the actors of the project and then creating a roadmap and the story map with the client based on their **highest priorities.** 

![an image alt text]({{ site.baseurl }}/images/path-to-the-light.png "The journey")


We try to macro estimate what can and must be done in the future at this stage, then we can agree on attainable goals in the short term and the mid-term.

Similarly, Martin Fowler’s blog highlights Paulo Caroli’s work at Thoughtworks where he created a process named Lean Inception [here](https://martinfowler.com/articles/lean-inception/).

About prioritization this [article](https://cutle.fish/blog/4-prioritization-lessons-using-cost-of-delay-and-cd3) from John cutler is also quite interesting to read.


## Make reasonable choices

After completing the 360 framing and depending on what has been discovered, the clients as well as the consultants can very well say that this is not what they want or not doable given the company constraints or context.

* __If projects were dropped at this stage__ there would be a lot less money wasted than the alternative - going on for months and months until either the budget or the level of trust is completely depleted. 
* If the projects were to continue after the framing process, I think there would be a lot more projects succeeding thanks to a better understanding and alignment of consultants and their clients. 

Both cases look to me like a win for companies. Dropping a project early or ensuring that the project is moving in the right direction is very important for companies to move forward and stay focused.

## Accept uncertainty as part of the process but in a controlled way

This approach, where:

* we consider failing or dropping a project as options
* we can say: “no we won’t do it” or “no it’s not possible” 

can destabilize big companies. 

But we also think that IT is a complex matter to address broad topics. Moreover, given the growth of the IT industry, and how companies need to evolve quickly there is uncertainty that cannot be erased from IT projects. This uncertainty cannot be hidden. It needs to be acknowledged in order to be addressed properly. Indeed, I prefer to see a project being stopped after the framing or after a few iterations without wasting too much money and where the remaining money will be reassigned to other IT topics, as opposed to a big project with 5 teams for 6 months that fails miserably. I reckon the stakeholders also prefer this approach when the financial year approaches.

Following that, we proceed to the implementation for a few iterations, do demonstrations to the client to show how we progress. We go into production from the first iteration. Our goal being: to create an environment where we can build trust and deliver immediate value. If the client is not happy with the delivery speed or how the teams are evolving they can very well stop the project after a few iterations. On the other hand, if the client is happy they can re-iterate the experience.

If the projects are evolving well or succeeding, based on agreed metrics, then we can propose to scale to more teams. Rarely before. We prefer to focus on a few goals and reach them as opposed to having many goals and barely reaching any. Indeed, having a lot of projects or goals in parallel makes it more complicated to see the causes and effects of what is occuring. Therefore, we set our management compass on one or a few selected projects until they bring some value to the client. Only then, can we think of scaling our methodology. 

## Costs and risks

What is the impact from a budget point of view?

If you are tight on budget, doing a framing is two fold: 

* You dig into what you need and you take a lean approach. If it is going to be too expensive you can stop it before the implementation starts.
* There are less risks of going sideways as you know more precisely the scope of what is going to be implemented in the first few iterations.

The goal in this approach is to mitigate the risks associated with the project. Which allows to re-evaluate what people thought at the beginning they wanted and in the end what appears to be what they need. 
If then the projects are done with a time and resource material approach it can be re-evaluated every X-number of iterations/months/weeks or you can set a fixed price contract on sub-scoped parts which can also be renewed. This would allow companies to give more visibility to their finance department. A bit of reading Fixed price approach [here](https://martinfowler.com/bliki/FixedPrice.html) and [here](https://scrumology.com/scrum-and-fixed-price-contracts/). 

Therefore, it is better to build something at a steady pace with good quality instead of building software at scale with a lot of problems and that will not be used at all or for years for an astronomical cost.

Of course projects will still cost a lot of money but they might have better success rate and start delivering value for a lot less money in the meantime. 

In my opinion, it is better to start small with reachable targets and address problems on the way as opposed to going head first with some digital factories and spending ridiculous amount of money for some very low return on investment. Yes, IT is an investment, and if considered as this, then we need to study the ROI that it brings to the company.

# Takeaways

My point of view of why companies end up spending so much money on IT projects:

* impatience: companies want software that is capable of doing everything from the beginning or they want to follow trends.
* _cognitive biases_ on the Software industry thinking it is easy without understanding this industry.
* managers and consulting companies sell the idea that scaling from the beginning is possible in every case.

How to make software an investment with a good ROI and limit the waste:

* build trust, learn and get something delivered before scaling
* negotiate  smaller contracts: start simple then iterate, even for your own contracts
* contract for framing then decide if you want to proceed or not
* time and Material Contracts when possible or Fixed price but not fixed scope
* be business driven
* insist on quality otherwise you will spend more money in the end in enhancements and bug fixes

![an image alt text]({{ site.baseurl }}/images/savings.png "IT is an investment")