# Notes-of-Designing-Data-Intensive-Applications-
Notes of book &lt;Designing Data-Intensive Applications>

# Chapter 1

Three concerns that are important in software systems:

1. Reliability

The system should continue to work correctly (performing the correct function at the desired level of performance) even in face of hardware or software faults, and human error.

Fault-tolerance mechanisms should be designed to prevent faults from causing failures. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user. 

In such fault-tolerant systems, it can make sense to increase the rate of faults by triggering the deliberately - for example, by randomly killing individual processes without warning. <b>By deliberately inducing faults</b>, you ensure that the fault-tolerance machinery is continually exercised and tested, which can increase your confidence that faults will be handled correctly when they occur naturally. The [Netflix Chaos Monkey](https://medium.com/netflix-techblog/the-netflix-simian-army-16e57fbab116) is an example.

>This was our philosophy when we built Chaos Monkey, a tool that randomly disables our production instances to make sure we can survive this common type of failure without any customer impact. 

+ Hard disk failure

Mean time to failure (MTTF) of hard disks is about 10 to 50 years.

（1） Add redundancy to the individual hardware components: Disks mey be set up in a RAID configuration(?); Servers may have dual power supplies and hot-swappable(?) CPUs, and datacenters may have batteries and diesel generators for backup power.

（2） Use software fault-tolerance techniques

+ Software errors

 (1) Carefully thinking about assumptions and interactions in the system;
 
 (2) Thorough testing;
 
 (3) Process isolation;
 
 (4) Allowing processes to crash and restart;
 
 (5) Measuring, monitoring, and analyzing system behavior in production.
 
+ Human errors

 (1) System design: well-designed abstractions, APIs and admin interfaces;
 
 (2) Provide fully featured non-production sandbox environment for people to explore and experiment safely, using real data, without affecting real users;
 
 (3) Thorough testing; automated testing;
 
 (4) Set up detailed and clear monitoring, such as performance metrics and error rates;

2. Scalability

As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth.

+ Describing Load

Load Parameters: requests per second (to a Web Server); the ratio of reads to writes (in a Database); the number of simultaneously active users (in a chat room); the hit rate (on a cache)

+ Describing Performance

Throughput: the number of records we can process per second;

Response Time = Service Time + Network Delays + Queueing Delays;

Usually it is better to use percentiles than average response time. The median is also knowsn as the 50th percentile, abbr. p50. In order to figure out how bad your outliers are, you can look at higher percentiles: the 95th, 99th, 99.9th percentiles. p95, i.e. the 95th percentile, means 95% of requests are faster than this threshold. High percentiles of response times, also known as tail latencies, are important because they directly affect users' experience of the service, e.g. for Amazon, the customers with the slowest requests are often the most valuable customers.

Queueing delays, caused by a small number of slow requests holding up the processing of subsequent requests, i.e. head-of-line blocking, often account for a large part of the response time at high percentiles.

Latency: the duration that a request is waiting to be handled - during which it is latent, awaiting service;

+ Approaches for Coping with Load

Good architectures usually involve a pragmatic mixture of *scailing up* (vertical scaling, moving to a more powerful machine) and *scaling out* (horizontal scaling, distributing the load across multiple smaller machines).

Some systems are *elastic*, meaining that they can automatically add computing resources when they detect a load increase.

While distributing stateless services across multiple machines is fairly straitforward, taking stateful data systems from a single node to a distributed setup can introduce a lot of additional complexity.

3. Maintainability

The system should be easily envolved and worked on by many different people productively.
