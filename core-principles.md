---
layout: page
title: Core Principles
permalink: /core-principles/
---

# Core Principles
The following core principles were given to me by a mentor of mine and help guide my thinking about building software in the large and the small.

### 1. Solve the real problem.
Whenever possible, solve the real problem. It's hard to explain it better than the following. [Yes, I'm going to quote a "capital-A" Agile guy. It's the dogma that sometimes comes along that can cause concern, not all of the ideas. I'm not entirely sure where this quote of his idea is originally from.]

#### Managing Technical Debt:
Ward Cunningham sometimes compares cleaning up the design with paying off debts. Going further, he discusses managing the technical debt on the project. Making hasty additions to the system corresponds to borrowing against the future, taking on debt. Cleaning up the design corresponds to paying off debt. Sometimes, he points out, it is appropriate to take on debt and make hasty changes in order to take advantage of opportunity. Just as debt accumulates interest and grows over time, though, so does the cost to the project of not cleaning up those hasty design changes. Cut corners in the design, he suggests, when you are willing to take on the debt, and clean up the design to pay off the debt before interest grows too high.

### 2. Solve the whole problem.
library, an application, or a system, by **solving the real problem**, you make sure you clearly delineate the **areas of responsibility** of yourself and others using **well-defined interfaces**. By solving the whole problem, you ensure that the well-defined interface best represents the most appropriate division of responsibility. This idea can be represented by the notion that a system component should make the work it does **significantly easier** for clients if they use the component versus doing it themselves.
Note that while your design should aim to solve the whole problem, that doesn't mean your implementation has to. For small problems, like a function or a class, or even a library, you may have time to implement everything in your design at once. But for larger projects, you will need to incrementally fill in the whole problem space with solutions, which is good, because you will learn as you go and the end result will tend to be better.

### 3. The implementation is more flexible than the interface.
If you have **well-defined interfaces** dividing **areas of responsibility**, then you "write to the interface". Doing this properly and taking advantage of the abstraction requires designing the interface to match the division of responsibility (i.e. **solving the whole problem**) and then writing the code to implement as much of that interface as is necessary (maybe all of it). The wrong thing to do is to write an interface that matches (read "exposes") your current implementation out of convenience and then be jailed to that implementation forever.

### 4. Never let perfect stand in the way of very good.
It may be tempting to wait until you have the time, the knowledge, or the inclination to design the "perfect" solution, especially if you aim to **solve the real problem**. However, you must temper this instinct with practicality. While it may look like you are holding out for "the perfect solution" (that solves the whole, real problem), what you are really doing is preventing "the very good solution" that can be applied in the interim. We must recognize that perfection can only be approached asymptotically through evolution of design and implementation: in essence by refining our deployed very good solutions to make them more perfect. Solving the real problem should be applied where scope allows and it should guide our path to tell us where perfect is, but we are allowed to get there in more than one step. Very good solutions have value, and value delayed is value lost.

# Specific Principles
These principles are "rules of thumb" that have proven themselves valuable over time through experience and thus been promoted to the level of a principle.

### 1. Simplicity begets quality.
- "There are two ways of constructing a software design. One is to make it so simple that there are obviously no deficiencies; the other is to make it so complicated that there are no obvious deficiencies. The first method is far more difficult." — C. A. R. Hoare in The Emperor's Old Clothes, CACM February 1981

### 2. Grant the fewest rights necessary to perform an action.
- Enhances real-word security.
- Enhances encapsulation.
- Promotes predictability of behaviour of less-privileged "client" classes/code/etc
- Improves maintenance by having fewer components that use more extensive functionality (i.e. there fewer things to change).
- Guides API users towards the intended usage by only providing the access necessary to accomplish the tasks managed by the API.
- Part of "less is more."
- Granting fewer rights sometimes means splitting a large interface into smaller ones, at least logically.

### 3. When choosing a tool for the job, pick the one that gives you no more power than you need, unless that power is free.
- For example:
  - Use an array or a vector if that's all you need instead of a sorted binary tree.
  - Don't use a 10K XML message to pass 32 bytes of data.
- Counter examples:
  - In C++, use an std::string over a C-string or an std::vector over a raw array in most cases, most often because you really do need the power, but often because you can afford the cost.
  - Use a heavier, standardized XML interface to interface with a distant third party because you need extremely loose coupling.
- Doing so enhances API lifecycle management because you can tell which parts of an interface are really used and for what purpose.
- Promotes efficiency, because simpler operations can often be implemented faster or with fewer resources.

### 4. Make real-world error handling automatic whenever possible.
- Reduces onus on testing because you can be more sure that it works if it's very hard to do it wrong.
- Produces more reliable software by providing "automatic" or "assisted rigour".

### 5. Lifetime matters.
- A lot.
- Promotes easy yet responsible and rigorous control of resource allocation.

### 6. Program using local information; design using global information.
- Also can be stated as "To your code, it's a black box. To you, it's transparent."
- Encapsulation is critical to proper API design (and usage), but the more you (or someone you trust, software-wise) knows about what is really behind that API, the more information you have about the system as a whole and the better you can approach the problem.
- Sometimes good things like encapsulation and layers can hide the fact that you don't need or want them all. Sometimes there is a simpler way.
- Networking should not be magical.
  - This is a specialized version of the black box principle. Encapsulation is excellent and necessary, but you (or someone working with the software) should know how the magic works.
  - A network implies an interface, and interfaces are places that bugs collect. It's hard to design against problems or diagnose bugs in a black box.

### 7. Never treat network resources as if they were local (the NFS lesson).
- They aren't. They don't behave the same way.
- "Timing is everything."
- The prototypical example: Windows Explorer

### 8. Exceptions solve some problems, but not all.
- Don't overuse them.
- Don't assume because an exception is thrown or caught the error is handled.
- Exceptions do not free us from being rigorous about error handling.

### 9. Reap the benefits of having invested in solving a hard problem.
Some problems are inherently difficult to solve, and every time we try to solve them, we will make many mistakes and it will take a lot of testing and experience to be able to fix "all" the bugs and make everything just right. It is solutions to problems like this that especially benefit from being encapsulated well and made available for reuse.
For example, building a set of tools to make working with TCP/IP and sockets easy without sacrificing performance, reliability or correctness is difficult and represents a serious investment. Make that investment pay off by having one implementation serve as many needs as it can. Take advantage of the feedback and bugfixes generated by a larger user base.

### 10. Concurrency is hard.
- Like all hard problems, it's best to solve them "in one place" and leverage it. In other words, focused concurrency is better than distributed concurrency.

### 11. High-availability is best implemented with designed-in redundancy, robustness, and scalability.
- It's the cheapest way, for sure, and it's proven to work.

### 12. Don't trade making the easy easier for making the hard harder.
- Many designs and solutions exist that go to great lengths to make easy problems easier, while inadvertantly making the harder problems harder. The hard problems are the ones we need help with, not the easy ones, so choose solutions that makes the hard easier without making the easy hard.

### 13. Assume the implementation of other components is different from yours.
Even in the most decoupled systems we have, we still make basic assumptions such as "there will be an (IP) network between the components" or "they will have disks and files". While all real interfaces dictate their implementation to some degree, an idealized interface would not. We can't achieve this ideal, but we can keep this goal in mind and aim to keep our interfaces as free of implementation details as possible.
Why do this? At the system level, the components we build today may exist and evolve for years to come. The implementation tools we choose to use today may not be the best choice for tomorrow's problems. However, there are common denominators in the domain of interfaces that we can rely on to be around or be more evolvable as implementation tools change. For example, networks, and specifically IP networks, have proven to be quite stable even in the face of decades of leaps and bounds in software evolution. A TCP application from today can talk to a TCP application from 25 years ago because the rules around connectivity have not changed. This works not just because TCP has remained backwards and forwards compatible for so long, but because the interfaces built to run on networks tend to make the implicit assumption that the system is heterogeneous. A VAX running an ftp client does not assume that a MacBook Pro is running an ftp server written in the same language, on the same architecture, on the same filesystem. The **only shared assumptions are those written into the interface**. Everything else is allowed to be different, and that flexibility buys freedom and decoupling.

### 14. Automate what proves to be frequent.
Given [YAGNI](http://en.wikipedia.org/wiki/You_Ain%27t_Gonna_Need_It), one might think that it leads to a tendency to not deal with general-case problems. YAGNI helps us not generalize too soon, but we must still remember to go back, refactor, and generalize what has proven through experience to be truly general. This approach applies as well to process as it does to programming.
A good rule of thumb for generalizing code has proven to be:
1. The first time you do something, just do it.
2. The second time you do something, if you can use the first stuff as is, do so. If you'd need to make some generalizations, don't yet; just deal with the second case separately.
3. The third time you find yourself working in the same general area, you probably have enough information (based on your experiences doing it twice before) to know how to go back and generalize the first two implementations to cover all three (and most future) cases.
When we are at step one and we think we do know how to do the generalization of step three, it usually turns out that we are either:
- wrong, or
- our past experience has actually taken us through steps one and two before, and we are really already at step three.
Sometimes, the generalization takes the form of a process improvement or a new technique for doing something better. In these cases, we must take the time and effort to capture these improvements (by writing them down), then refine them with the group and then share and teach them to others. That is, we create a "process library" offering tools and techniques for doing frequent tasks in ways that are based on experience and best practices.

### 15. Be prepared to question your original assumptions.
Sometimes design seems to lead to dead ends or roadblocks in all directions. Sometimes it seems that from where you are, every road ahead is a difficult climb. Be prepared to turn around and revisit a previous choice to see if you will still make the same decision given everything you have learned while exploring down that branch of the highway.
Essentially, we're all going to make wrong decisions sometimes. We need to be ready to notice when that is, and go back and change our minds.
